# kodkod

Hub aplikasi belajar interaktif untuk siswa. Dibuat dengan HTML statis biasa — tidak perlu build tool, langsung bisa di-deploy ke GitHub Pages.

## Struktur folder

```
kodkod-repo/
├── index.html                     ← halaman utama (hub kodkod)
├── apps/
│   ├── kartu-software/
│   │   └── index.html             ← ganti dengan app Kartu Software kamu
│   └── mouse-move/
│       └── index.html             ← ganti dengan app Mouse Move kamu
├── assets/
│   ├── css/                       ← untuk stylesheet bersama (opsional)
│   ├── js/                        ← untuk script bersama (opsional)
│   └── img/                       ← untuk gambar/ikon (opsional)
└── README.md
```

## Menambah app baru

1. Buat folder baru di dalam `apps/`, contoh: `apps/nama-app-baru/`
2. Taruh semua file app tersebut (HTML/CSS/JS-nya) di dalam folder itu, dengan `index.html` sebagai file utama.
3. Tambahkan satu `<a class="card">` baru dan satu `<a class="dock-icon">` baru di `index.html` (bagian hub), lalu daftarkan path-nya di object `routes` dalam tag `<script>`.
4. Tambahkan header & footer kodkod ke `index.html` app tersebut (lihat bagian di bawah).

Setiap app boleh berdiri sendiri (App terpisah, library terpisah) — tidak akan bentrok satu sama lain selama masing-masing ada di foldernya sendiri.

## Header & footer kodkod di setiap app

Supaya semua app terasa satu keluarga dengan hub-nya, setiap `index.html` di dalam `apps/*/` sebaiknya punya header (link kembali ke kodkod) dan footer (link kembali + label app). Stylesheet-nya sudah disiapkan terpusat di `assets/css/kodkod-frame.css` — tidak perlu ditulis ulang tiap app.

**1. Import stylesheet-nya** di `<head>`:
```html
<link rel="stylesheet" href="../../assets/css/kodkod-frame.css">
```
(`../../` karena app ada di `apps/nama-app/index.html`, dua tingkat di bawah root — sesuaikan jumlah `../` kalau strukturnya beda)

**2. Tempel header** persis setelah `<body>`:
```html
<header class="kodkod-frame-header">
  <a class="kodkod-frame-back" href="../../index.html">
    <svg width="16" height="16" viewBox="0 0 24 24" fill="none"><path d="M19 12H5M5 12L11 6M5 12L11 18" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
    <span class="kodkod-frame-logo-dot"></span>
    kodkod
  </a>
  <span class="kodkod-frame-title">Nama App Kamu</span>
</header>
```

**3. Tempel footer** sebelum `</body>`:
```html
<footer class="kodkod-frame-footer">
  <a href="../../index.html">
    <svg width="14" height="14" viewBox="0 0 24 24" fill="none"><path d="M19 12H5M5 12L11 6M5 12L11 18" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
    Kembali ke semua apps kodkod
  </a>
  <p>Nama App Kamu &middot; bagian dari kodkod</p>
</footer>
```

Ganti "Nama App Kamu" di dua tempat (header & footer) sesuai nama app-nya. Link `../../index.html` di keduanya sudah langsung menuju halaman utama kodkod — tidak perlu diubah selama app-nya tetap di `apps/nama-app/`.

Ketiga app contoh (`kartu-software`, `mouse-move`, `kuis-cepat`) sudah dipasangi header & footer ini — bisa dipakai sebagai referensi langsung.

## Deploy ke GitHub Pages

1. Push seluruh isi folder ini ke repo GitHub kamu (`kodkod-repo` bisa diganti nama apa saja).
2. Buka **Settings → Pages** di repo tersebut.
3. Di bagian **Source**, pilih branch `main` dan folder `/ (root)`.
4. Simpan — GitHub akan memberi kamu URL seperti `https://username.github.io/nama-repo/`.
5. Tunggu 1-2 menit, lalu buka URL-nya. Halaman hub kodkod akan langsung tampil di root, dan setiap app bisa diakses lewat `/apps/nama-app/`.

## Catatan

- Semua app di `apps/` diakses lewat path relatif, jadi tidak perlu ubah apa pun kalau nama repo GitHub-nya berubah.
- Kalau salah satu app butuh library eksternal (misalnya dari CDN), tambahkan langsung di dalam `index.html` app tersebut — tidak akan memengaruhi app lain.
