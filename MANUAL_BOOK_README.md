# Manual Book - Business Process SALIMS

## 📚 Deskripsi

Manual book ini berisi dokumentasi lengkap tentang proses bisnis dalam sistem SALIMS (Sistem Administrasi Laboratorium). Manual book tersedia dalam 2 format:

1. **BUSINESS_PROCESS_MANUAL.md** - Format Markdown (untuk GitHub, GitLab, atau dokumentasi berbasis Markdown)
2. **BUSINESS_PROCESS_MANUAL.html** - Format HTML (untuk website langsung)

## 📋 Isi Manual Book

Manual book mencakup:

1. **Overview Sistem** - Penjelasan umum tentang sistem SALIMS
2. **Business Process Overview** - Gambaran umum proses bisnis utama
3. **11 Proses Bisnis Detail**:
   - Pendaftaran Pelanggan
   - Administrasi Sampel Uji
   - Kaji Ulang Permintaan (KUP)
   - Verifikasi Pembayaran
   - Pengambilan Sampel
   - Pengolahan Sampel
   - Penanganan Sampel
   - Persiapan Pengujian
   - Penerbitan LHU
   - Manajemen Persediaan
   - Manajemen Aset
4. **Integrasi Data** - Penjelasan tentang integrasi antar proses dan sistem eksternal
5. **Role dan Tanggung Jawab** - Daftar role dan tanggung jawab masing-masing
6. **Glossary** - Daftar istilah penting

## 🖼️ Diagram

Manual book ini dirancang untuk menampilkan diagram BPMN yang telah disediakan. Di file HTML, terdapat placeholder untuk diagram yang dapat diganti dengan gambar diagram yang sebenarnya.

### Cara Menambahkan Diagram ke HTML:

1. Simpan gambar diagram dengan nama yang jelas, contoh:
   - `diagram-pendaftaran-pelanggan.png`
   - `diagram-administrasi-sampel-uji.png`
   - dll.

2. Ganti placeholder di HTML dengan tag `<img>`:

```html
<!-- Sebelum -->
<div class="diagram-placeholder">
    Diagram: Business Process Pendaftaran Pelanggan<br>
    <small>Gambar diagram akan ditampilkan di sini</small>
</div>

<!-- Sesudah -->
<div class="diagram-container">
    <img src="path/to/diagram-pendaftaran-pelanggan.png" 
         alt="Business Process Pendaftaran Pelanggan" 
         style="max-width: 100%; height: auto; border-radius: 8px;">
</div>
```

3. Atau gunakan base64 encoding untuk embed langsung:

```html
<img src="data:image/png;base64,iVBORw0KGgoAAAANS..." alt="Diagram">
```

## 🌐 Cara Menggunakan untuk Website

### Opsi 1: Menggunakan File HTML Langsung

1. Copy file `BUSINESS_PROCESS_MANUAL.html` ke folder public website Anda
2. Tambahkan diagram ke folder yang sesuai
3. Update path gambar di HTML
4. Akses melalui browser: `https://yourdomain.com/BUSINESS_PROCESS_MANUAL.html`

### Opsi 2: Integrasi ke CMS/Website Framework

#### Laravel:
```php
// Di routes/web.php
Route::get('/manual-book', function () {
    return view('manual-book');
});

// Di resources/views/manual-book.blade.php
// Copy isi dari BUSINESS_PROCESS_MANUAL.html
```

#### WordPress:
1. Install plugin untuk custom HTML page
2. Copy isi HTML ke page editor
3. Atau gunakan shortcode

#### Static Site (Jekyll, Hugo, dll):
1. Copy file HTML ke folder templates
2. Atau convert Markdown ke format yang sesuai

### Opsi 3: Menggunakan Markdown dengan Converter

1. Gunakan tool seperti:
   - [Marked](https://marked.js.org/) - JavaScript
   - [Pandoc](https://pandoc.org/) - Command line
   - [Markdown-it](https://github.com/markdown-it/markdown-it) - Node.js

2. Convert Markdown ke HTML:
```bash
pandoc BUSINESS_PROCESS_MANUAL.md -o output.html --standalone --css=style.css
```

## 🎨 Kustomisasi Styling

File HTML sudah include styling internal. Untuk kustomisasi:

1. **Ubah Warna Theme**: Edit CSS di bagian `<style>`:
```css
header {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    /* Ganti dengan warna yang diinginkan */
}
```

2. **Ubah Font**: Edit di bagian body:
```css
body {
    font-family: 'Your Font', sans-serif;
}
```

3. **Extract CSS ke File Terpisah**: 
   - Copy isi tag `<style>` ke file `manual-book.css`
   - Link di HTML: `<link rel="stylesheet" href="manual-book.css">`

## 📱 Responsive Design

File HTML sudah responsive dan akan menampilkan menu toggle di mobile. Untuk testing:

1. Buka di browser
2. Tekan F12 untuk Developer Tools
3. Toggle device toolbar
4. Test di berbagai ukuran layar

## 🔍 SEO Optimization

Untuk optimasi SEO, tambahkan meta tags di bagian `<head>`:

```html
<meta name="description" content="Manual Book Business Process SALIMS - Sistem Administrasi Laboratorium">
<meta name="keywords" content="SALIMS, Laboratorium, Business Process, Manual Book">
<meta property="og:title" content="Manual Book - Business Process SALIMS">
<meta property="og:description" content="Dokumentasi lengkap proses bisnis sistem SALIMS">
```

## 📝 Update Manual Book

Untuk update manual book:

1. Edit file Markdown (`BUSINESS_PROCESS_MANUAL.md`)
2. Update file HTML jika diperlukan
3. Update diagram jika ada perubahan proses
4. Update versi dokumen di bagian footer

## 🚀 Deployment

### GitHub Pages:
1. Push file HTML ke repository
2. Enable GitHub Pages di settings
3. Akses melalui: `https://username.github.io/repo/BUSINESS_PROCESS_MANUAL.html`

### Netlify/Vercel:
1. Upload folder yang berisi HTML dan gambar
2. Deploy otomatis
3. Akses melalui URL yang diberikan

### Server Traditional:
1. Upload file ke folder public_html atau www
2. Set permission yang sesuai
3. Akses melalui domain

## 📞 Support

Untuk pertanyaan atau dukungan:
- **Email**: my.orbitteam@gmail.com
- **Tim Development**: Tim SALIMS

## 📄 License

Dokumen ini dibuat untuk keperluan internal dan dokumentasi sistem SALIMS.

---

**Versi**: 1.0  
**Tanggal**: 2025  
**Status**: Production Ready

