# 🚀 Panduan Deploy ke Vercel

Panduan lengkap untuk mengupload dan deploy project ini ke Vercel.

## 📋 Prasyarat

1. Akun Vercel (gratis) - Daftar di [vercel.com](https://vercel.com)
2. Project sudah di GitHub (opsional, tapi direkomendasikan)
3. Node.js terinstall (untuk Vercel CLI)

## 🎯 Metode 1: Deploy via Vercel CLI (Paling Mudah)

### Langkah 1: Install Vercel CLI

```bash
npm install -g vercel
```

### Langkah 2: Login ke Vercel

```bash
vercel login
```

Ikuti instruksi di terminal untuk login via browser.

### Langkah 3: Deploy Project

Dari folder project, jalankan:

```bash
cd /Users/sinergi/API/manual-book-web
vercel
```

Vercel akan menanyakan beberapa pertanyaan:
- **Set up and deploy?** → Tekan Enter (Yes)
- **Which scope?** → Pilih akun/team Anda
- **Link to existing project?** → Tekan Enter (No) untuk project baru
- **What's your project's name?** → Tekan Enter untuk menggunakan nama default atau ketik nama custom
- **In which directory is your code located?** → Tekan Enter (./)

### Langkah 4: Deploy ke Production

Setelah deploy pertama berhasil, deploy ke production:

```bash
vercel --prod
```

Project Anda akan langsung online di URL yang diberikan Vercel!

---

## 🌐 Metode 2: Deploy via GitHub Integration (Recommended)

### Langkah 1: Push ke GitHub

Pastikan project sudah di-push ke GitHub repository:

```bash
git add .
git commit -m "Prepare for Vercel deployment"
git push origin main
```

### Langkah 2: Import Project di Vercel Dashboard

1. Buka [vercel.com/dashboard](https://vercel.com/dashboard)
2. Klik tombol **"Add New..."** → **"Project"**
3. Pilih **"Import Git Repository"**
4. Pilih repository `abdicamp/manual-book-web` (atau repository Anda)
5. Klik **"Import"**

### Langkah 3: Konfigurasi Project

Di halaman konfigurasi:

- **Framework Preset**: Pilih **"Other"** atau **"Static Site"**
- **Root Directory**: Biarkan `./` (root directory)
- **Build Command**: Kosongkan (tidak perlu build)
- **Output Directory**: Kosongkan atau isi dengan `./`

### Langkah 4: Deploy

Klik tombol **"Deploy"** dan tunggu proses deploy selesai.

Vercel akan otomatis:
- ✅ Deploy project Anda
- ✅ Memberikan URL production (contoh: `manual-book-web.vercel.app`)
- ✅ Setup auto-deploy setiap kali ada push ke GitHub

---

## 📤 Metode 3: Deploy via Drag & Drop (Quick Test)

### Langkah 1: Siapkan Folder

Buat folder zip dari project (atau gunakan folder langsung):

```bash
cd /Users/sinergi/API/manual-book-web
zip -r manual-book-web.zip . -x "*.git*" -x "*.md" -x "node_modules/*"
```

### Langkah 2: Upload di Vercel Dashboard

1. Buka [vercel.com/dashboard](https://vercel.com/dashboard)
2. Klik **"Add New..."** → **"Project"**
3. Scroll ke bawah, cari bagian **"Deploy"**
4. Drag & drop folder project atau file zip ke area upload
5. Tunggu proses deploy selesai

**Catatan**: Metode ini tidak akan auto-deploy saat ada update. Gunakan untuk testing cepat saja.

---

## ⚙️ Konfigurasi Tambahan

### File `vercel.json`

File `vercel.json` sudah dibuat dengan konfigurasi:
- ✅ Routing untuk file HTML
- ✅ Homepage redirect ke `BUSINESS_PROCESS_MANUAL.html`
- ✅ Cache headers untuk optimasi

### Custom Domain

Setelah deploy, Anda bisa menambahkan custom domain:

1. Buka project di Vercel Dashboard
2. Klik tab **"Settings"** → **"Domains"**
3. Tambahkan domain Anda
4. Ikuti instruksi untuk setup DNS

---

## 🔄 Auto-Deploy Setup

Jika menggunakan GitHub integration, Vercel akan otomatis:
- ✅ Deploy setiap kali ada push ke branch `main`
- ✅ Membuat preview deployment untuk setiap Pull Request
- ✅ Memberikan URL preview untuk setiap commit

---

## 📁 Struktur File yang Di-deploy

Vercel akan deploy semua file di folder project:
- ✅ `BUSINESS_PROCESS_MANUAL.html` (file utama)
- ✅ Folder `diagrams/` (semua diagram)
- ✅ Folder `images/` (semua gambar)
- ✅ File konfigurasi `vercel.json`

**Catatan**: File `.md` (Markdown) tidak akan di-deploy karena tidak diperlukan untuk website.

---

## 🐛 Troubleshooting

### Problem: File gambar tidak muncul

**Solusi**: Pastikan path gambar di HTML menggunakan relative path:
```html
<!-- ✅ Benar -->
<img src="diagrams/process-1-pendaftaran-pelanggan.png">

<!-- ❌ Salah -->
<img src="/diagrams/process-1-pendaftaran-pelanggan.png">
```

### Problem: 404 Not Found

**Solusi**: Pastikan file `vercel.json` sudah ada dan konfigurasi routing benar.

### Problem: Build Error

**Solusi**: 
- Pastikan tidak ada build command yang salah
- Untuk static site, kosongkan build command
- Pastikan root directory benar (`./`)

---

## 📝 Checklist Sebelum Deploy

- [ ] File `vercel.json` sudah ada
- [ ] Semua path gambar di HTML menggunakan relative path
- [ ] Test file HTML di local browser
- [ ] Pastikan semua gambar ada di folder `diagrams/` dan `images/`
- [ ] Project sudah di-push ke GitHub (jika menggunakan GitHub integration)

---

## 🎉 Setelah Deploy

Setelah deploy berhasil, Anda akan mendapatkan:
- ✅ Production URL: `https://manual-book-web.vercel.app` (atau custom)
- ✅ Dashboard untuk monitoring
- ✅ Analytics (jika diaktifkan)
- ✅ Logs untuk debugging

---

## 📞 Bantuan

Jika ada masalah:
1. Cek [Vercel Documentation](https://vercel.com/docs)
2. Cek logs di Vercel Dashboard → Project → Deployments
3. Pastikan semua file sudah ter-upload dengan benar

---

**Selamat Deploy! 🚀**

