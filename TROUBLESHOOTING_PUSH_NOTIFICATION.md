# Troubleshooting Push Notification Tidak Terkirim ke Mobile

## Masalah yang Ditemukan dan Diperbaiki

### 1. **Masalah Logika Zona Matching (FIXED)**
**Lokasi**: `app/Jobs/ProcessNotificationJob.php` baris 311

**Masalah**:
- Kondisi `if ($smMusers && $this->zonacode == $smMusers->zonaauthority)` terlalu ketat
- Query sudah mencari user dengan `zonaauthority = $zona`, tapi kemudian membandingkan dengan `$this->zonacode` yang mungkin berbeda
- Ini menyebabkan notifikasi tidak terkirim meskipun user ditemukan

**Solusi**:
- Diperbaiki logika matching zona untuk lebih fleksibel
- Sekarang mendukung:
  - Jika `zonacode` dari request cocok dengan zona user
  - Jika `zonacode` null, gunakan zona dari user langsung
  - Jika zona user mengandung `zonacode` (untuk multiple zones)

## Checklist Troubleshooting

### 1. **Cek Firebase Configuration**
```bash
# Cek apakah file credentials ada
ls -la storage/app/firebase-auth.json

# Atau cek env variable
echo $FIREBASE_CREDENTIALS
echo $GOOGLE_APPLICATION_CREDENTIALS
```

**File**: `config/firebase.php`
- Pastikan path ke Firebase credentials file benar
- Default: `storage/app/firebase-auth.json`

### 2. **Cek Queue Worker Berjalan**
```bash
# Cek apakah queue worker berjalan
php artisan queue:work --queue=notifications

# Atau jika menggunakan supervisor/pm2
ps aux | grep queue
```

**Masalah**: Jika queue worker tidak berjalan, job tidak akan diproses.

### 3. **Cek Log untuk Error**
```bash
# Cek log Laravel
tail -f storage/logs/laravel.log | grep -i "notification\|fcm\|firebase"

# Cek log khusus notification
tail -f storage/logs/laravel.log | grep -i "FCM\|notification\|zona"
```

**Cari error seperti**:
- `Firebase messaging not initialized`
- `FCM token is empty`
- `Zone code mismatch`
- `Firebase credentials file not found`

### 4. **Cek FCM Token User**
```sql
-- Cek apakah user memiliki FCM token
SELECT id, username, token_fcm, zonaauthority 
FROM users 
WHERE token_fcm IS NOT NULL 
AND token_fcm != '';

-- Cek zona authority user
SELECT id, usernam, zonaauthority 
FROM sm_m_user 
WHERE zonaauthority IS NOT NULL 
AND zonaauthority != '';
```

**Masalah**: 
- User tidak memiliki FCM token
- FCM token kosong atau invalid

### 5. **Cek Zona Authority Matching**
```sql
-- Cek zona dari request vs zona user
SELECT 
    u.id,
    u.username,
    u.token_fcm,
    sm.zonaauthority as user_zona,
    'ZONA_DARI_REQUEST' as request_zona
FROM users u
JOIN sm_m_user sm ON u.username = sm.usernam
WHERE u.token_fcm IS NOT NULL
AND u.token_fcm != '';
```

**Masalah**: 
- Zona dari request tidak cocok dengan zona authority user
- User memiliki multiple zones (comma-separated) tapi matching tidak tepat

### 6. **Cek Notification History**
```sql
-- Cek status notification history
SELECT 
    batch_id,
    status,
    status_message,
    error_message,
    user_count,
    success_count,
    failure_count,
    skipped_count,
    created_at,
    started_at,
    completed_at
FROM notification_history
ORDER BY created_at DESC
LIMIT 10;
```

**Cek**:
- Status: `initial`, `processing`, `completed`, `error`
- Jika `error`, lihat `error_message`
- Jika `failure_count` tinggi, ada masalah dengan pengiriman

### 7. **Cek Job Queue**
```sql
-- Cek job yang pending/failed
SELECT 
    id,
    queue,
    attempts,
    reserved_at,
    available_at,
    created_at
FROM jobs
WHERE queue = 'notifications'
ORDER BY created_at DESC
LIMIT 10;

-- Cek failed jobs
SELECT 
    id,
    queue,
    payload,
    exception,
    failed_at
FROM failed_jobs
WHERE queue = 'notifications'
ORDER BY failed_at DESC
LIMIT 10;
```

### 8. **Test Manual Send Notification**
```php
// Test di tinker
php artisan tinker

// Test send notification
$helper = new \App\Traits\MyHelper();
$result = $helper->sendNotification(
    'FCM_TOKEN_DISINI',
    'Test Title',
    'Test Body',
    'test_screen'
);
dd($result);
```

## Common Issues dan Solusi

### Issue 1: "Firebase messaging not initialized"
**Solusi**:
1. Pastikan file `storage/app/firebase-auth.json` ada
2. Pastikan file credentials valid (JSON format)
3. Cek permission file: `chmod 644 storage/app/firebase-auth.json`

### Issue 2: "FCM token is empty"
**Solusi**:
1. Pastikan user sudah login dan register FCM token
2. Cek tabel `users` kolom `token_fcm`
3. Pastikan mobile app mengirim token saat login

### Issue 3: "Zone code mismatch"
**Solusi**:
1. Cek zona dari request vs zona authority user
2. Pastikan format zona sama (case sensitive)
3. Jika user punya multiple zones, pastikan matching logic benar

### Issue 4: Queue tidak diproses
**Solusi**:
```bash
# Start queue worker
php artisan queue:work --queue=notifications --tries=3

# Atau menggunakan supervisor
# Edit /etc/supervisor/conf.d/laravel-worker.conf
```

### Issue 5: Notification terkirim tapi tidak muncul di mobile
**Solusi**:
1. Cek FCM token masih valid (tidak expired)
2. Cek mobile app permission untuk notification
3. Cek Firebase console untuk delivery status
4. Test dengan Firebase console langsung

## Debug Steps

1. **Cek Log Notification History**
   - Lihat `notification_history` table
   - Cek status dan error message

2. **Cek Log Laravel**
   - Filter log dengan keyword "notification", "FCM", "firebase"
   - Cari error atau warning

3. **Test dengan Single User**
   - Test send notification ke satu user dulu
   - Pastikan user punya FCM token dan zona cocok

4. **Cek Firebase Console**
   - Login ke Firebase Console
   - Cek Cloud Messaging > Reports
   - Lihat delivery status

5. **Test Manual**
   - Gunakan tinker untuk test send notification
   - Pastikan Firebase credentials valid

## Monitoring

### Query untuk Monitoring
```sql
-- Summary notification history
SELECT 
    DATE(created_at) as date,
    status,
    COUNT(*) as count,
    SUM(user_count) as total_users,
    SUM(success_count) as total_success,
    SUM(failure_count) as total_failure,
    SUM(skipped_count) as total_skipped
FROM notification_history
WHERE created_at >= DATE_SUB(NOW(), INTERVAL 7 DAY)
GROUP BY DATE(created_at), status
ORDER BY date DESC, status;
```

## Contact & Support

Jika masalah masih terjadi setelah mengikuti checklist di atas:
1. Cek log file lengkap
2. Screenshot error message
3. Cek notification_history untuk batch_id yang error
4. Test manual dengan tinker

