# Panduan Menambahkan Gambar ke Manual Book

## 📸 Cara Menambahkan Screenshot ke HTML

### Opsi 1: Menggunakan File Gambar (Direkomendasikan)

1. **Buat folder `images`** di direktori yang sama dengan file HTML:
   ```
   /Users/sinergi/API/api-salims/
   ├── BUSINESS_PROCESS_MANUAL.html
   ├── images/
   │   ├── testing-order-form.png
   │   ├── testing-order-form-2.png
   │   └── ...
   ```

2. **Simpan screenshot** dengan nama:
   - `testing-order-form.png` - Screenshot form Testing Order lengkap
   - `testing-order-form-2.png` - Screenshot form Testing Order dengan section Quality Reference dan Parameter

3. **Path sudah diset** di HTML sebagai: `images/testing-order-form.png`

### Opsi 2: Menggunakan Base64 Encoding (Embed Langsung)

Jika Anda ingin gambar ter-embed langsung di HTML tanpa file terpisah:

1. **Convert gambar ke Base64**:
   ```bash
   # Menggunakan command line (Mac/Linux)
   base64 -i screenshot.png -o base64.txt
   
   # Atau menggunakan online tool:
   # https://www.base64-image.de/
   # https://base64.guru/converter/encode/image
   ```

2. **Ganti tag img** di HTML:
   ```html
   <!-- Sebelum -->
   <img src="images/testing-order-form.png" alt="Form Testing Order">
   
   <!-- Sesudah (dengan base64) -->
   <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA..." alt="Form Testing Order">
   ```

### Opsi 3: Menggunakan URL Eksternal

Jika gambar di-host di server atau cloud storage:

```html
<img src="https://yourdomain.com/images/testing-order-form.png" alt="Form Testing Order">
```

## 📋 Daftar Screenshot yang Perlu Ditambahkan

Berdasarkan screenshot yang telah dibagikan:

1. **testing-order-form.png** 
   - Form Testing Order dengan section SAMPLE, QUALITY REFERENCE, dan PARAMETER
   - Sudah ditambahkan di bagian "Mengisi Form Permintaan Pengujian Sampel"

2. **planning-taking-sample-form.png**
   - Form Planning Taking Sample dengan section SAMPLE, EQUIPMENT, LABOUR, dan PARAMETER
   - Sudah ditambahkan di bagian "Pengambilan Sampel" → "Planning Taking Sample"

3. **taking-sample-form.png**
   - Form Taking Sample untuk pengambilan sampel aktual di lapangan
   - Sudah ditambahkan di bagian "Pengambilan Sampel" → "Sub-process: Pengambilan Sampel Dilapangan" → "Melakukan Pengambilan Sampel"

4. **sample-handling-form.png**
   - Form Sample Handling untuk penanganan sampel di laboratorium
   - Sudah ditambahkan di bagian "Penanganan Sampel" → "Fase 1: Penerimaan dan Pengolahan" → "Sample Handling"

5. **sample-proses-form.png**
   - Form Sample Proses (Testing Process) untuk proses pengujian sampel
   - Sudah ditambahkan di bagian "Penanganan Sampel" → "Fase 3: Pengujian" → "Melakukan Pengujian dan/atau Mencatat Hasil Pengujian"

6. **sample-autorize-form.png**
   - Form Sample Autorize (Testing Review) untuk review dan otorisasi hasil pengujian
   - Sudah ditambahkan di bagian "Penanganan Sampel" → "Fase 4: Verifikasi LHU" → "Sample Autorize"

7. **transfer-warehouse-form.png**
   - Form Transfer Warehouse untuk transfer persediaan antar warehouse
   - Sudah ditambahkan di bagian "Manajemen Persediaan" → "Memperbarui Data Persediaan"

8. **assembly-form.png**
   - Form Assembly untuk perakitan produk dari komponen berdasarkan BOM
   - Sudah ditambahkan di bagian "Manajemen Persediaan" → "Operasi Inventory Tambahan" → "Assembly"

9. **product-information-form.png**
   - Form Product Information untuk melihat dan mengelola informasi produk di inventory
   - Sudah ditambahkan di bagian "Manajemen Persediaan" → "Informasi Produk" → "Product Information"

