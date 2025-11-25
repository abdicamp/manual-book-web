# Panduan Identifikasi Diagram BPMN

## 🎯 Masalah
Anda memiliki file-file gambar diagram, tapi tidak tahu file mana yang harus di-rename menjadi nama apa.

## ✅ Solusi: Script Interaktif

Saya sudah membuat script Python interaktif yang akan membantu Anda mengidentifikasi setiap file gambar dan memetakannya ke nama file yang benar.

## 🚀 Cara Menggunakan

### Langkah 1: Pastikan file gambar ada di root directory
Letakkan semua file gambar diagram di folder root (`/Users/sinergi/API/api-salims/`)

### Langkah 2: Jalankan script
```bash
cd /Users/sinergi/API/api-salims
python3 identify_diagrams.py
```

### Langkah 3: Ikuti instruksi di script
Script akan:
1. Menampilkan daftar semua diagram yang diperlukan
2. Untuk setiap diagram, menampilkan:
   - Deskripsi diagram
   - File-file yang mungkin cocok (berdasarkan keywords)
   - Semua file yang tersedia
3. Anda memilih file mana yang sesuai dengan diagram tersebut
4. Script akan otomatis rename dan pindahkan ke folder `diagrams/`

## 📋 Daftar Diagram dan Deskripsinya

### 1. Business Process Pendaftaran Pelanggan
- **File target**: `process-1-pendaftaran-pelanggan.png`
- **Keywords**: pendaftaran, pelanggan, customer, registration, register
- **Deskripsi**: Diagram dengan 2 swimlane: Pelanggan dan Admin. Proses mulai dari pendaftaran di portal, mengisi data, verifikasi oleh admin, dan approval.

### 2. Business Process Administrasi Sampel Uji
- **File target**: `process-2-administrasi-sampel-uji.png`
- **Keywords**: administrasi, sampel, uji, sample, administration, testing
- **Deskripsi**: Diagram dengan 3 swimlane: Pelanggan, Pelayanan Kepada Admin, dan Manajer Teknis. Proses lengkap dari permintaan pengujian hingga penerbitan LHU.

### 3. Business Process Kaji Ulang Permintaan (KUP)
- **File target**: `process-3-kaji-ulang-permintaan.png`
- **Keywords**: kaji, ulang, permintaan, kup, review, request
- **Deskripsi**: Diagram dengan 3 swimlane: Kaji Ulang Permintaan, Manager Teknis, dan Analis. Proses parallel check untuk peralatan, bahan uji, dan ketersediaan analis.

### 4. Business Process Verifikasi Pembayaran
- **File target**: `process-4-verifikasi-pembayaran.png`
- **Keywords**: verifikasi, pembayaran, payment, verification, cis
- **Deskripsi**: Diagram dengan 2 swimlane: Data Integration (API CIS) dan Verifikasi Pembayaran (Admin). Proses konfirmasi pembayaran, pencarian data, dan koneksi ke CIS.

### 5. Business Process Pengambilan Sampel
- **File target**: `process-5-pengambilan-sampel.png`
- **Keywords**: pengambilan, sampel, sample, collection, taking
- **Deskripsi**: Diagram dengan 2 swimlane: Pengambilan Sampel dan Admin Persediaan. Proses mulai dari jadwal, persiapan peralatan/bahan, kalibrasi, print barcode, pengambilan di lapangan, dan bawa ke lab.

### 6. Business Process Pengolahan Sampel
- **File target**: `process-6-pengolahan-sampel.png`
- **Keywords**: pengolahan, sampel, processing, sample
- **Deskripsi**: Diagram dengan 1 swimlane: Admin. Proses sederhana: analisa permohonan, bagi sampel, lalu parallel: tambah bahan, dinginkan, dan simpan sampel.

