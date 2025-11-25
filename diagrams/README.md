# Diagram Business Process SALIMS

Folder ini berisi diagram BPMN untuk semua proses bisnis dalam sistem SALIMS.

## 📁 Struktur File Diagram

Semua diagram harus disimpan dengan nama sesuai dengan proses bisnis yang diwakilinya:

### Overview dan Integrasi
- `business-process-overview.png` - Diagram Business Process Overview (4 proses bisnis utama)
- `integrasi-data.png` - Diagram Integrasi Data

### Proses Bisnis Detail
- `process-1-pendaftaran-pelanggan.png` - Diagram Proses 1: Pendaftaran Pelanggan
- `process-2-administrasi-sampel-uji.png` - Diagram Proses 2: Administrasi Sampel Uji
- `process-3-kaji-ulang-permintaan.png` - Diagram Proses 3: Kaji Ulang Permintaan (KUP)
- `process-4-verifikasi-pembayaran.png` - Diagram Proses 4: Verifikasi Pembayaran
- `process-5-pengambilan-sampel.png` - Diagram Proses 5: Pengambilan Sampel
- `process-6-pengolahan-sampel.png` - Diagram Proses 6: Pengolahan Sampel
- `process-7-penanganan-sampel.png` - Diagram Proses 7: Penanganan Sampel
- `process-8-persiapan-pengujian.png` - Diagram Proses 8: Persiapan Pengujian
- `process-9-penerbitan-lhu.png` - Diagram Proses 9: Penerbitan LHU
- `process-10-manajemen-persediaan.png` - Diagram Proses 10: Manajemen Persediaan
- `process-11-manajemen-aset.png` - Diagram Proses 11: Manajemen Aset
- `process-12-proses-approval.png` - Diagram Proses 12: Proses Approval

## 📋 Cara Menambahkan Diagram

1. **Siapkan Diagram BPMN**
   - Buat diagram menggunakan tool BPMN (contoh: Camunda Modeler, Bizagi, Draw.io)
   - Export diagram dalam format PNG dengan resolusi tinggi (minimal 1920px width)
   - Pastikan diagram jelas dan mudah dibaca

2. **Simpan Diagram**
   - Simpan diagram dengan nama sesuai daftar di atas
   - Letakkan file di folder `diagrams/` (relatif terhadap file HTML)

3. **Verifikasi**
   - Buka file `BUSINESS_PROCESS_MANUAL.html` di browser
   - Diagram akan otomatis muncul jika file sudah ada
   - Jika diagram tidak ditemukan, akan muncul placeholder dengan instruksi

## 🎨 Spesifikasi Diagram

- **Format**: PNG (disarankan) atau JPG
- **Resolusi**: Minimal 1920px width untuk kualitas baik
- **Background**: Putih atau transparan
- **Format BPMN**: Mengikuti standar BPMN 2.0
- **Warna**: Gunakan warna yang kontras dan mudah dibaca

## 📍 Mapping Diagram dengan Menu

Diagram sudah dikonfigurasi untuk muncul di section yang sesuai dengan menu sidebar:

| Menu Sidebar | Diagram File | Section ID |
|--------------|--------------|------------|
| Business Process Overview | `business-process-overview.png` | `#business-overview` |
| 1. Pendaftaran Pelanggan | `process-1-pendaftaran-pelanggan.png` | `#process-1` |
| 2. Administrasi Sampel Uji | `process-2-administrasi-sampel-uji.png` | `#process-2` |
| 3. Kaji Ulang Permintaan (KUP) | `process-3-kaji-ulang-permintaan.png` | `#process-3` |
| 4. Verifikasi Pembayaran | `process-4-verifikasi-pembayaran.png` | `#process-4` |
| 5. Pengambilan Sampel | `process-5-pengambilan-sampel.png` | `#process-5` |
| 6. Pengolahan Sampel | `process-6-pengolahan-sampel.png` | `#process-6` |
| 7. Penanganan Sampel | `process-7-penanganan-sampel.png` | `#process-7` |
| 8. Persiapan Pengujian | `process-8-persiapan-pengujian.png` | `#process-8` |
| 9. Penerbitan LHU | `process-9-penerbitan-lhu.png` | `#process-9` |
| 10. Manajemen Persediaan | `process-10-manajemen-persediaan.png` | `#process-10` |
| 11. Manajemen Aset | `process-11-manajemen-aset.png` | `#process-11` |
| 12. Proses Approval | `process-12-proses-approval.png` | `#process-12` |
| Integrasi Data | `integrasi-data.png` | `#integration` |

## ✅ Checklist

- [ ] Diagram Business Process Overview
- [ ] Diagram Proses 1: Pendaftaran Pelanggan
- [ ] Diagram Proses 2: Administrasi Sampel Uji
- [ ] Diagram Proses 3: Kaji Ulang Permintaan (KUP)
- [ ] Diagram Proses 4: Verifikasi Pembayaran
- [ ] Diagram Proses 5: Pengambilan Sampel
- [ ] Diagram Proses 6: Pengolahan Sampel
- [ ] Diagram Proses 7: Penanganan Sampel
- [ ] Diagram Proses 8: Persiapan Pengujian
- [ ] Diagram Proses 9: Penerbitan LHU
- [ ] Diagram Proses 10: Manajemen Persediaan
- [ ] Diagram Proses 11: Manajemen Aset
- [ ] Diagram Proses 12: Proses Approval
- [ ] Diagram Integrasi Data

## 💡 Tips

1. **Konsistensi**: Gunakan style dan warna yang konsisten untuk semua diagram
2. **Legenda**: Tambahkan legenda jika menggunakan simbol khusus
3. **Ukuran**: Pastikan teks dalam diagram mudah dibaca saat di-zoom
4. **Format**: Simpan dalam format PNG untuk kualitas terbaik
5. **Testing**: Test diagram di berbagai ukuran layar (desktop, tablet, mobile)