10. **maintenance-request-form.png**
   - Form Maintenance Request untuk membuat permintaan pemeliharaan peralatan
   - Sudah ditambahkan di bagian "Manajemen Aset" → "Equipment Maintenance" → "Maintenance Request"

11. **maintenance-process-form.png**
   - Form Maintenance Process untuk mengeksekusi proses pemeliharaan peralatan
   - Sudah ditambahkan di bagian "Manajemen Aset" → "Equipment Maintenance" → "Maintenance Process"

12. **print-form-lhu.png**
   - Form Print Form LHU untuk mencetak dan melihat preview Laporan Hasil Uji (LHU)
   - Sudah ditambahkan di bagian "Penerbitan LHU" → "Form Laporan" → "Print Form LHU"

13. **laporan-air-baku.png**
   - Form Laporan Air Baku untuk membuat dan mencetak laporan pengujian kualitas air permukaan
   - Sudah ditambahkan di bagian "Penerbitan LHU" → "Laporan Air Baku" → "Laporan Air Baku"

14. **approval-ls-testing-order.png**
   - Form Approval LS untuk Testing Order (approval data testing order)
   - Sudah ditambahkan di bagian "Administrasi Sampel Uji" → "Fase 1: Pendaftaran dan Analisa Permintaan" → "Approval Testing Order"

15. **approval-dm-equipment.png**
   - Form Approval DM untuk Equipment (approval data master equipment)
   - Sudah ditambahkan di bagian "Manajemen Aset" → "Approval Data Master (Approval DM)" → "Approval DM untuk Equipment"

3. **testing-order-form-detail-price.png** (opsional)
   - Form Testing Order dengan section DETAIL PRICE
   - Bisa ditambahkan di bagian "Mengkalkulasi Biaya Pengujian"

## 🔧 Lokasi Tag img di HTML

Screenshot sudah ditambahkan di:
- **File**: `BUSINESS_PROCESS_MANUAL.html`
- **Lokasi**: Proses 2 - Administrasi Sampel Uji → Fase 1 → Langkah 4
- **Line**: Sekitar line 475-495

## 📝 Format Gambar yang Disarankan

- **Format**: PNG atau JPG
- **Ukuran**: Maksimal 1920px lebar (akan otomatis di-resize)
- **Nama file**: 
  - Gunakan lowercase
  - Gunakan dash (-) untuk spasi
  - Contoh: `testing-order-form.png`, `sample-handling-form.png`

## ✅ Checklist

- [ ] Buat folder `images/` di direktori yang sama dengan HTML
- [ ] Simpan screenshot dengan nama `testing-order-form.png`
- [ ] Pastikan path `images/testing-order-form.png` benar
- [ ] Test buka HTML di browser untuk memastikan gambar muncul
- [ ] Jika gambar tidak muncul, cek:
  - Path file benar
  - Nama file sesuai (case-sensitive di beberapa sistem)
  - File gambar tidak corrupt

## 🚀 Quick Start

```bash
# 1. Buat folder images
mkdir images

# 2. Copy screenshot ke folder images
# (Gunakan file manager atau command line)

# 3. Buka HTML di browser
open BUSINESS_PROCESS_MANUAL.html
# atau
# Buka dengan browser: file:///path/to/BUSINESS_PROCESS_MANUAL.html
```

## 💡 Tips

1. **Optimasi Gambar**: Gunakan tool seperti TinyPNG untuk mengurangi ukuran file
2. **Naming Convention**: Gunakan nama yang deskriptif dan konsisten
3. **Backup**: Simpan screenshot original sebelum di-optimize
4. **Version Control**: Jika menggunakan Git, pertimbangkan untuk menambahkan folder `images/` ke repository

## 🆘 Troubleshooting

### Gambar tidak muncul
- Cek path file (relatif terhadap lokasi HTML)
- Cek nama file (case-sensitive)
- Cek console browser untuk error (F12)

### Gambar terlalu besar
- Gunakan tool optimasi gambar
- Atau gunakan base64 untuk file kecil (< 100KB)

### Path tidak bekerja
- Gunakan path absolut: `/Users/sinergi/API/api-salims/images/testing-order-form.png`
- Atau gunakan base64 encoding