### 7. Business Process Penanganan Sampel
- **File target**: `process-7-penanganan-sampel.png`
- **Keywords**: penanganan, sampel, handling, sample
- **Deskripsi**: Diagram dengan 5 swimlane: PPS, Manager Teknis, Penyelia Penanganan Sampel Uji, Analis, dan Admin. Proses lengkap dari pengambilan hingga penerbitan LHU.

### 8. Business Process Persiapan Pengujian
- **File target**: `process-8-persiapan-pengujian.png`
- **Keywords**: persiapan, pengujian, preparation, testing, test
- **Deskripsi**: Diagram dengan 2 swimlane: Analis dan Admin Persediaan. Proses mulai dari jadwal pengambilan, cek permintaan, persiapan peralatan/bahan (parallel), konfirmasi, dan kalibrasi jika perlu.

### 9. Business Process Penerbitan LHU
- **File target**: `process-9-penerbitan-lhu.png`
- **Keywords**: penerbitan, lhu, laporan, hasil, uji, report
- **Deskripsi**: Diagram dengan 4 swimlane: Data Integration, Admin, Verifikasi Pembayaran, dan Pelanggan. Proses mulai dari cek pembayaran, kalkulasi biaya, tagihan, pembayaran, hingga download LHU.

### 10. Business Process Manajemen Persediaan
- **File target**: `process-10-manajemen-persediaan.png`
- **Keywords**: manajemen, persediaan, inventory, stock, opname
- **Deskripsi**: Diagram dengan 2 swimlane: Admin Persediaan dan Penyelia. Proses mulai dari buat daftar, stock opname (parallel dengan cek batas minimum), rekap, konfirmasi, update data, dan disposal jika kadaluarsa.

### 11. Business Process Manajemen Aset
- **File target**: `process-11-manajemen-aset.png`
- **Keywords**: manajemen, aset, asset, peralatan, equipment, kalibrasi, calibration
- **Deskripsi**: Diagram dengan 4 swimlane: Analis, Manajemen Aset Supervisor, Manajer Lab, dan Internal/External Kalibrasi. Ada 2 proses parallel: maintenance (pemeriksaan, pemeliharaan) dan calibration (program, jadwal, permintaan, kalibrasi).

### 12. Business Process To Be - Integrasi Data
- **File target**: `integrasi-data.png`
- **Keywords**: integrasi, data, integration, to be, overview
- **Deskripsi**: Diagram overview dengan 4 kotak Business Process (Administrasi Sample Uji, Penanganan Sampel, Manajemen Persediaan, Manajemen Aset) dan 1 kotak Integrasi Data di bawah. Ada panah-panah menghubungkan semua proses ke Integrasi Data.

## 💡 Tips

1. **Buka file gambar** untuk melihat isinya sebelum memilih
2. **Perhatikan jumlah swimlane** - ini bisa membantu identifikasi
3. **Perhatikan keywords** - nama file biasanya mengandung kata kunci
4. **Gunakan deskripsi** - deskripsi menjelaskan struktur diagram
5. **Skip jika tidak yakin** - Anda bisa skip dan lanjutkan nanti

## 🔄 Jika Salah Pilih

Jika Anda salah memilih file, jangan khawatir:
1. File yang sudah dipindahkan ada di folder `diagrams/`
2. Anda bisa rename manual atau jalankan script lagi
3. Script akan membuat backup jika file target sudah ada

## 📞 Troubleshooting

### Script tidak berjalan
```bash
# Pastikan Python 3 terinstall
python3 --version

# Berikan permission execute
chmod +x identify_diagrams.py

# Jalankan dengan python3
python3 identify_diagrams.py
```

### File tidak ditemukan
- Pastikan file gambar ada di root directory (bukan di subfolder)
- Pastikan ekstensi file adalah .png, .jpg, atau .jpeg
- File di folder `images/` dan `diagrams/` akan diabaikan

### Tidak yakin file mana yang dipilih
- Buka file gambar untuk melihat isinya
- Bandingkan dengan deskripsi diagram
- Perhatikan jumlah swimlane dan struktur diagram

