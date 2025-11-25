# Manual Book - Business Process SALIMS
## Sistem Administrasi Laboratorium

---

## 📋 Daftar Isi

1. [Overview Sistem](#overview-sistem)
2. [Business Process Overview](#business-process-overview)
3. [Proses Bisnis Detail](#proses-bisnis-detail)
   - [1. Pendaftaran Pelanggan](#1-pendaftaran-pelanggan)
   - [2. Administrasi Sampel Uji](#2-administrasi-sampel-uji)
   - [3. Kaji Ulang Permintaan (KUP)](#3-kaji-ulang-permintaan-kup)
   - [4. Verifikasi Pembayaran](#4-verifikasi-pembayaran)
   - [5. Pengambilan Sampel](#5-pengambilan-sampel)
   - [6. Pengolahan Sampel](#6-pengolahan-sampel)
   - [7. Penanganan Sampel](#7-penanganan-sampel)
   - [8. Persiapan Pengujian](#8-persiapan-pengujian)
   - [9. Penerbitan LHU](#9-penerbitan-lhu)
   - [10. Manajemen Persediaan](#10-manajemen-persediaan)
   - [11. Manajemen Aset](#11-manajemen-aset)
   - [12. Proses Approval](#12-proses-approval)
4. [Integrasi Data](#integrasi-data)
5. [Role dan Tanggung Jawab](#role-dan-tanggung-jawab)
6. [Glossary](#glossary)

---

## Overview Sistem

SALIMS (Sistem Administrasi Laboratorium) adalah sistem terintegrasi yang mengelola seluruh proses bisnis laboratorium pengujian, mulai dari pendaftaran pelanggan hingga penerbitan Laporan Hasil Uji (LHU). Sistem ini dirancang untuk mengoptimalkan alur kerja, meningkatkan akurasi data, dan memastikan kepatuhan terhadap standar kualitas laboratorium.

### Fitur Utama:
- **Manajemen Pelanggan**: Pendaftaran dan manajemen data pelanggan
- **Administrasi Sampel**: Pengelolaan permintaan pengujian dan sampel
- **Manajemen Pengujian**: Proses pengujian dari persiapan hingga hasil
- **Manajemen Pembayaran**: Verifikasi dan konfirmasi pembayaran
- **Manajemen Persediaan**: Pengelolaan bahan uji dan persediaan
- **Manajemen Aset**: Pemeliharaan dan kalibrasi peralatan
- **Integrasi Data**: Integrasi dengan sistem eksternal (CIS)

---

## Business Process Overview

Sistem SALIMS terdiri dari 4 proses bisnis utama yang saling terintegrasi:

```
┌─────────────────────────┐
│ 1. Administrasi Sampel  │
│         Uji             │
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│ 2. Penanganan Sampel    │
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│ 3. Manajemen Persediaan │
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│ 4. Manajemen Aset       │
└─────────────────────────┘
```

**Diagram Business Process To Be:**
- **1. Administrasi Sampel Uji** ↔ **2. Penanganan Sampel**: Penyerahan Sampel Uji & Penyerahan Hasil Uji
- **2. Penanganan Sampel** ↔ **3. Manajemen Persediaan**: Penggunaan Bahan Uji & Penyerahan Bahan Uji
- **2. Penanganan Sampel** ↔ **4. Manajemen Aset**: Penggunaan Peralatan Uji & Informasi Peralatan Uji
- **5. Integrasi Data**: Menerima data dari semua proses bisnis utama

---

## Proses Bisnis Detail

### 1. Pendaftaran Pelanggan

**Deskripsi**: Proses pendaftaran pelanggan baru melalui portal pelanggan dengan verifikasi data oleh admin.

**Diagram**: Business Process Pendaftaran Pelanggan

**Role yang Terlibat**:
- **Pelanggan**: Melakukan pendaftaran dan mengisi data
- **Admin**: Verifikasi data pendaftaran

**Alur Proses**:

1. **Mulai** → Pelanggan memulai proses pendaftaran
2. **Melakukan Pendaftaran Pelanggan Pada Portal Pelanggan**
   - Pelanggan mengakses portal dan memulai pendaftaran
3. **Mengisi Data Pelanggan**
   - Pelanggan mengisi formulir pendaftaran dengan data lengkap
4. **Akses Data** (Intermediate Event)
   - Data pendaftaran diakses oleh sistem untuk verifikasi
5. **Verifikasi Data Pendaftaran** (Admin)
   - Admin memverifikasi kelengkapan dan kebenaran data
6. **Decision: Data Lengkap?**
   - **Tidak**: Kembali ke langkah 3 (Mengisi Data Pelanggan)
   - **Ya**: Lanjut ke langkah 7
7. **Menerima Informasi Pendaftaran Disetujui**
   - Pelanggan menerima notifikasi persetujuan pendaftaran
8. **Selesai**

**Output**:
- Data pelanggan terdaftar dalam sistem
- Status pendaftaran: Disetujui

**Catatan Penting**:
- Data harus lengkap dan valid sebelum disetujui
- Pelanggan dapat memperbaiki data jika ditolak

---

### 2. Administrasi Sampel Uji

**Deskripsi**: Proses administrasi lengkap dari permintaan pengujian sampel hingga penerbitan LHU, melibatkan pelanggan, customer service admin, dan technical manager.

**Diagram**: Business Process Administrasi Sampel Uji

**Role yang Terlibat**:
- **Pelanggan**: Mengajukan permintaan, melakukan pembayaran, menerima hasil
- **Pelayanan Kepada Pelanggan Admin**: Menganalisa permintaan, mengelola pembayaran, menyiapkan dokumen
- **Manajer Teknis**: Melakukan KUP (Kaji Ulang Permintaan), menganalisa permintaan pengujian, membuat jadwal pengambilan sampel

**Alur Proses**:

#### Fase 1: Pendaftaran dan Analisa Permintaan

1. **Mulai** → Pelanggan memulai proses
2. **Melakukan Pendaftaran Pelanggan**
   - Jika belum terdaftar, pelanggan harus mendaftar terlebih dahulu
3. **Decision: Pelanggan Sudah Terdaftar?**
   - **Tidak**: Kembali ke langkah 2
   - **Ya**: Lanjut ke langkah 4
4. **Mengisi Form Permintaan Pengujian Sampel**
   - Pelanggan mengisi formulir permintaan pengujian
   - **Implementasi Sistem**: Form "Testing Order" di modul Sample Handling
     - **Request Details**: Request Number, Request Date, Periode, Customer, Request By, Description
     - **Section SAMPLE**: Menambahkan data sampel yang akan diuji
       - Sample No, Sample Name, Version, Service Type, Sample Category, Zona Name, Sub Zona Name, Is Acceleration, Subtotal Price
     - **Section QUALITY REFERENCE**: Menambahkan referensi kualitas untuk sampel
       - Quality Reference Name, Description
       - Digunakan sebagai standar acuan kualitas yang akan digunakan dalam evaluasi hasil pengujian
     - **Section PARAMETER**: Menambahkan parameter pengujian yang akan dilakukan
       - Parameter Name, Method ID, In Situ (pengujian di lokasi), Price
       - Menentukan jenis pengujian dan metode yang digunakan untuk setiap parameter
5. **Menganalisa Permintaan** (Admin)
   - Admin menganalisa kelayakan permintaan
6. **Approval Testing Order** - Lihat detail di [Proses 12: Proses Approval](#12-proses-approval)
7. **Kaji Ulang Permintaan (KUP)** (Manajer Teknis)
   - Technical manager melakukan review teknis
7. **Hasil KUP** (Message Event)
   - Hasil review dikirim kembali ke admin
8. **Decision: Dapat Dilakukan Pengujian?**
   - **Tidak**: Kembali ke "Mengisi Data Pelanggan"
   - **Ya**: Lanjut ke langkah 9
9. **Decision: Lanjutkan Proses Pengujian?**
   - **Tidak**: Konfirmasi Pembatalan Pengajuan → **Selesai**
   - **Ya**: Konfirmasi Persetujuan Pengujian → Lanjut ke Fase 2

#### Fase 2: Pembayaran

10. **Decision: Pelanggan Non MoU (Pra-Bayar)?**
    - **Ya**: 
      - **Mengkalkulasi Biaya Pengujian** (Admin)
        - **Implementasi Sistem**: Bagian "Additional Cost" dan "Detail Price" di form Testing Order
          - Additional Cost: Biaya tambahan (Expense Name, Expense Value, Description)
          - Detail Price: Kalkulasi harga (Gross, Discount %, DPP, VAT %, PPH %, NET)
      - **Menerbitkan Tagihan** (Admin)
      - Lanjut ke langkah 11
    - **Tidak**: Langsung ke langkah 11
11. **Melakukan Pembayaran** (Pelanggan)
    - Pelanggan melakukan pembayaran sesuai tagihan
12. **Verifikasi Pembayaran** (Admin)
    - Admin memverifikasi pembayaran
13. **Decision: Pembayaran Diterima?**
    - **Tidak**: Kembali ke langkah 11
    - **Ya**: Lanjut ke Fase 3

#### Fase 3: Pengambilan Sampel dan Dokumen

14. **Menyiapkan Dokumen Pengajuan** (Admin)
    - Admin menyiapkan dokumen yang diperlukan
15. **Decision: Sampel Dibawa Pelanggan?**
    - **Ya**: 
      - **Mengirim Bukti Penerimaan Pengajuan** (Pelanggan)
      - **Menerima Bukti Penerimaan Pengajuan** (Pelanggan)
      - Lanjut ke Fase 4
    - **Tidak**: 
      - **Menganalisa Permintaan Pengujian** (Manajer Teknis)
      - **Membuat Jadwal Pengambilan Sampel** (Manajer Teknis)
      - **SPK Pengambilan Sampel** (Message Event)
      - Lanjut ke Fase 4

#### Fase 4: Proses Pengujian dan LHU

16. **Proses Pengujian Selesai** (Message Event)
    - Notifikasi bahwa proses pengujian telah selesai
17. **Memberikan LHU** (Admin)
    - Admin memberikan Laporan Hasil Uji kepada pelanggan
18. **Selesai**

**Output**:
- Permintaan pengujian terdaftar
- Tagihan (jika diperlukan)
- Bukti pembayaran
- Bukti penerimaan pengajuan
- LHU (Laporan Hasil Uji)

**Catatan Penting**:
- Proses KUP menentukan kelayakan pengujian
- Pembayaran harus diverifikasi sebelum proses lanjutan
- SPK diperlukan jika sampel tidak dibawa pelanggan

---

### 3. Kaji Ulang Permintaan (KUP)

**Deskripsi**: Proses review teknis untuk menentukan kelayakan permintaan pengujian berdasarkan ketersediaan peralatan, bahan uji, analis, dan metode uji.

**Diagram**: Business Process Kaji Ulang Permintaan (KUP)

**Role yang Terlibat**:
- **Manager Teknis**: Menganalisa ketersediaan peralatan dan bahan uji
- **Analis**: Menganalisa ketersediaan analis dan metode uji

**Alur Proses**:

1. **Mulai** → Trigger dari proses Administrasi Sampel Uji
2. **Menganalisa Permintaan Pengujian** (Manager Teknis)
   - Manager teknis menganalisa kebutuhan pengujian
3. **Parallel Gateway (Split)** → Tiga proses paralel dimulai:
   
   **Path 1: Ketersediaan Peralatan**
   - **Menganalisa Ketersediaan Peralatan** (Manager Teknis)
   - **Decision: Kadaluarsa?**
     - **Ya/Tidak**: Keduanya menuju ke Parallel Join
   
   **Path 2: Ketersediaan Bahan Uji**
   - **Menganalisa Ketersediaan Bahan Uji** (Manager Teknis)
   - Menuju ke "Disposal Bahan Uji" atau langsung ke Parallel Join
   
   **Path 3: Ketersediaan Analis dan Metode Uji**
   - **Menganalisa Ketersediaan Analis dan Metode Uji** (Analis)
   - **Decision: Tersedianya Analis?**
     - **Tidak**: Langsung ke Parallel Join
     - **Ya**: 
       - **Decision: Bisa Melakukan Pengujian?**
         - **Tidak**: Langsung ke Parallel Join
         - **Ya**: 
           - **Mengkonfirmasi Ketersediaan** (Analis)
           - Menuju ke "Disposal Bahan Uji"

4. **Disposal Bahan Uji** (Analis)
   - Jika diperlukan, dilakukan disposal bahan uji
5. **Parallel Gateway (Join)**
   - Semua path paralel bergabung
6. **Hasil KUP** (Message Event)
   - Hasil review dikirim kembali ke proses Administrasi Sampel Uji
7. **Selesai**

**Output**:
- Hasil KUP (Kaji Ulang Permintaan)
- Status ketersediaan: Dapat/Tidak Dapat Dilakukan Pengujian

**Kriteria Penilaian**:
- Ketersediaan peralatan (termasuk status kadaluarsa)
- Ketersediaan bahan uji
- Ketersediaan analis yang kompeten
- Ketersediaan metode uji yang sesuai

---

### 4. Verifikasi Pembayaran

**Deskripsi**: Proses verifikasi pembayaran pelanggan dengan integrasi ke sistem CIS (Customer Information System) untuk mendapatkan data pembayaran.

**Diagram**: Business Process Verifikasi Pembayaran

**Role yang Terlibat**:
- **Admin**: Melakukan verifikasi pembayaran
- **Data Integration (API CIS)**: Menyediakan data pembayaran

**Alur Proses**:

1. **Mulai** → Admin memulai proses verifikasi
2. **Menkonfirmasi Pembayaran Atas Nomor Permohonan Pengujian**
   - Admin mengkonfirmasi pembayaran berdasarkan nomor permohonan
3. **Melakukan Pencarian Data Pembayaran**
   - Admin mencari data pembayaran di sistem
4. **Decision: Terhubung dengan CIS?**
   - **Tidak**: Kembali ke langkah 3 (retry)
   - **Ya**: Lanjut ke langkah 5
5. **Menerima Data Pembayaran** (dari API CIS)
   - Sistem menerima data pembayaran dari API CIS
   - Data integration: API CIS → Admin
6. **Selesai**

**Output**:
- Data pembayaran terverifikasi
- Status pembayaran: Diterima/Belum Diterima

**Catatan Penting**:
- Sistem harus terhubung dengan CIS untuk mendapatkan data pembayaran
- Jika koneksi gagal, proses akan retry

---

### 5. Pengambilan Sampel

**Deskripsi**: Proses pengambilan sampel di lapangan, termasuk persiapan peralatan, kalibrasi, pencetakan barcode, dan pengujian in-situ jika diperlukan.

**Diagram**: Business Process Pengambilan Sampel

**Role yang Terlibat**:
- **Pengambilan Sampel (PPS)**: Tim yang melakukan pengambilan sampel
- **Admin Persediaan**: Mengkonfirmasi penggunaan peralatan dan bahan uji

**Alur Proses**:

1. **Skedul Pengambilan Sampel** (Timer Start Event)
   - Proses dimulai berdasarkan jadwal yang telah ditentukan
2. **Planning Taking Sample (Perencanaan Pengambilan Sampel)**
   - **Implementasi Sistem**: Form "Planning Taking Sample" di modul Sample Handling
     - **Planning Details**: Planning Taking Sample Number, Request Number (dari Testing Order), PTS Date, Periode, Description
     - **Section SAMPLE**: Data sampel yang akan diambil dengan status:
       - Equipment Sample Status - Status ketersediaan peralatan untuk sampel
       - Equipment Parameter Status - Status ketersediaan peralatan untuk parameter
       - Labour Status - Status ketersediaan tenaga kerja
       - Product Status - Status ketersediaan produk/bahan
     - **Section EQUIPMENT**: Daftar peralatan yang akan digunakan (Equipment Name, Equipment Version, Due Date Calibration, Hold Duration)
     - **Section LABOUR**: Daftar tenaga kerja yang akan ditugaskan (Labour Name, Hold Duration)
     - **Section PARAMETER**: Parameter pengujian yang akan dilakukan (Parameter Name, Standard Duration)
   - Form ini digunakan untuk merencanakan pengambilan sampel dengan menentukan peralatan, tenaga kerja, dan parameter yang diperlukan
3. **Mengecek Permintaan Pengambilan Sampel Uji**
   - Tim memeriksa detail permintaan pengambilan sampel
3. **Parallel Gateway (Split)** → Dua persiapan paralel:
   
   **Path 1: Persiapan Peralatan**
   - **Melakukan Persiapan Peralatan Uji**
   
   **Path 2: Persiapan Bahan Uji**
   - **Melakukan Persiapan Bahan Uji**

4. **Parallel Gateway (Join)**
   - Kedua persiapan selesai
5. **Mengkonfirmasi Penggunaan Peralatan dan Bahan Uji** (Admin Persediaan)
   - Admin memastikan peralatan dan bahan tersedia dan siap digunakan
6. **Decision: Perlu Dikalibrasi?**
   - **Ya**: 
     - **Melakukan Kalibrasi**
     - Lanjut ke langkah 7
   - **Tidak**: Langsung ke langkah 7
7. **Melakukan Print Barcode Permintaan Pengujian Berdasarkan Parameter**
   - Mencetak barcode untuk identifikasi sampel
8. **Sub-process: Pengambilan Sampel Dilapangan** (Ad-hoc)
   
   a. **Melakukan Pengambilan Sampel**
      - Tim mengambil sampel di lokasi
      - **Implementasi Sistem**: Form "Taking Sample" di modul Sample Handling
        - **Taking Sample Details**: Taking Sample Number, Periode, Taking Sample Date, Planning Taking Sample Number (relasi dengan Planning Taking Sample), Sample Code, Sample No
        - **Lokasi dan Kondisi**: Geo Tag (koordinat GPS), Address, Weather, Wind Direction, Temperatur
        - **Personnel**: Sampling By - Nama personel yang melakukan pengambilan
        - **Additional Data**: Description, Parameter pengujian, Foto sampel (upload)
      - Form ini digunakan untuk mencatat data pengambilan sampel aktual di lapangan, termasuk lokasi (GPS), kondisi cuaca, dan informasi lain yang diperlukan untuk traceability
   
   b. **Decision: Permintaan Pengujian In-situ?**
      - **Ya**: 
        - **Melakukan Pengujian In-situ**
        - Lanjut ke langkah c
      - **Tidak**: Langsung ke langkah c
   
   c. **Mencatat Informasi Sampel Sesuai dengan Label**
      - Mencatat semua informasi sampel sesuai dengan barcode/label

9. **Membawa Sampel Ke Laboratorium**
   - Sampel dibawa ke laboratorium untuk proses selanjutnya
10. **Selesai**

**Output**:
- Sampel yang telah diambil dan dilabeli
- Data pengambilan sampel
- Hasil pengujian in-situ (jika ada)
- Barcode untuk tracking

**Catatan Penting**:
- Kalibrasi wajib dilakukan jika diperlukan
- Pengujian in-situ bersifat opsional
- Semua informasi sampel harus tercatat dengan lengkap

---

### 6. Pengolahan Sampel

**Deskripsi**: Proses pengolahan sampel setelah diterima di laboratorium, termasuk pembagian sampel, penambahan bahan, pendinginan, dan penyimpanan.

**Diagram**: Business Process Pengolahan Sampel

**Role yang Terlibat**:
- **Admin**: Melakukan pengolahan sampel

**Alur Proses**:

1. **Mulai** → Sampel diterima di laboratorium
2. **Menganalisa Permohonan Pengujian**
   - Admin menganalisa kebutuhan pengujian dari permohonan
3. **Membagi Sampel Berdasarkan Parameter Uji**
   - Sampel dibagi sesuai dengan parameter yang akan diuji
4. **Parallel Gateway (Split)** → Tiga proses paralel:
   
   **Path 1: Penambahan Bahan**
   - **Menambahkan Bahan**
   
   **Path 2: Pendinginan Sampel**
   - **Mendinginkan Sampel**
   
   **Path 3: Penyimpanan Sampel**
   - **Menyimpan Sampel**

5. **Parallel Gateway (Join)**
   - Semua proses pengolahan selesai
6. **Pengolahan Sample** (Message End Event)
   - Notifikasi bahwa pengolahan sampel selesai
7. **Selesai**

**Output**:
- Sampel yang telah diolah dan siap untuk pengujian
- Sampel yang telah dibagi sesuai parameter
- Sampel yang telah disimpan dengan kondisi yang tepat

**Catatan Penting**:
- Pembagian sampel harus sesuai dengan parameter uji
- Kondisi penyimpanan harus sesuai dengan standar
- Semua proses pengolahan harus selesai sebelum lanjut ke proses pengujian

---

### 7. Penanganan Sampel

**Deskripsi**: Proses penanganan sampel dari penerimaan hingga verifikasi LHU, melibatkan multiple role dengan quality control di setiap tahap.

**Diagram**: Business Process Penanganan Sampel

**Role yang Terlibat**:
- **PPS**: Pengambilan sampel
- **Manager Teknis**: Menerima sampel, verifikasi LHU
- **Penyelia (Supervisor)**: Konfirmasi pengolahan dan hasil uji
- **Analis**: Persiapan dan pelaksanaan pengujian
- **Admin**: Pengolahan sampel dan penerimaan LHU

**Alur Proses**:

#### Fase 1: Penerimaan dan Pengolahan

1. **Jadwal Pengambilan Sampel** (Timer Start Event)
   - Proses dimulai berdasarkan jadwal
2. **Pengambilan Sampel** (Sub-process)
   - PPS melakukan pengambilan sampel
3. **Contoh Uji Diterima** (Message Catching Event)
   - Notifikasi sampel telah diterima
4. **Menerima Contoh Uji (Disposisi Teknis)** (Manager Teknis)
   - Manager teknis menerima dan melakukan disposisi teknis
5. **Pengolahan Sampel** (Sub-process, Admin)
   - Admin melakukan pengolahan sampel
6. **Sample Handling (Penanganan Sampel)**
   - **Implementasi Sistem**: Form "Sample Handling" di modul Sample Handling
     - **Sample Handling Details**: SS Number (Sample Handling Number), SS Date, Period, SR Number (Sample Registration Number - relasi dengan Sample Registration), Sample Code, Sample No, Sample Version, Labour Code, Description
     - **Section DETAILS**: Detail pengujian yang akan dilakukan (Test ID, Unit Code, Quantity, Description, Parameter Code)
   - Form ini digunakan untuk mencatat penanganan sampel setelah diterima di laboratorium, termasuk detail pengujian yang akan dilakukan untuk setiap parameter
7. **Penanganan Sampel** (Message Throwing Event)
   - Notifikasi pengolahan selesai

#### Fase 2: Konfirmasi Pengolahan

8. **Penanganan Sampel** (Message Catching Event, Penyelia)
   - Penyelia menerima notifikasi
9. **Mengkonfirmasi Pengolahan Sampel** (Penyelia)
   - Penyelia memverifikasi hasil pengolahan
10. **Decision: Memenuhi Syarat?**
    - **Tidak**: 
      - **Hasil Pengujian External Diterima** (Message Event)
      - Langsung ke Persiapan Pengujian (Path External)
    - **Ya**: 
      - **Inclusive Gateway**: 
        - **Path "Segera"**: Langsung ke Persiapan Pengujian
        - **Path "Menunggu Jadwal"**: Timer Event → Persiapan Pengujian

#### Fase 3: Pengujian

11. **Persiapan Pengujian** (Sub-process, Analis)
    - Analis mempersiapkan pengujian
12. **Melakukan Pengujian dan/atau Mencatat Hasil Pengujian** (Analis)
    - Analis melakukan pengujian dan mencatat hasil
    - **Implementasi Sistem**: Form "Sample Proses" (Testing Process) di modul Sample Handling
      - **Process Details**: Branch Code, Period, Process Date, SR Number (Sample Registration Number), SS Number (Sample Handling Number), Test ID, Execute Date, Duration, Metspec (spesifikasi metode), Description
      - **Section PRODUCTS**: Produk/bahan yang digunakan dalam pengujian (Product Code, Version, Unit Code, Batch No, Warehouse Code, Location Code, Product Qty, Product Qty Use, Exp Date)
      - **Section LABOUR**: Tenaga kerja yang terlibat (Labour Code, Hold Duration)
      - **Section FORMULAS**: Formula pengujian (Formula Code, Version, Formula Result, L Spec, U Spec, Parameter, Parameter Result)
      - **Section EQUIPMENT**: Peralatan yang digunakan (Equipment Code, Version, Due Date Calibration, Hold Duration)
    - Form ini digunakan untuk mencatat proses pengujian sampel, termasuk produk yang digunakan, tenaga kerja, formula pengujian, dan peralatan yang diperlukan
13. **Mengkonfirmasi Hasil Uji** (Penyelia)
    - Penyelia memverifikasi hasil pengujian
14. **Decision: Memenuhi Syarat?**
    - **Tidak**: Kembali ke langkah 12 (re-test)
    - **Ya**: Lanjut ke langkah 15

#### Fase 4: Verifikasi LHU

15. **Sample Autorize (Otorisasi Sampel / Testing Review)**
    - **Implementasi Sistem**: Form "Sample Autorize" (Testing Review) di modul Sample Handling
      - **Review Details**: Branch Code, Review Date, Period, SR Number (Sample Registration Number), Product Code, Description
      - **Section Review Details**: Detail review untuk setiap proses pengujian (Process Number dari Sample Proses, Description, Is Taken - status apakah hasil sudah diambil/disetujui)
    - Form ini digunakan untuk melakukan review dan otorisasi hasil pengujian sebelum LHU diterbitkan. Setiap proses pengujian direview dan disetujui sebelum lanjut ke verifikasi LHU.
16. **Verifikasi LHU** (Manager Teknis)
    - Manager teknis memverifikasi LHU
17. **Decision: Memenuhi Syarat?**
    - **Tidak**: Kembali ke langkah 12 (re-test)
    - **Ya**: 
      - **LHU** (Message Throwing Event)
      - Lanjut ke langkah 18
18. **Menerima LHU** (Admin)
    - Admin menerima LHU yang telah diverifikasi
19. **Selesai** (Terminate End Event)

**Output**:
- Sampel yang telah diolah
- Hasil pengujian
- LHU yang telah diverifikasi

**Quality Control Points**:
1. Konfirmasi Pengolahan Sampel (Penyelia)
2. Konfirmasi Hasil Uji (Penyelia)
3. Verifikasi LHU (Manager Teknis)

**Catatan Penting**:
- Setiap tahap memiliki quality control
- Jika tidak memenuhi syarat, proses dapat diulang
- Pengujian external dapat digunakan jika diperlukan

---

### 8. Persiapan Pengujian

**Deskripsi**: Proses persiapan sebelum pengujian dimulai, termasuk persiapan peralatan, bahan uji, konfirmasi penggunaan, dan kalibrasi jika diperlukan.

**Diagram**: Business Process Persiapan Pengujian

**Role yang Terlibat**:
- **Analis**: Melakukan persiapan peralatan, bahan uji, dan kalibrasi
- **Admin Persediaan**: Mengkonfirmasi penggunaan peralatan dan bahan uji

**Alur Proses**:

1. **Skedul Pengambilan Sampel** (Timer Start Event)
   - Proses dimulai berdasarkan jadwal
2. **Mengecek Permintaan Pengambilan Sampel Uji**
   - Analis memeriksa detail permintaan
3. **Parallel Gateway (Split)** → Dua persiapan paralel:
   
   **Path 1: Persiapan Peralatan**
   - **Melakukan Persiapan Peralatan Uji**
   
   **Path 2: Persiapan Bahan Uji**
   - **Melakukan Persiapan Bahan Uji**

4. **Parallel Gateway (Join)**
   - Kedua persiapan selesai
5. **Mengkonfirmasi Penggunaan Peralatan dan Bahan Uji** (Admin Persediaan)
   - Admin memastikan peralatan dan bahan tersedia
6. **Decision: Perlu Dikalibrasi?**
   - **Ya**: 
     - **Melakukan Kalibrasi**
     - Lanjut ke Selesai
   - **Tidak**: Langsung ke Selesai

**Output**:
- Peralatan siap digunakan
- Bahan uji siap digunakan
- Peralatan terkalibrasi (jika diperlukan)

**Catatan Penting**:
- Kalibrasi wajib dilakukan jika diperlukan
- Konfirmasi dari Admin Persediaan diperlukan sebelum pengujian

---

### 9. Penerbitan LHU

**Deskripsi**: Proses penerbitan LHU (Laporan Hasil Uji) yang melibatkan verifikasi pembayaran, kalkulasi biaya (jika diperlukan), penerbitan tagihan, konfirmasi pembayaran, dan pengiriman LHU kepada pelanggan.

**Diagram**: Business Process Penerbitan LHU

**Role yang Terlibat**:
- **Admin**: Mengecek pembayaran, mengkalkulasi biaya, menerbitkan tagihan, mengkonfirmasi pembayaran, memberikan LHU hard copy
- **Pelanggan**: Mengakses portal, mengecek status, melakukan pembayaran, mengisi feedback, mengunduh LHU soft copy
- **Data Integration (API CIS)**: Menyediakan data pembayaran

**Alur Proses**:

#### Path Admin:

1. **Mulai** → Admin memulai proses
2. **Melakukan Pengecekan Data Pembayaran**
   - Admin mengecek status pembayaran
3. **Decision: Pelanggan MoU (Pasca-Bayar) dan Ditemukan Biaya?**
   - **Ya**: 
     - **Mengkalkulasi Biaya Pengujian**
     - Lanjut ke langkah 4
   - **Tidak**: Langsung ke langkah 4
4. **Menerbitkan Tagihan**
   - Admin menerbitkan tagihan (Message → Pelanggan)
5. **Menkonfirmasi Pembayaran Atas Nomor Permohonan Pengujian**
   - Admin mengkonfirmasi pembayaran (Trigger dari Pelanggan)
6. **Melakukan Pencarian Data Pembayaran**
   - Admin mencari data pembayaran
7. **Decision: Data Ditemukan?**
   - **Tidak**: Kembali ke langkah 5
   - **Ya**: Lanjut ke langkah 8
8. **Menerima Data Pembayaran** (dari API CIS)
   - Sistem menerima data dari API CIS
9. **Decision: Data Feedback Ditemukan?**
   - **Tidak**: 
     - **Mengisi Feedback**
     - Lanjut ke langkah 10
   - **Ya**: Langsung ke langkah 10
10. **Menerima LHU (Hard Copy)**
    - Admin menerima LHU hard copy
11. **Selesai**

#### Path Pelanggan:

1. **Mulai** → Pelanggan memulai proses
2. **Mengakses Portal Pelanggan**
   - Pelanggan login ke portal
3. **Decision: Status Pengujian Selesai?**
   - **Tidak**: Kembali ke langkah 2
   - **Ya**: Lanjut ke langkah 4
4. **Pengecekan Data Pembayaran**
   - Pelanggan mengecek status pembayaran
5. **Decision: Data Pembayaran Ditemukan?**
   - **Tidak**: 
     - **Melakukan Pembayaran** (Message → Admin)
     - Kembali ke langkah 4
   - **Ya**: Lanjut ke langkah 6
6. **Decision: Data Feedback Ditemukan?**
   - **Tidak**: 
     - **Mengisi Feedback**
     - Lanjut ke langkah 7
   - **Ya**: Langsung ke langkah 7
7. **Mengunduh LHU (Soft Copy)**
   - Pelanggan mengunduh LHU dari portal
8. **Selesai**

**Output**:
- Tagihan (jika diperlukan)
- Konfirmasi pembayaran
- LHU Hard Copy (untuk Admin)
- LHU Soft Copy (untuk Pelanggan)
- Feedback (jika diisi)

**Print Form LHU (Laporan Hasil Uji)**
- **Implementasi Sistem**: Form "Print Form LHU" di modul LAPORAN
  - **Fungsi**: Form ini digunakan untuk mencetak dan melihat preview Laporan Hasil Uji (LHU), termasuk:
    - Nomor Laporan - Nomor laporan hasil uji
    - Judul Pengujian - Judul atau jenis pengujian yang dilakukan
    - Informasi Laboratorium - Logo, nama, alamat, dan kontak laboratorium
    - Informasi Pelanggan - Nama dan alamat pelanggan
    - Informasi Sampel - Kode contoh uji, metode pengambilan, tanggal pengambilan
    - Informasi Analisa - Tempat analisa, tanggal analisa
    - Tabel Hasil Pengujian - Parameter, satuan, standar maksimal, hasil, limit deteksi, metode analisa, keterangan
  - Form ini menghasilkan LHU yang berisi informasi lengkap tentang hasil pengujian sampel, termasuk semua parameter yang diuji beserta hasilnya. LHU ini dapat dicetak sebagai hard copy atau diunduh sebagai soft copy.

**Laporan Air Baku (Raw Water Report)**
- **Implementasi Sistem**: Form "Laporan Air Baku" di modul LAPORAN
  - **Fungsi**: Form ini digunakan untuk membuat dan mencetak laporan pengujian kualitas air permukaan, termasuk:
    - Filter Customer - Filter berdasarkan pelanggan
    - Range Tanggal - Filter berdasarkan tanggal mulai dan tanggal akhir
    - Informasi Laporan - Nomor laporan, judul pengujian (contoh: "Pengujian kualitas air permukaan IPAM Ngagel")
    - Informasi Pelanggan - Nama dan alamat pelanggan
    - Informasi Sampel - Kode contoh uji, metode pengambilan, tanggal pengambilan
    - Informasi Analisa - Tempat analisa, tanggal analisa
    - Tabel Hasil Pengujian - Parameter (TDS, Kesadahan, Magnesium, Chlorida, dll), satuan, standar maksimal, hasil, limit deteksi, metode analisa, keterangan
  - Form ini khusus digunakan untuk laporan pengujian kualitas air permukaan yang dilakukan secara berkala (bulanan). Laporan ini membantu dalam monitoring kualitas air baku di IPAM (Instalasi Pengolahan Air Minum).

**Catatan Penting**:
- Pelanggan MoU (Pasca-Bayar) akan dikenakan biaya setelah pengujian
- Feedback dapat diisi oleh Admin atau Pelanggan
- LHU tersedia dalam format hard copy dan soft copy

---

### 10. Manajemen Persediaan

**Deskripsi**: Proses manajemen persediaan bahan uji, termasuk stock opname, monitoring batas minimum, rekonsiliasi, dan disposal bahan kadaluarsa.

**Diagram**: Business Process Manajemen Persediaan

**Role yang Terlibat**:
- **Admin Persediaan**: Melakukan stock opname, monitoring, rekonsiliasi, update data
- **Penyelia (Supervisor)**: Mengkonfirmasi hasil rekonsiliasi

**Alur Proses**:

1. **Mulai** → Admin memulai proses
2. **Membuat Daftar Persediaan**
   - Admin membuat daftar persediaan yang ada
3. **Periode StockOpname** (Timer Event)
   - Menunggu periode stock opname
4. **Parallel Gateway (Split)** → Dua proses paralel:

   **Path 1: Stock Opname**
   - **Melakukan Stok Opname**
   - **Decision: Terdapat Perbedaan Data?**
     - **Tidak**: Langsung ke **Selesai**
     - **Ya**: Menuju ke Parallel Join
   
   **Path 2: Cek Minimum Inventory**
   - **Mengecek Batas Minimum Persediaan**
   - **Decision: Terdapat Persediaan yang Mencapai Batas Bawah?**
     - **Tidak**: Langsung ke **Selesai**
     - **Ya**: Menuju ke Parallel Join

5. **Parallel Gateway (Join)**
   - Bergabung jika ada perbedaan data ATAU persediaan mencapai batas bawah
6. **Melakukan Rekap**
   - Admin melakukan rekonsiliasi data
7. **Mengkonfirmasi Hasil Recap** (Penyelia)
   - Supervisor mengkonfirmasi hasil rekonsiliasi
8. **Memperbarui Data Persediaan**
   - Admin memperbarui data persediaan
   - **Implementasi Sistem**: Form "Transfer Warehouse" di modul Inventory
     - **Transfer Details**: Transaction Index, AD Number (Adjustment Number), AD Date, AD Type, Branch Code, Period, Warehouse Code (warehouse sumber), Location Code (lokasi sumber), Reference Number, Description, User
     - Form ini digunakan untuk melakukan transfer persediaan dari satu warehouse ke warehouse lain, termasuk update data persediaan di kedua warehouse (sumber dan tujuan)
9. **Decision: Kadaluarsa?**
   - **Tidak**: Langsung ke **Selesai**
   - **Ya**: 
     - **Disposal Bahan Uji**
     - Lanjut ke **Selesai**

**Operasi Inventory Tambahan:**

**Assembly (Perakitan Produk)**
- **Implementasi Sistem**: Form "Assembly" di modul Inventory
  - **Assembly Details**: Branch Code, Transaction Index, User Created, Assembly Number, Period, Assembly Date, Product Code (produk hasil perakitan), BOM Code (Bill of Materials), Assembly By, Quantity, Expiry Date, Destination Warehouse Code, Destination Location Code, Unit Code, Description
  - **Section ASSEMBLY DETAIL**: Detail komponen yang digunakan dalam perakitan (Product Version, Warehouse Code, Location Code, Product Code, Batch No, Unit Code, Unit Code Use, Product Qty)
- Form ini digunakan untuk melakukan perakitan produk dari komponen-komponen berdasarkan BOM (Bill of Materials), termasuk update persediaan komponen dan produk hasil perakitan

**Product Information (Informasi Produk)**
- **Implementasi Sistem**: Form "Product Information" di modul Inventory
  - **Fungsi**: Form ini digunakan untuk melihat dan mengelola informasi produk di inventory, termasuk:
    - Product Code, Product Name, Product Version
    - Product Type, Product Category
    - Warehouse Code, Location Code - Lokasi penyimpanan
    - Unit Code - Satuan produk
    - Batch No - Nomor batch
    - Product Qty - Jumlah persediaan
    - Exp Date - Tanggal kadaluarsa
    - Min Stock - Batas minimum persediaan
    - Shelf Life - Masa simpan
    - Manufacture Code - Kode pabrikan
    - Building Code - Kode gedung
    - Description - Deskripsi produk
  - Form ini membantu dalam monitoring dan tracking informasi produk di inventory, termasuk status persediaan, lokasi, dan informasi penting lainnya

**Output**:
- Daftar persediaan terbaru
- Hasil stock opname
- Data rekonsiliasi
- Data persediaan yang diperbarui
- Bahan kadaluarsa yang telah didisposal
- Produk hasil perakitan (Assembly)

**Catatan Penting**:
- Stock opname dilakukan secara berkala
- Monitoring batas minimum dilakukan secara kontinyu
- Bahan kadaluarsa harus segera didisposal

---

### 11. Manajemen Aset

**Deskripsi**: Proses manajemen aset peralatan laboratorium, termasuk pemeliharaan rutin dan kalibrasi peralatan.

**Diagram**: Business Process Manajemen Aset

**Role yang Terlibat**:
- **Analis**: Membuat daftar peralatan, jadwal pemeliharaan, melakukan pemeriksaan dan pemeliharaan, membuat laporan kerusakan, membuat riwayat peralatan
- **Manajemen Aset Supervisor**: Membuat program kalibrasi, mengajukan permintaan kalibrasi, melakukan pemutakhiran data peralatan
- **Manajer Lab**: Mengkonfirmasi permintaan kalibrasi
- **Internal/External Kalibrasi**: Melakukan kalibrasi peralatan

**Alur Proses**:

#### Process 1: Equipment Maintenance

1. **Mulai** → Analis memulai proses
2. **Membuat Daftar Peralatan**
   - Analis membuat daftar semua peralatan
3. **Membuat Jadwal Pemeliharaan**
   - Analis membuat jadwal pemeliharaan rutin
4. **Jadwal Pemeriksaan dan Pemeliharaan** (Data Store)
   - Jadwal disimpan dalam sistem
5. **Melakukan Pemeriksaan dan Pemeliharaan**
   - Analis melakukan pemeriksaan dan pemeliharaan sesuai jadwal
6. **Decision: Alat Rusak?**
   - **Ya**: 
     - **Membuat Laporan Kerusakan**
     - **Update Status Peralatan**
     - **Selesai**
   - **Tidak**: 
     - **Membuat Riwayat Peralatan**
     - **Selesai**

**Maintenance Request (Permintaan Pemeliharaan)**
- **Implementasi Sistem**: Form "Maintenance Request" di modul Equipment Maintenance
  - **Fungsi**: Form ini digunakan untuk membuat permintaan pemeliharaan peralatan, termasuk:
    - MR Number - Nomor permintaan pemeliharaan (auto-generate atau manual)
    - Branch Code - Kode cabang
    - Period - Periode transaksi
    - MR Date - Tanggal permintaan pemeliharaan
    - Equipment Code - Kode peralatan yang akan dipelihara
    - Equipment Version - Versi peralatan
    - Description - Deskripsi permintaan pemeliharaan (alasan, detail kerusakan, dll)
    - User Created - User yang membuat permintaan
    - Transaction Status - Status transaksi
    - Approval Status - Status persetujuan
    - Is Auto No - Flag untuk auto-generate nomor
  - Form ini merupakan langkah awal dalam proses pemeliharaan peralatan. Setelah maintenance request dibuat, akan dilanjutkan ke proses maintenance process untuk eksekusi pemeliharaan.

**Maintenance Process (Proses Pemeliharaan)**
- **Implementasi Sistem**: Form "Maintenance Process" di modul Equipment Maintenance
  - **Fungsi**: Form ini digunakan untuk mengeksekusi proses pemeliharaan peralatan berdasarkan Maintenance Request yang telah dibuat, termasuk:
    - MP Number - Nomor proses pemeliharaan (auto-generate atau manual)
    - Branch Code - Kode cabang
    - Period - Periode transaksi
    - MP Date - Tanggal proses pemeliharaan
    - Maintenance Request - Referensi ke Maintenance Request yang akan diproses (MR Number)
    - Status - Status proses pemeliharaan (dalam proses, selesai, dll)
    - Description - Deskripsi proses pemeliharaan yang dilakukan (tindakan yang diambil, hasil pemeriksaan, dll)
    - User Created - User yang membuat proses pemeliharaan
    - Transaction Status - Status transaksi
    - Approval Status - Status persetujuan
    - Is Auto No - Flag untuk auto-generate nomor
  - Form ini merupakan langkah eksekusi dari Maintenance Request. Setelah maintenance request dibuat, maintenance process digunakan untuk mencatat dan mengeksekusi tindakan pemeliharaan yang dilakukan pada peralatan.

#### Process 2: Equipment Calibration

1. **Mulai** → Manajemen Aset Supervisor memulai proses
2. **Membuat Program Kalibrasi**
   - Supervisor membuat program kalibrasi
3. **Jadwal Kalibrasi** (Data Store)
   - Jadwal kalibrasi disimpan dalam sistem
4. **Mengajukan Permintaan Kalibrasi**
   - Supervisor mengajukan permintaan kalibrasi
5. **Mengkonfirmasi Permintaan Kalibrasi** (Manajer Lab)
   - Lab manager mengkonfirmasi permintaan
6. **Melakukan Kalibrasi** (Internal/External Kalibrasi)
   - Tim kalibrasi melakukan kalibrasi peralatan
7. **Laporan Kalibrasi** (Message Flow)
   - Laporan kalibrasi dibuat
8. **Melakukan Pemutakhiran Data Peralatan** (Manajemen Aset Supervisor)
   - Supervisor memperbarui data peralatan berdasarkan laporan kalibrasi
9. **Selesai**

**Output**:
- Daftar peralatan
- Jadwal pemeliharaan
- Riwayat pemeliharaan
- Laporan kerusakan (jika ada)
- Status peralatan terbaru
- Program kalibrasi
- Jadwal kalibrasi
- Laporan kalibrasi
- Data peralatan terbaru

**Catatan Penting**:
- Pemeliharaan dilakukan secara rutin sesuai jadwal
- Kalibrasi dilakukan sesuai program yang telah ditentukan
- Status peralatan harus selalu diperbarui
- Laporan kerusakan harus dibuat jika ditemukan kerusakan

---

### 12. Proses Approval

**Deskripsi**: Proses approval untuk memastikan kualitas dan validitas data sebelum digunakan dalam proses bisnis. Approval dilakukan untuk transaksi (Approval LS) dan data master (Approval DM).

**Diagram**: Business Process Approval

**Role yang Terlibat**:
- **Approver**: Melakukan review dan approval terhadap transaksi atau data master
- **Admin**: Membuat transaksi atau data master yang memerlukan approval
- **Manager**: Melakukan final approval untuk transaksi penting

**Jenis Approval**:

#### 1. Approval LS (Laboratory Sample) - Approval Transaksi

**Deskripsi**: Approval LS digunakan untuk approval transaksi yang terkait dengan sample dan pengujian, seperti Testing Order, Planning Taking Sample, Taking Sample, Sample Handling, Testing Process, dan Testing Review.

**Implementasi Sistem**: Form "Approval LS" di modul APPROVAL

**Fungsi**: Form ini digunakan untuk melakukan approval terhadap transaksi, termasuk:
- Detail Transaksi - Menampilkan informasi lengkap transaksi yang akan di-approve
- Detail Sample (untuk Testing Order) - Menampilkan daftar sample beserta detailnya
- Detail Price - Menampilkan breakdown harga (Gross, Discount, DPP, VAT, PPH, NET)
- Modal Approval - Form untuk melakukan approval dengan field:
  - Status - Dropdown dengan opsi: CHECKED, VERIFIED, APPROVED, REJECT, CANCEL
  - Approval Date - Tanggal approval

Form ini memungkinkan approver untuk melihat detail lengkap transaksi sebelum melakukan approval. Status approval menentukan apakah transaksi dapat dilanjutkan ke proses berikutnya atau ditolak.

#### 2. Approval DM (Data Master) - Approval Data Master

**Deskripsi**: Approval DM digunakan untuk approval data master seperti Equipment, Sample, Formula, BOM (Bill of Materials), dan Formula Reference. Approval ini memastikan data master yang digunakan dalam sistem sudah divalidasi dan disetujui.

**Implementasi Sistem**: Form "Approval DM" di modul APPROVAL

**Fungsi**: Form ini digunakan untuk melakukan approval terhadap data master, termasuk:
- Detail Data Master - Menampilkan informasi lengkap data master yang akan di-approve (Equipment, Sample, Formula, BOM, atau Formula Reference)
- Modal Approval - Form untuk melakukan approval dengan field:
  - Status - Dropdown dengan opsi: CHECKED, VERIFIED, APPROVED, REJECT, CANCEL
  - Approval Date - Tanggal approval
  - Description - Deskripsi atau komentar approval (opsional)

Form ini memungkinkan approver untuk melihat detail lengkap data master sebelum melakukan approval. Status approval menentukan apakah data master dapat digunakan dalam sistem atau perlu direvisi.

**Alur Proses Approval**:

1. **Mulai** → Admin/User membuat transaksi atau data master
2. **Transaksi/Data Master Dibuat** - Status awal: Pending Approval
3. **Approval Request** - Sistem mengirimkan notifikasi ke approver
4. **Approver Review** - Approver melihat detail transaksi/data master
5. **Decision: Setujui?**
   - **Ya**: 
     - Pilih Status: CHECKED, VERIFIED, atau APPROVED
     - Isi Approval Date
     - Isi Description (opsional)
     - Submit Approval
   - **Tidak**: 
     - Pilih Status: REJECT atau CANCEL
     - Isi Approval Date
     - Isi Description (alasan penolakan)
     - Submit Approval
6. **Update Status** - Sistem memperbarui status transaksi/data master
7. **Decision: Semua Approval Selesai?**
   - **Ya**: Transaksi/Data Master dapat digunakan
   - **Tidak**: Menunggu approval berikutnya
8. **Selesai**

**Output**:
- Status approval transaksi/data master
- Riwayat approval (approver, tanggal, status)
- Notifikasi approval kepada user terkait
- Transaksi/data master yang telah disetujui dapat digunakan

**Catatan Penting**:
- Approval dapat dilakukan secara bertahap (multi-level approval)
- Status approval menentukan apakah transaksi/data master dapat dilanjutkan
- Approval REJECT atau CANCEL memerlukan revisi dari pembuat transaksi/data master
- Riwayat approval tersimpan untuk audit trail

---

## Integrasi Data

**Deskripsi**: Semua proses bisnis utama mengirimkan data ke sistem integrasi data untuk konsolidasi dan pelaporan.

**Diagram**: Business Process To Be - Integrasi Data

**Proses yang Terintegrasi**:

1. **Administrasi Sampel Uji** → **Integrasi Data**
   - Data permintaan pengujian
   - Data pembayaran
   - Data LHU

2. **Penanganan Sampel** → **Integrasi Data**
   - Data pengolahan sampel
   - Data hasil pengujian
   - Data LHU

3. **Manajemen Persediaan** → **Integrasi Data**
   - Data stock opname
   - Data penggunaan bahan uji
   - Data persediaan

4. **Manajemen Aset** → **Integrasi Data**
   - Data pemeliharaan peralatan
   - Data kalibrasi
   - Data status peralatan

**Integrasi Eksternal**:

- **API CIS**: Integrasi untuk data pembayaran pelanggan
  - Digunakan dalam proses Verifikasi Pembayaran
  - Digunakan dalam proses Penerbitan LHU

**Manfaat Integrasi**:
- Konsolidasi data dari semua proses
- Pelaporan terpusat
- Analisis data yang lebih komprehensif
- Tracking end-to-end dari semua proses

---

## Role dan Tanggung Jawab

### 1. Pelanggan
**Tanggung Jawab**:
- Melakukan pendaftaran
- Mengisi form permintaan pengujian
- Melakukan pembayaran
- Mengakses portal untuk mengecek status
- Mengunduh LHU
- Mengisi feedback

### 2. Pelayanan Kepada Pelanggan Admin
**Tanggung Jawab**:
- Menganalisa permintaan pengujian
- Mengisi data pelanggan
- Mengkalkulasi biaya pengujian
- Menerbitkan tagihan
- Verifikasi pembayaran
- Menyiapkan dokumen pengajuan
- Memberikan LHU hard copy

### 3. Manager Teknis
**Tanggung Jawab**:
- Melakukan Kaji Ulang Permintaan (KUP)
- Menganalisa ketersediaan peralatan dan bahan uji
- Menerima contoh uji (disposisi teknis)
- Menganalisa permintaan pengujian
- Membuat jadwal pengambilan sampel
- Verifikasi LHU

### 4. Analis
**Tanggung Jawab**:
- Menganalisa ketersediaan analis dan metode uji
- Mengkonfirmasi ketersediaan
- Melakukan persiapan pengujian
- Melakukan pengujian
- Mencatat hasil pengujian
- Melakukan kalibrasi peralatan
- Membuat daftar peralatan
- Membuat jadwal pemeliharaan
- Melakukan pemeriksaan dan pemeliharaan
- Membuat laporan kerusakan
- Membuat riwayat peralatan

### 5. Penyelia (Supervisor)
**Tanggung Jawab**:
- Mengkonfirmasi pengolahan sampel
- Mengkonfirmasi hasil uji
- Mengkonfirmasi hasil rekonsiliasi persediaan

### 6. Admin Persediaan
**Tanggung Jawab**:
- Mengkonfirmasi penggunaan peralatan dan bahan uji
- Membuat daftar persediaan
- Melakukan stock opname
- Mengecek batas minimum persediaan
- Melakukan rekap
- Memperbarui data persediaan
- Disposal bahan uji kadaluarsa

### 7. Manajemen Aset Supervisor
**Tanggung Jawab**:
- Membuat program kalibrasi
- Mengajukan permintaan kalibrasi
- Melakukan pemutakhiran data peralatan

### 8. Manajer Lab
**Tanggung Jawab**:
- Mengkonfirmasi permintaan kalibrasi

### 9. Internal/External Kalibrasi
**Tanggung Jawab**:
- Melakukan kalibrasi peralatan
- Membuat laporan kalibrasi

### 10. PPS (Pengambilan Sampel)
**Tanggung Jawab**:
- Melakukan pengambilan sampel di lapangan
- Melakukan pengujian in-situ (jika diperlukan)
- Mencatat informasi sampel
- Membawa sampel ke laboratorium

---

## Glossary

**LHU**: Laporan Hasil Uji - Dokumen resmi yang berisi hasil pengujian sampel

**KUP**: Kaji Ulang Permintaan - Proses review teknis untuk menentukan kelayakan permintaan pengujian

**MoU**: Memorandum of Understanding - Perjanjian kerjasama antara laboratorium dan pelanggan

**Pra-Bayar**: Sistem pembayaran dimana pelanggan membayar sebelum pengujian dilakukan

**Pasca-Bayar**: Sistem pembayaran dimana pelanggan membayar setelah pengujian selesai (biasanya untuk pelanggan MoU)

**SPK**: Surat Perintah Kerja - Dokumen yang mengatur jadwal dan detail pengambilan sampel

**In-situ**: Pengujian yang dilakukan langsung di lokasi pengambilan sampel

**Stock Opname**: Proses penghitungan fisik persediaan untuk memastikan kesesuaian dengan data sistem

**Kalibrasi**: Proses pengecekan dan penyesuaian akurasi peralatan pengujian

**Disposal**: Proses pembuangan bahan uji yang sudah kadaluarsa atau tidak layak digunakan

**CIS**: Customer Information System - Sistem informasi pelanggan yang terintegrasi

**Barcode**: Kode batang untuk identifikasi dan tracking sampel

**Parameter Uji**: Jenis pengujian yang akan dilakukan pada sampel

**Metode Uji**: Prosedur standar yang digunakan untuk melakukan pengujian

**Analis**: Personel yang melakukan pengujian di laboratorium

**Penyelia**: Supervisor yang mengawasi dan mengkonfirmasi hasil pengujian

---

## Catatan Implementasi

### Teknologi yang Digunakan:
- **Backend**: Laravel (PHP Framework)
- **Database**: MySQL/PostgreSQL
- **Queue System**: Laravel Queue dengan PM2
- **API Integration**: RESTful API untuk integrasi dengan CIS
- **Authentication**: JWT/Sanctum

### Endpoint API yang Relevan:
- `/api/testing-order` - Testing Order Management
- `/api/sample-handling` - Sample Handling
- `/api/sample-registration` - Sample Registration
- `/api/taking-sample` - Taking Sample
- `/api/testing-process` - Testing Process
- `/api/testing-review` - Testing Review (KUP)
- `/api/customer` - Customer Management
- `/api/equipment` - Equipment Management
- `/api/inventory` - Inventory Management

### Notifikasi:
- Sistem menggunakan `ActionNotificationService` untuk mengirim notifikasi email
- Notifikasi dikirim untuk setiap aksi penting dalam proses bisnis
- Queue system digunakan untuk memproses notifikasi secara asynchronous

---

## Versi Dokumen

**Versi**: 1.0  
**Tanggal**: 2025  
**Penulis**: Tim Development SALIMS  
**Status**: Draft Final

---

## Kontak dan Dukungan

Untuk pertanyaan atau dukungan terkait manual book ini, silakan hubungi:
- **Email**: my.orbitteam@gmail.com
- **Tim Development**: Tim SALIMS

---

*Dokumen ini dibuat berdasarkan diagram BPMN yang telah disetujui dan dapat digunakan sebagai referensi untuk implementasi dan dokumentasi sistem.*

