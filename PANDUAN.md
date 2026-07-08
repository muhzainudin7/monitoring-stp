# Panduan Aplikasi Monitoring STP — PLN UIP Sulawesi

> **Aplikasi sudah online**: https://muhzainudin7.github.io/monitoring-stp/
> Kode tersimpan di: https://github.com/muhzainudin7/monitoring-stp

Aplikasi ini satu file saja: `index.html`, dan bersifat **hanya-baca (viewer)**.
Siapa pun yang membuka URL-nya hanya bisa melihat status, membuka halaman Detail,
dan mengunggah dokumen lewat link OneDrive. **Satu-satunya cara mengubah data adalah
Anda mengedit spreadsheet monitoring** — aplikasi mengikuti otomatis.

## Cara kerja singkat

```
Spreadsheet Google                    ← hanya Anda yang mengubah (setelah cek file di OneDrive)
  ├─ sheet "REKAP"                    → status 10 dokumen + Pending Item per proyek
  └─ sheet per-proyek                 → rincian pending item (halaman Detail)
        ↓ dibaca otomatis saat aplikasi dibuka / tombol muat ulang (ikon panah memutar)
Aplikasi (index.html di-hosting)      ← dibuka siapa saja lewat browser, hanya-baca
        ↓ tombol "Lengkapi Dokumen"
Link OneDrive "Request Files"         ← orang lain mengunggah dokumen (umumnya PDF)
```

- Progres proyek dihitung dari **11 item**: 10 dokumen STP + PNDG (Pending Item, kolom P).
- Baris yang Anda **sembunyikan** di sheet REKAP tidak ikut tampil (mis. proyek KM 2025
  yang sudah selesai).
- Tombol **Detail** membuka halaman rincian pending item proyek tersebut — datanya diambil
  dari sheet proyek yang bersangkutan (bagian "Pending Item & Catatan Hasil Invent
  STOP-STAP"), menampilkan: nomor, deskripsi, status Open/Close, deadline (untuk yang
  Open), dan tanggal completion (untuk yang Close).

## 1. Hosting lewat GitHub Pages (gratis)

1. Buat akun di https://github.com (gratis).
2. Klik tombol **+** (kanan atas) → **New repository** → beri nama, misal `monitoring-stp`
   → pilih **Public** → **Create repository**.
3. Di halaman repo, klik **uploading an existing file** (atau Add file → Upload files),
   tarik-taruh `index.html`, lalu klik **Commit changes**.
4. Buka **Settings → Pages** (menu kiri). Pada "Build and deployment":
   Source = **Deploy from a branch**, Branch = **main**, folder **/ (root)** → **Save**.
5. Tunggu ±1–2 menit. URL aplikasi muncul di halaman yang sama:
   `https://<nama-akun>.github.io/monitoring-stp/`
6. Bagikan URL itu ke grup WhatsApp. Di HP, buka URL → menu browser →
   **"Tambahkan ke layar utama"** agar tampil seperti aplikasi.

Memperbarui aplikasi nanti: buka repo → klik `index.html` → ikon pensil / Upload ulang →
Commit. URL tidak berubah.

Alternatif yang lebih cepat tanpa GitHub: **Netlify Drop** (https://app.netlify.com/drop) —
tarik-taruh folder berisi `index.html`, langsung dapat URL.

## 2. Menyiapkan spreadsheet

1. Spreadsheet dibagikan: **Bagikan → Siapa saja yang memiliki link → Pelihat (Viewer)**.
   (Saat ini sudah benar.)
2. Sheet **REKAP** dengan susunan kolom seperti sekarang (B=No, C=UPP, D=Nama Proyek,
   E=Target, F–O = 10 dokumen, P=Pending Item). Nilai sel: `OK` / `PROSES` / `NO`.
3. Proyek yang sudah tidak perlu dimonitor cukup **disembunyikan barisnya** — otomatis
   hilang dari aplikasi.
4. Sheet rincian per proyek dibiarkan seperti sekarang (tabel "Pending Item & Catatan
   Hasil Invent STOP-STAP" dengan kolom No/Deskripsi/Deadline/PIC/Checklist/Tanggal
   Diserahkan). Checklist `v` = Close, `x`/kosong = Open.
5. **Jika nama proyek di REKAP diganti atau proyek baru ditambahkan**, halaman Detail
   mencari sheet dengan nama yang sama persis dengan nama proyek di REKAP. Agar rincian
   terbaca, samakan nama sheet-nya (atau beri tahu pengembang untuk memperbarui peta nama
   di aplikasi).

### Link upload OneDrive per proyek

Supaya tombol **"Lengkapi Dokumen"** berfungsi untuk semua orang:

1. Di sheet REKAP, isi header kolom **S** (baris 4) dengan teks: `LINK UPLOAD`.
2. Untuk tiap proyek, tempel link **OneDrive "Request Files"** (OneDrive → klik kanan
   folder → Minta file / Request files) di kolom S pada baris proyek tersebut.
3. Muat ulang aplikasi — tombol langsung mengarah ke link itu.

## 3. Isi aplikasi

- **Beranda** — ringkasan (total proyek, % kelengkapan, selesai, belum lengkap), filter
  UPP dan kelompok (KM 2026 / Beyond KM 2026), pencarian, dan daftar proyek
  **10 kartu per halaman** (tombol halaman di bawah). Tiap kartu: 11 kotak indikator
  (10 dokumen + PNDG; hijau = OK, kuning = proses, merah = belum), progres X/11, tombol
  **Lengkapi Dokumen** dan **Detail**.
- **Detail** — ringkasan proyek + daftar pending item (Open merah dengan deadline,
  Close hijau dengan tanggal completion).
- **Rekap** — bahan rapat bulanan: % kelengkapan, proyek Selesai/Proses/Belum jalan,
  grafik kelengkapan per UPP, grafik item paling menghambat (termasuk Pending Item),
  tombol **Ekspor PDF** (laporan formal: tabel kelompok TARGET STP (KM) 2026 lalu per
  UPP) dan **Bagikan**.

## 4. Jika data tidak termuat

- Aplikasi harus dibuka lewat **URL online** (GitHub Pages/Netlify). Jika file
  `index.html` dibuka langsung dengan dobel-klik, browser memblokir pengambilan data
  dari Google — yang tampil hanya data cadangan bawaan.
- Pastikan HP/laptop online, lalu tekan ikon panah memutar di kanan atas.
- Pastikan spreadsheet masih dibagikan "siapa saja yang memiliki link".
- Tanpa koneksi, aplikasi menampilkan data hasil pemuatan terakhir (tersimpan di browser).
