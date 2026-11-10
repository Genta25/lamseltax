---
name: lamsel-tax-mapping-design
description: Sistem desain Lamsel Tax Mapping — aplikasi survei & pemetaan potensi pajak daerah Bapenda Kabupaten Lampung Selatan (kolaborasi Pemkab Lamsel x Universitas Teknokrat Indonesia) dengan nuansa civic-tech navy blue (#0B2A5B) dan font Plus Jakarta Sans. Gunakan skill ini setiap kali pengguna meminta layar, komponen, modal, atau halaman baru yang harus konsisten dengan Lamsel Tax Mapping, atau menyebut Beranda petugas, dashboard admin Bapenda, peta persebaran GIS, formulir pendataan usaha baru, daftar/detail objek pajak, NOP, PBJT (restoran, perhotelan, hiburan), pajak reklame, antrean verifikasi, revisi survei, profil petugas lapangan, bottom sheet detail objek, atau aplikasi pemerintah daerah/pajak/GIS bergaya serupa — walaupun pengguna tidak menyebut "Lamsel Tax Mapping" secara eksplisit. Output berupa HTML + Tailwind CSS (CDN) berbahasa Indonesia, mobile-first untuk petugas dan desktop untuk admin.
---

# Lamsel Tax Mapping — Sistem Desain

Aplikasi dua permukaan untuk Bapenda Kabupaten Lampung Selatan:

| Permukaan | Pengguna | Layout |
|---|---|---|
| **Mobile app** | Petugas lapangan (contoh: Budi Santoso) | Kolom tunggal `max-w-md`/`max-w-lg`, bottom navigation 4 tab |
| **Web admin** | Administrator/verifikator Bapenda (contoh: Drs. Hendra Gunawan) | Sidebar kiri `w-72`/`w-64` + konten utama, grid KPI & tabel |

Karakter visual: **resmi, tepercaya, padat informasi, tenang**. Dasar navy blue, aksen biru cerah untuk aksi, dan empat warna status yang bermakna hukum/administratif. Tidak ada gradien dekoratif, tidak ada ilustrasi playful.

---

## 1. Aturan Wajib (jangan pernah dilanggar)

1. **Disclaimer resmi** harus muncul di setiap layar yang menampilkan angka potensi pajak, persis:
   > `Estimasi simulasi — bukan penetapan pajak, tagihan, atau bukti pembayaran.`
2. **Dasar hukum** (di callout/footer layar yang relevan):
   > `Berdasarkan Perda Kab. Lampung Selatan No. 1 Tahun 2024 tentang Pajak Daerah dan Retribusi Daerah.`
3. **Footer hak cipta** persis (perhatikan tidak ada spasi setelah ©):
   > `Copyright©2026 by Genta dan Dr. Erliyan Redy Susanto, M.Kom`
   diikuti tautan: `Kabupaten Lampung Selatan` • `Universitas Teknokrat Indonesia` • `Kebijakan Privasi` (dipisah `•`).
4. **Dua logo institusi** (Pemkab Lampung Selatan & Universitas Teknokrat Indonesia) tampil di header/sidebar/banner, selalu dengan `alt` bertuliskan `Logo Pemkab Lampung Selatan` dan `Logo Universitas Teknokrat Indonesia`. Label teks pendamping: `Pemkab Lamsel` / `Univ Teknokrat` (ringkas) atau nama lengkap bila ruang cukup.
5. **Bahasa Indonesia** untuk semua teks UI. Atribut `lang="id"`.
6. **Nama instansi ditulis `Bapenda`** (Badan Pendapatan Daerah). Jangan menulis "Bappenda"/"Bappeda" untuk instansi ini.
7. **Status verifikasi hanya empat** (lihat bagian 4). Jangan menambah warna status baru.
8. Angka rupiah memakai titik pemisah ribuan: `Rp 14.500.000`, satuan periode di samping dengan teks kecil: `/ bulan` atau `/ tahun`. Untuk agregat: `Rp 48,25 M` (koma desimal).

---

## 2. Setup Teknis (head standar)

Setiap file HTML memakai tumpukan berikut:

```html
<html lang="id">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:wght,FILL@100..700,0..1&display=swap" rel="stylesheet">
<script src="https://cdn.tailwindcss.com?plugins=forms,container-queries"></script>
<script id="tailwind-config"> /* lihat bagian 3 */ </script>
<style>
  .material-symbols-outlined {
    font-variation-settings: 'FILL' 0, 'wght' 400, 'GRAD' 0, 'opsz' 24;
    display: inline-block; vertical-align: middle; line-height: 1;
  }
  .no-scrollbar::-webkit-scrollbar { display: none; }
  .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
</style>
</head>
```

- Ikon: **Material Symbols Outlined**. Ikon aktif/terpilih memakai `style="font-variation-settings:'FILL' 1;"`.
- Untuk peta fullscreen mobile gunakan viewport `maximum-scale=1.0, user-scalable=no` dan container `h-[100dvh]`.
- Dark mode `darkMode: "class"` diaktifkan di konfigurasi, tetapi tampilan utama adalah **light**.

---

## 3. Token Desain (salin utuh ke `tailwind.config`)

```js
tailwind.config = {
  darkMode: "class",
  theme: { extend: {
    colors: {
      "primary": "#00163a",
      "primary-container": "#0b2a5b",      // NAVY UTAMA: header, sidebar, tombol primer
      "on-primary": "#ffffff",
      "on-primary-container": "#7a93ca",   // teks sekunder di atas navy
      "primary-fixed": "#d8e2ff",
      "primary-fixed-dim": "#aec6ff",
      "on-primary-fixed": "#001a42",
      "on-primary-fixed-variant": "#2c4678",
      "inverse-primary": "#aec6ff",
      "secondary": "#0051d5",              // BIRU AKSI: tab aktif, link, CTA sekunder
      "secondary-container": "#316bf3",
      "on-secondary": "#ffffff",
      "on-secondary-container": "#fefcff",
      "secondary-fixed": "#dbe1ff",
      "secondary-fixed-dim": "#b4c5ff",
      "on-secondary-fixed": "#00174b",
      "on-secondary-fixed-variant": "#003ea8",
      "tertiary": "#001c10",
      "tertiary-container": "#003321",
      "tertiary-fixed": "#85f8c4",
      "tertiary-fixed-dim": "#68dba9",
      "on-tertiary": "#ffffff",
      "on-tertiary-container": "#29a678",
      "on-tertiary-fixed": "#002114",
      "on-tertiary-fixed-variant": "#005137",
      "error": "#ba1a1a",
      "error-container": "#ffdad6",
      "on-error": "#ffffff",
      "on-error-container": "#93000a",
      "background": "#f9f9ff",
      "surface": "#f9f9ff",
      "surface-bright": "#f9f9ff",
      "surface-dim": "#cfdaf2",
      "surface-container-lowest": "#ffffff",  // kartu
      "surface-container-low": "#f0f3ff",     // panel/callout/sub-area
      "surface-container": "#e7eeff",
      "surface-container-high": "#dee8ff",
      "surface-container-highest": "#d8e3fb",
      "surface-variant": "#d8e3fb",
      "surface-tint": "#455e91",
      "on-surface": "#111c2d",
      "on-surface-variant": "#44474f",
      "on-background": "#111c2d",
      "outline": "#747780",
      "outline-variant": "#c4c6d0",
      "inverse-surface": "#263143",
      "inverse-on-surface": "#ecf1ff"
    },
    borderRadius: { DEFAULT: "0.25rem", lg: "0.5rem", xl: "0.75rem", full: "9999px" },
    spacing: {
      "space-xs": "0.25rem", "space-sm": "0.5rem", "space-md": "1rem",
      "space-lg": "1.5rem", "space-xl": "2rem",
      "gutter-mobile": "1rem", "gutter": "1.5rem",
      "margin-mobile": "1rem", "margin": "2rem"
    },
    fontFamily: {
      /* semua kunci berikut = ["Plus Jakarta Sans"] */
      "body-sm": ["Plus Jakarta Sans"], "body-md": ["Plus Jakarta Sans"], "body-lg": ["Plus Jakarta Sans"],
      "label-sm": ["Plus Jakarta Sans"], "label-md": ["Plus Jakarta Sans"], "label-lg": ["Plus Jakarta Sans"],
      "headline-sm": ["Plus Jakarta Sans"], "headline-md": ["Plus Jakarta Sans"],
      "headline-lg": ["Plus Jakarta Sans"], "headline-xl": ["Plus Jakarta Sans"],
      "headline-lg-mobile": ["Plus Jakarta Sans"], "headline-xl-mobile": ["Plus Jakarta Sans"],
      "code-num": ["Plus Jakarta Sans"]
    },
    fontSize: {
      "body-sm":  ["12px", { lineHeight: "16px", fontWeight: "400" }],
      "body-md":  ["14px", { lineHeight: "20px", fontWeight: "400" }],
      "body-lg":  ["16px", { lineHeight: "24px", fontWeight: "400" }],
      "label-sm": ["11px", { lineHeight: "14px", letterSpacing: "0.05em",  fontWeight: "700" }],
      "label-md": ["12px", { lineHeight: "16px", letterSpacing: "0.025em", fontWeight: "600" }],
      "label-lg": ["14px", { lineHeight: "20px", fontWeight: "600" }],
      "headline-sm": ["16px", { lineHeight: "24px", fontWeight: "600" }],
      "headline-md": ["20px", { lineHeight: "28px", fontWeight: "600" }],
      "headline-lg": ["28px", { lineHeight: "36px", fontWeight: "700" }],
      "headline-xl": ["36px", { lineHeight: "44px", fontWeight: "700" }],
      "headline-lg-mobile": ["22px", { lineHeight: "30px", fontWeight: "700" }],
      "headline-xl-mobile": ["28px", { lineHeight: "36px", fontWeight: "700" }],
      "code-num": ["13px", { lineHeight: "18px", fontWeight: "500" }]
    }
  } }
}
```

### Pemakaian token

| Peran | Kelas |
|---|---|
| Header, sidebar, tombol primer | `bg-primary-container text-on-primary` (hover: `hover:bg-primary`) |
| Sub-banner di bawah header (mobile) | `bg-primary` |
| Tab aktif, link, tombol sekunder, ikon judul seksi | `text-secondary` / `bg-secondary text-on-secondary` |
| Latar halaman | `bg-surface` / `bg-background` |
| Kartu | `bg-surface-container-lowest rounded-xl border border-outline-variant shadow-sm` |
| Panel dalam kartu, callout | `bg-surface-container-low` |
| Judul | `text-primary` (navy gelap) |
| Teks isi | `text-on-surface`; sekunder `text-on-surface-variant`; tersier `text-outline` |
| Teks kecil terdampak | `text-label-sm` (uppercase untuk label metrik), `text-body-sm` untuk deskripsi |
| Angka, NOP, koordinat | `font-code-num` (mobile) atau `font-mono` (NOP di tabel/detail) |

**Radius:** kartu `rounded-xl`, tombol/input `rounded-lg`, chip filter `rounded-full`, bottom sheet `rounded-t-2xl`, badge status `rounded-md` (kartu) atau `rounded-full` (tabel).
**Bayangan:** `shadow-sm` default; `shadow-md` untuk tombol CTA & kontrol peta; `shadow-xl/2xl` hanya untuk overlay/sheet.
**Interaksi:** `active:scale-95` (tombol kecil) atau `active:scale-[0.98]` (CTA lebar), `transition-all`/`transition-colors`.

---

## 4. Status Verifikasi (empat saja, dengan makna tetap)

| Status | Label | Chip (kelas) | Titik/penanda peta | Ikon | Border kiri kartu |
|---|---|---|---|---|---|
| Valid | `Terverifikasi` | `bg-[#D1FAE5] text-[#065F46] border border-[#6EE7B7]` | `#059669` / `#10B981` | `verified`, `check_circle` | `border-l-4 border-l-[#065F46]` |
| Antre | `Menunggu Verifikasi` | `bg-[#FEF3C7] text-[#92400E] border border-[#FCD34D]` | `#D97706` / `#F59E0B` (animasi pulse) | `pending_actions`, `hourglass_top` | (tanpa border kiri) |
| Revisi | `Perlu Perbaikan` (varian pendek: `Perlu Revisi`) | `bg-[#FFE4E6] text-[#9F1239] border border-[#FDA4AF]` | `#E11D48` / `#EF4444` | `warning`, `error`, `report` | `border-l-4 border-l-error` |
| Draf | `Draft` | `bg-[#F3F4F6] text-[#374151] border border-[#D1D5DB]` | `#6B7280` | `draft`, `pending` | (tanpa border kiri) |

Pola chip standar (mobile, di kartu):

```html
<span class="inline-flex items-center px-2 py-0.5 rounded-md text-label-sm font-label-sm uppercase font-bold tracking-wide bg-[#FEF3C7] text-[#92400E] border border-[#FCD34D] whitespace-nowrap">Menunggu Verifikasi</span>
```

Pola chip di tabel admin (pil dengan titik): `rounded-full text-[11px] font-bold uppercase tracking-wide px-2.5 py-1` + `<span class="w-1.5 h-1.5 rounded-full bg-[#92400E]">` di depan teks.

**Tombol aksi mengikuti status:**

| Status | Aksi mobile | Aksi admin |
|---|---|---|
| Terverifikasi | `Unduh NOP` / `Unduh BAP` (outline) | `Cetak SKPD` (netral) |
| Menunggu | `Detail` / `Lihat Detail` (outline) | `Verifikasi` (`bg-secondary`) |
| Perlu Perbaikan | `Perbaiki` / `Perbaiki Data` (`bg-error text-on-error`, ikon kamera/lokasi) | `Revisi` (`bg-rose-700`) |
| Draft | `Lanjutkan` / `Lanjutkan Entri` (`bg-secondary` atau navy) | `Lengkapi` (`bg-slate-200`) |

---

## 5. Domain & Konten

**Wilayah (kecamatan, urutan chip):** Semua, Kalianda, Natar, Jati Agung, Tanjung Bintang, Sidomulyo, Katibung, Penengahan, Ketapang. Chip boleh menampilkan jumlah: `Kalianda (428)`.

**Kategori pajak (jenis objek):**

| Label panjang | Label pendek | Ikon |
|---|---|---|
| PBJT Makanan/Minuman/Restoran | PBJT Restoran | `restaurant` |
| PBJT Perhotelan | PBJT Hotel | `hotel` |
| Pajak Reklame | Reklame | `featured_video` / `ad_units` / `campaign` |
| PBJT Kesenian/Hiburan | Hiburan | `theater_comedy` |
| Pajak Parkir | Parkir | `local_parking` |
| BPHTB / PBB-P2 | BPHTB/PBB-P2 | `local_gas_station` (contoh SPBU) |

**Tarif simulasi PBJT:** 10 %. Parameter simulasi restoran: jumlah meja/kursi, estimasi pengunjung/hari, rata-rata transaksi per pengunjung (Rp). Hotel: jumlah kamar, tarif PBJT, okupansi rata-rata (%).

**NOP daerah:** format `18.01.040.002.012-0045.0` (monospace, `font-mono text-xs font-semibold text-primary`). Awalan `18.01` = Lampung Selatan. Dalam satu prototipe gunakan satu format NOP yang konsisten per objek.

**Koordinat:** `-5.7284° S, 105.5921° E` (pil GPS) atau `Koordinat: -5.7284, 105.5921` (di kartu). Akurasi GPS ditampilkan sebagai `±3 meter` / `Akurasi GPS 98.2%`.

**Data contoh yang konsisten** (gunakan kembali agar antarlayar nyambung):

| Objek | Kategori | Kecamatan | Potensi | Status |
|---|---|---|---|---|
| Hotel Krakatau Indah | PBJT Perhotelan | Kalianda | Rp 14.500.000 / bulan | Menunggu Verifikasi |
| Warung Makan Sari Rasa | PBJT Restoran | Natar | Rp 2.800.000 / bulan | Perlu Perbaikan |
| Rumah Makan Pantai Merak | PBJT Restoran | Kalianda | Rp 5.250.000 / bulan | Terverifikasi |
| Toko Sumber Rejeki | Pajak Reklame | Sidomulyo | Rp 750.000 / tahun | Draft |

**Penanda waktu:** `Hari ini 14:30 WIB`, `17 Mar 2026`, `15 Maret 2026`. Selalu sertakan `WIB` untuk jam.

---

## 6. Komponen Mobile

### 6.1 Top App Bar + Banner Institusi (Beranda)

- `<header class="bg-primary-container text-on-primary shadow-sm w-full sticky top-0 z-40">`
- Baris 1: ikon `account_balance` + judul `Lamsel Tax Mapping` (`text-headline-sm font-bold tracking-tight`) di kiri; tombol `account_circle` bulat 32 px di kanan. Border bawah `border-outline-variant/30`.
- Banner (bawah, `bg-primary`): grid 2 kolom logo (`bg-surface-container-lowest rounded-lg border shadow-sm`, logo `h-7`), lalu sub-judul `Survei & Pemetaan Potensi Pajak Lapangan` / `Bapenda Kabupaten Lampung Selatan`, badge status `Online - GPS Aktif` (`bg-tertiary-container text-tertiary-fixed`, titik berdenyut), dan kartu petugas (avatar inisial `bg-secondary`, nama, `Petugas Lapangan Bapenda • Wilayah …`, `Reg ID`).
- Layar dalam (formulir, profil, modal) memakai versi ringkas: tombol kembali/ikon + judul layar + sub-judul `text-label-sm text-on-primary-container`, `max-w-md mx-auto`. Logo dipindah ke strip tipis `bg-surface-container-low border-b`.

### 6.2 Kartu Statistik (grid 2×2)

```html
<div class="bg-surface-container-lowest rounded-xl border border-outline-variant p-3.5 shadow-sm border-l-4 border-l-[#FCD34D]">
  <span class="text-label-sm text-on-surface-variant uppercase tracking-wider block mb-1">Menunggu Verifikasi</span>
  <div class="flex items-baseline space-x-1">
    <span class="text-headline-lg-mobile font-bold text-[#92400E]">245</span>
    <span class="text-body-sm text-on-surface-variant font-medium">Objek</span>
  </div>
  <div class="mt-2 text-label-sm text-[#92400E] font-semibold flex items-center space-x-1">
    <span class="material-symbols-outlined text-xs">pending_actions</span><span>Antrean Pemeriksaan</span>
  </div>
</div>
```
Kartu pertama (total) netral dengan aksen sudut `bg-surface-container-high/40 rounded-bl-full`; tiga lainnya memakai border kiri warna status. Judul seksi: ikon `text-secondary` + teks `text-headline-sm font-bold text-primary`.

### 6.3 Tombol Aksi Cepat

- **CTA utama** `+ Tambah Pendataan Usaha Baru`: `w-full bg-primary-container rounded-xl py-3.5 px-4 shadow-md`, ikon kotak `w-10 h-10 bg-secondary rounded-lg` berisi `add_a_photo`, sub-teks `Autolokasi GPS & Ambil Bukti Lapangan`, panah `arrow_forward` di kanan (geser saat hover).
- **Banner sinkronisasi offline** di bawahnya: `bg-surface-container-low rounded-xl border`, ikon `cloud_sync`, teks `3 formulir draft menunggu kirim` (`text-error`), tombol `Kirim Data`.

### 6.4 Chip Filter Kecamatan (horizontal scroll)

Container `flex space-x-1.5 overflow-x-auto no-scrollbar`. Aktif: `bg-primary-container text-on-primary font-bold`. Tidak aktif: `bg-surface-container-low border border-outline-variant/60 text-on-surface`. Bentuk `rounded-full px-3 py-1 whitespace-nowrap`. Di layar peta, chip kategori ditambahkan setelah pemisah vertikal tipis; chip kategori aktif memakai `bg-surface-container-high text-primary`.

### 6.5 Kartu Objek Pajak

Struktur: label kategori kecil (`text-secondary bg-surface-container rounded px-2 py-0.5 font-semibold`) → nama usaha (`text-headline-sm font-bold text-primary`) → chip status di kanan atas → dua baris info (`location_on` text-secondary; `explore` text-outline dengan `font-code-num text-xs`) → *opsional* kotak catatan verifikator → kotak potensi pajak (`bg-surface-container-low rounded-lg p-2.5 flex justify-between`) dengan tombol aksi sesuai status (bagian 4).

Kotak catatan verifikator (hanya status Perlu Perbaikan): `bg-error-container/40 border border-error-container text-error text-body-sm`, ikon `error`, awalan `Catatan Verifikator:`.

### 6.6 Callout Disclaimer / Dasar Hukum

```html
<div class="border-l-4 border-primary-container bg-surface-container-low p-3.5 rounded-r-xl border border-outline-variant/60">
  <div class="flex items-start space-x-2.5">
    <span class="material-symbols-outlined text-primary text-xl mt-0.5">info</span>
    <div>
      <h4 class="text-label-md font-bold text-primary">Pemberitahuan Resmi Lapangan:</h4>
      <p class="text-body-sm text-on-surface-variant font-medium">Estimasi simulasi — bukan penetapan pajak, tagihan, atau bukti pembayaran.</p>
      <p class="text-[10px] text-outline mt-1">Berdasarkan Perda Kab. Lampung Selatan No. 1 Tahun 2024 tentang Pajak Daerah dan Retribusi Daerah.</p>
    </div>
  </div>
</div>
```
Varian strip sticky tipis di atas konten (modal): `bg-surface-container-high border-l-4 border-primary-container px-3 py-1.5`.

### 6.7 Footer

`bg-surface-container-low border-t border-outline-variant text-center py-space-md px-gutter` (beri `mb-14` bila ada bottom nav tetap). Baris 1: (opsional) nama aplikasi `text-headline-sm font-bold text-primary`. Baris 2: teks copyright `text-body-sm text-on-surface-variant`. Baris 3: tiga tautan `text-label-sm` dipisah `•` berwarna `text-outline-variant`.

### 6.8 Bottom Navigation (4 tab, wajib seragam)

Urutan & ikon: **Beranda** (`home`) · **Data Usaha** (`business`) · **Peta** (`map`) · **Profil** (`person`).

```html
<nav class="fixed bottom-0 left-0 w-full z-50 flex justify-around items-center px-gutter-mobile h-14 bg-surface-container-lowest shadow-md border-t border-outline-variant">
  <!-- tab aktif -->
  <a class="flex flex-col items-center justify-center text-secondary font-bold border-t-2 border-secondary pt-1 pb-1 transition-all duration-200 active:scale-95 w-1/4" href="#">
    <span class="material-symbols-outlined text-xl" style="font-variation-settings:'FILL' 1;">home</span>
    <span class="text-label-sm tracking-tight mt-0.5">Beranda</span>
  </a>
  <!-- tab tidak aktif: text-on-surface-variant hover:text-primary, ikon FILL 0 -->
</nav>
```
Beri `pb-24` pada `<body>` agar konten tidak tertutup. Tab aktif ditentukan layar: Beranda untuk dashboard petugas, Data Usaha untuk formulir & modal revisi, Peta untuk GIS, Profil untuk profil.

---

## 7. Formulir Pendataan Usaha Baru (mobile)

- Header ringkas + strip logo + badge GPS di kanan (`bg-[#D1FAE5] text-[#065F46]`, `GPS Akurat (±3 meter) • Terkoneksi Satelit`).
- **Stepper**: kartu putih dengan label `Tahapan Formulir Lapangan` dan 5 batang `h-1.5 rounded-full` (`bg-secondary` selesai, `bg-outline-variant` belum).
- **Lima seksi bernomor**, tiap seksi satu kartu: badge nomor `w-6 h-6 rounded-md bg-primary-container text-on-primary text-xs font-bold` + judul `text-headline-sm font-bold text-primary` + tag kecil di kanan.
  1. Identitas Objek & Wajib Pajak (tag `Wajib Isi`) — nama usaha, pemilik, NIK/NPWPD 16 digit (`font-code-num`), telepon/WhatsApp, kategori sebagai daftar radio (terpilih: `border-2 border-secondary bg-surface-container-low`).
  2. Geolokasi & Pemetaan Spasial (tag `GNSS Realtime`) — mini peta `h-44` dengan pin tengah, tombol `Kunci Titik Koordinat GPS` (`bg-secondary`) + `Kalibrasi Ulang` (outline), kecamatan (select), alamat & patokan (textarea).
  3. Bukti Fisik & Foto Objek (tag `Watermark Aktif`) — slot unggah dengan `border border-dashed border-outline bg-surface-container-low`; pratinjau foto diberi **watermark** LAT/LON, tanggal-jam WIB, `SURVEI LAPANGAN BAPENDA LAMSEL` dan chip `Tersimpan`.
  4. Parameter Simulasi Potensi (PBJT) (tag `Simulasi 10%`) — input angka dengan satuan di dalam kolom kanan (`Unit`, `Orang`) atau awalan `Rp`; kotak hasil simulasi + disclaimer wajib.
  5. Opsi Simpan & Status — chip default `Menunggu Verifikasi`, indikator `Penyimpanan Terenkripsi`, tombol utama `Kirim untuk Verifikasi Bapenda` (navy, ikon `send`) dan tombol outline `Simpan sebagai Draft Lapangan (Offline)`.
- Input: `rounded-lg border border-outline-variant bg-white focus:border-secondary focus:ring-2 focus:ring-secondary/20`, ikon prefiks `text-[18px] text-on-surface-variant` pada `pl-9`. Tanda wajib `<span class="text-error">*</span>`.

---

## 8. Peta GIS Mobile (fullscreen)

Susunan vertikal dalam `relative w-full h-[100dvh] max-w-md mx-auto flex flex-col`:

1. **Kanvas peta** (`absolute inset-0`): latar `#E5ECE9` + `gis-grid-pattern` (garis 40 px `rgba(196,198,208,.25)`), SVG laut `#C7DCF3`/`#B3D1EE` dengan label `TELUK LAMPUNG`/`SELAT SUNDA`, tol (oranye putus-putus `#F59E0B`), jalan arteri (putih + `#D97706`), kawasan hijau `#A7F3D0`.
2. **Header melayang** (`z-30`): kartu navy `rounded-xl` berisi logo ganda + judul `Peta Spasial Lamsel` + badge `GNSS ON` + tombol layer & cari; kotak pencarian NOP (`font-code-num`, ikon `travel_explore`, `qr_code_scanner`); chip filter horizontal.
3. **Kontrol kanan**: tombol `w-10 h-10 rounded-xl` bertumpuk — satelit, heatmap potensi (`local_fire_department`), ukur jarak (`straighten`), kunci GPS (`my_location`, `bg-secondary` + ring), zoom +/−.
4. **Legenda mini kiri-bawah**: 4 status, 2 kolom, plus koordinat live dan akurasi `±1.8m`.
5. **Marker**: lingkaran `w-8 h-8 border-2 border-white shadow-md` berwarna status dengan ikon kategori + label nama (`text-[9px] font-bold bg-white/95`). Objek terpilih lebih besar (`w-9 h-9`, `border-[3px]`, `ring-2 ring-primary-container`) dengan animasi `pulse-amber` dan tooltip navy. Klaster: pil `bg-primary-container`/`bg-secondary` berisi `+45 Natar`.
6. **Bottom sheet detail** (`rounded-t-2xl max-h-[46vh]`, handle `w-12 h-1.5`): chip status + kategori, nama, pengelola, kotak NOP + alamat, grid foto (5 kol) & potensi bulanan (7 kol) dengan tarif/kamar/okupansi, callout disclaimer, tombol `Rute Lapangan` + `Foto Tambahan` (grid 2) dan `Buka Formulir Verifikasi` (navy penuh), lalu footer wajib.
7. Bottom nav (tab **Peta** aktif) tidak `fixed`, melainkan bagian akhir flex column (`relative z-40 h-14`).

---

## 9. Profil Petugas & Riwayat

- Kartu identitas: foto `w-16 h-16 rounded-xl border-2 border-outline-variant` dengan lencana `verified_user` di sudut; chip `Petugas Resmi Bapenda - Aktif` (hijau); nama + gelar, `NIP` (monospace); baris `fmd_good` zona kerja; dua sel info (Perangkat, GNSS Presisi).
- Statistik kinerja: bar progres capaian (`bg-secondary h-2 rounded-full`, mis. `89% (284 / 320 Objek)`) dan grid 2×2 memakai warna status dengan latar transparan (`bg-[#D1FAE5]/40` dsb.).
- Tab filter riwayat: `Semua (284)`, `Terverifikasi`, `Menunggu (48)`, `Perlu Revisi (18)`, `Draft Lokal (3)`; kartu riwayat mengikuti pola 6.5 dengan baris `Waktu Survei` / `Verifikator` / `Tanggal Verifikasi` / `Status Dokumen`.
- Menu pengaturan: daftar `divide-y` dengan ikon kotak `w-8 h-8 rounded-lg` (Sinkronisasi Paksa Data Offline, Panduan Teknis Pemetaan GIS, Bantuan Bapenda Lamsel). **Keluar Akun** memakai warna `error` dengan sub-teks `Selesaikan sinkronisasi sebelum logout`.

---

## 10. Modal Detail Revisi (bottom sheet)

Dipakai di atas daftar riwayat yang diburamkan (`opacity-40 blur-[1px]`); overlay `bg-[#0B2A5B]/55 backdrop-blur-[3px]`; sheet `rounded-t-2xl border-t-2 border-primary-container max-h-[88vh]`.

Urutan konten:
1. Header: chip `PERLU REVISI` + `ID: REV-2026-xxxx`, judul `Perbaikan Data Survei Lapangan`, NOP, tombol tutup `close`.
2. Kartu identitas objek + meta verifikator (nama, jabatan, waktu merah).
3. **Daftar Catatan Verifikator & Aksi Lapangan** (badge `3 Poin`): tiap poin berisi nomor bulat, judul, tag (`Kritis` merah solid / `Spasial GIS` / `Parameter`), kutipan catatan (`border-l-2` berwarna), dan satu tombol aksi (`Ambil Ulang Foto Reklame`, `Kalibrasi Ulang GPS & Peta`). Poin kritis memakai `border-2 border-error/30`.
4. **Perbandingan Data**: tabel 2 kolom `Data Lama (Ditolak)` (teks coret merah `line-through text-error`) vs `Koreksi Diperlukan` (input atau nilai baru dengan `check_circle`).
5. Textarea `Catatan Tindak Lanjut Petugas Lapangan` + tombol lampirkan berkas.
6. Callout `Dasar Hukum Penyesuaian Data:`.
7. Aksi: `Kirim Ulang Verifikasi (Resubmit)` (navy penuh), `Simpan Draf Revisi` (outline), `Hubungi Verifikator` (outline hijau, ikon `support_agent`).

---

## 11. Web Admin (desktop)

### 11.1 Kerangka
`<div class="flex flex-1 overflow-hidden min-h-screen">` → `aside` navy + `div.flex-1` (header sticky putih + `main`). Konten maksimum `max-w-[1600px] mx-auto p-gutter`. Scrollbar kustom 5 px (`#c4c6d0`).

### 11.2 Sidebar
- `w-72 bg-primary-container text-on-primary shrink-0 shadow-xl`.
- Atas: kotak ikon `w-10 h-10 rounded-lg bg-secondary-container` + `Lamsel Tax Mapping` / `Smart Economy Spatial Analytics`; grid 2 logo (`bg-primary/40 border border-outline-variant/30 rounded-lg`).
- Grup menu dengan judul `text-[10px] font-bold tracking-wider text-on-primary-container`:
  - **NAVIGASI UTAMA**: Dashboard, Data Usaha, Peta Persebaran (lencana `GIS`), Kategori Pajak, Estimasi Pajak, Verifikasi Data (lencana jumlah antrean amber).
  - **ADMINISTRASI & LAPORAN**: Laporan, Manajemen Pengguna, Data Wilayah, Riwayat Aktivitas, Pengaturan.
- Item aktif `bg-secondary-container text-on-primary font-bold shadow-sm` (ikon FILL 1); tidak aktif `text-on-primary-container hover:bg-primary hover:text-on-primary`.
- Bawah: profil admin (avatar, `Drs. Hendra Gunawan`, `NIP. …`, label `Administrator Bapenda`).

### 11.3 Header
`bg-surface-container-lowest sticky top-0 z-20 shadow-sm`: breadcrumb `Bapenda Lampung Selatan / Geospasial PAD / Ringkasan Sistem` (aktif `text-secondary font-bold`), judul `Dashboard Utama • Monitoring & Analisis Potensi Pajak Daerah`, pencarian (`Cari NOP, Wajib Pajak, atau Kecamatan...`), indikator `Sinkron Server Bapenda Aktif` (titik hijau berdenyut) + jam WIB, lonceng notifikasi dengan titik merah, tombol `Perbarui Data` (navy).

### 11.4 Isi Dashboard
1. Banner dasar hukum (`border-l-4 border-primary`, ikon `gavel`) + tag `Survei Lapangan 2026`.
2. **6 KPI** (`grid xl:grid-cols-6`): Total Wajib Pajak, Potensi PAD (Est), Terverifikasi (bar progres), Menunggu Verifikasi, Perlu Perbaikan, Draft/Belum Lengkap. Setiap kartu: label uppercase `text-label-sm text-outline`, ikon kotak `w-8 h-8 rounded-lg` berwarna tema, angka `text-headline-md font-bold`, baris keterangan. Warna angka mengikuti status (emerald-700, amber-700, rose-700, slate-700).
3. **Peta + panel kanan** (`lg:grid-cols-12`): peta 8 kolom (`h-[460px]`, header dengan chip kecamatan, kontrol kiri-atas, legenda kanan-bawah, indikator koordinat, bar metadata bawah `Total 17 Kecamatan • 256 Desa / Kelurahan Terdata • Tingkat Akurasi Geolokasi: 98.2%`); panel 4 kolom berisi **Distribusi Kategori Pajak** (bar horizontal `h-2` per kategori dengan `Rp x M (%)`) dan **Progres Verifikasi Wilayah** (bar `h-1.5`, hijau ≥80 %, biru 60–79 %, amber <60 %).
4. **Tabel Antrean Verifikasi**: toolbar (`Filter Status`, `Ekspor XLS / GeoJSON`, `Tambah Objek Baru`), tabel dengan kolom NOP/ID Objek · Nama Usaha/Wajib Pajak · Kecamatan & Alamat · Kategori Pajak · Estimasi Potensi (rata kanan, `font-mono font-bold`) · Status Verifikasi (pil) · Aksi Administrasi (ikon + tombol teks). Header `bg-surface-container-low text-[11px] font-bold uppercase text-outline`. Baris `hover:bg-surface-container-low`, baris Perlu Perbaikan diberi `bg-rose-50/20` dan catatan merah kecil. Paginasi `Menampilkan 1 - 4 dari 1.840 antrean verifikasi`.
5. Callout `Ketentuan & Disclaimer Hukum:` (disclaimer wajib + penjelasan metode analitik geospasial).
6. Footer desktop: nama aplikasi • Kabupaten • Universitas | copyright | `Kebijakan Privasi`, `Dokumentasi GIS`, `Bantuan SIPD`.

### 11.5 Peta Persebaran GIS (desktop fullscreen)
- Header navy dengan navigasi horizontal atas (Beranda, Data Usaha, **Peta** aktif dengan titik, Profil) + sidebar `w-64`.
- Toolbar melayang `bg-surface-container-lowest/95 backdrop-blur-md rounded-xl`: breadcrumb, pencarian, select jenis pajak, tombol `Lapisan Layer`, `Heatmap Potensi`, `Ekspor GeoJSON`, `Cetak Peta`, `Tutup Fullscreen` (navy).
- Bar chip: grup `Kec:` (dengan jumlah) dan grup `Status:` (empat chip status resmi).
- Kanvas `gis-topo-pattern` + grid 80 px, poligon batas kecamatan (`#0051d5` putus-putus, opacity rendah), klaster `+420`, pin status, objek terpilih dengan `animate-ping` dan tooltip navy bersegitiga.
- Panel inspektur kanan `w-96 absolute top-20 right-4 bottom-5 rounded-xl shadow-2xl`: tab `Detail Objek Terpilih` / `Statistik Wilayah`; foto objek + lencana status + `3 Foto Lapangan`; kategori & ID objek; NOP dengan tombol salin; lokasi & akurasi GPS; parameter operasional (Kapasitas, Tarif PBJT, Okupansi); kotak simulasi potensi bulanan; catatan surveyor; ringkasan viewport; kutipan disclaimer; aksi `Verifikasi Sekarang`, `Edit Data`, `Google Maps`.
- Legenda kiri-bawah `w-72` dengan versi `Bapenda GIS v2.4` dan baris kursor `Zoom: 14x`.

---

## 12. Peta Simulasi (tanpa library peta)

Prototipe tidak memuat Leaflet; peta disimulasikan dengan SVG + div absolut. Aturan:
- Posisi marker memakai persentase (`top-[44%] left-[46%]` + `-translate-x-1/2 -translate-y-1/2`), jangan koordinat piksel.
- Selalu sertakan atribusi kecil pada peta mini: `OpenStreetMap contributors | Bapenda Spatial Engine 2026`.
- Hanya satu objek "terpilih" per layar (lebih besar, berdenyut, bertooltip).
- Jangan memakai warna di luar palet peta: biru laut pucat, abu-slate grid, oranye jalan, hijau kawasan lindung.

---

## 13. Alur Kerja Saat Membuat Layar Baru

1. Tentukan permukaan (mobile petugas vs web admin) dan tab/menu aktif.
2. Mulai dari head standar (bagian 2) dan salin konfigurasi Tailwind (bagian 3) tanpa modifikasi.
3. Susun: header → (banner/logo) → konten berseksi → callout disclaimer (jika ada angka pajak) → footer wajib → bottom nav / sidebar.
4. Pakai data contoh bagian 5 agar konsisten; gunakan chip status & tombol aksi sesuai tabel bagian 4.
5. Tambahkan interaksi ringan hanya bila perlu (ganti chip aktif, tutup modal, `alert` konfirmasi pengiriman, jam real-time `id-ID`). Tanpa framework tambahan.
6. Periksa daftar centang:
   - [ ] Disclaimer persis + footer copyright persis + tiga tautan footer
   - [ ] Dua logo dengan `alt` benar
   - [ ] Hanya empat status, warna & label sesuai tabel
   - [ ] Bottom nav 4 tab dengan tab aktif tepat (mobile) / sidebar dengan item aktif (admin)
   - [ ] Rupiah berformat titik, WIB pada jam, koordinat `° S/° E`
   - [ ] `pb-24` (mobile berbottom-nav fixed) agar konten tidak tertutup
   - [ ] Semua teks UI berbahasa Indonesia

---

## 14. Larangan

- Jangan mengganti navy `#0B2A5B` dengan warna lain (hijau, ungu, dsb.) — skill ini **bukan** tema hijau; untuk aplikasi serupa bertema hijau zamrud gunakan skill `natartax-design`.
- Jangan menulis angka potensi sebagai "tagihan", "ketetapan", atau "wajib bayar"; selalu diposisikan sebagai **estimasi simulasi**.
- Jangan menambah status, ikon status, atau warna status baru.
- Jangan memakai font selain Plus Jakarta Sans (angka & NOP boleh `font-mono` di tabel/detail).
- Jangan menghilangkan footer hak cipta atau mengubah teksnya.
- Jangan menampilkan data pribadi nyata (NIK/NPWPD asli); gunakan placeholder seperti `180104xxxxxxxxxx`.
