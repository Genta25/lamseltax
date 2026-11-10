# Lamsel Tax Mapping

## Product Requirements Document (PRD)

**Versi:** 1.0\
**Tahun:** 2026\
**Domain:** Smart City -- Smart Economy\
**Cakupan:** Seluruh Kabupaten Lampung Selatan\
**Platform:** Web dan Mobile\
**Jenis data:** Data simulasi dan/atau data publik untuk demonstrasi dan
penelitian

## 1. Ringkasan Produk

Lamsel Tax Mapping adalah aplikasi web dan mobile untuk mendata,
memetakan, memantau, dan menganalisis potensi pajak daerah berdasarkan
aktivitas usaha di Kabupaten Lampung Selatan. Aplikasi menyediakan
pengelolaan data usaha, peta digital, proses verifikasi, estimasi
potensi pajak, dashboard, serta laporan.

Aplikasi ini merupakan prototipe Smart City bidang Smart Economy, bukan
sistem resmi Pemerintah Kabupaten Lampung Selatan. Aplikasi tidak
menetapkan pajak terutang, menerbitkan tagihan, atau memproses
pembayaran pajak.

## 2. Latar Belakang

Pendataan potensi pajak daerah membutuhkan informasi mengenai jenis
usaha, lokasi, kategori usaha, dan data pendukung. Data yang tersusun
dan terpetakan dapat membantu pengguna memahami persebaran aktivitas
ekonomi serta melihat gambaran potensi pajak berdasarkan wilayah.

Lamsel Tax Mapping menyajikan informasi tersebut melalui tabel, peta
digital, dashboard, dan laporan sehingga data dapat dipantau dan
dianalisis secara lebih terstruktur.

## 3. Tujuan Produk

1.  Mendata usaha di seluruh wilayah Kabupaten Lampung Selatan.
2.  Memetakan persebaran lokasi usaha.
3.  Mengelompokkan usaha berdasarkan kategori usaha dan kategori pajak
    yang relevan.
4.  Menghasilkan estimasi potensi pajak berdasarkan parameter simulasi.
5.  Mendukung pemeriksaan dan verifikasi data.
6.  Menyediakan dashboard dan laporan untuk analisis potensi ekonomi
    daerah.
7.  Mendukung pendataan lapangan melalui perangkat mobile.

## 4. Sasaran Pengguna dan Hak Akses

### Admin

-   Mengelola akun dan hak akses pengguna.
-   Mengelola data wilayah, kategori usaha, kategori pajak, dan
    parameter estimasi.
-   Melihat seluruh data serta riwayat aktivitas.

### Petugas Pendataan

-   Menambahkan dan memperbarui data usaha sesuai kewenangan.
-   Mengunggah foto usaha.
-   Mencatat koordinat lokasi.
-   Memantau status pendataan.

### Petugas Verifikasi

-   Memeriksa informasi, foto, dan lokasi usaha.
-   Menyetujui data atau meminta perbaikan.
-   Memberikan catatan hasil pemeriksaan.

### Pimpinan

-   Melihat dashboard dan ringkasan potensi pajak.
-   Melihat peta persebaran usaha.
-   Melihat dan mengunduh laporan.

## 5. Cakupan Fitur

### 5.1 Must-Have

1.  Autentikasi pengguna.
2.  Hak akses berdasarkan peran (RBAC).
3.  Dashboard ringkasan.
4.  Pengelolaan kecamatan dan desa/kelurahan.
5.  Pengelolaan kategori usaha dan kategori pajak.
6.  Pendataan dan pengelolaan data usaha.
7.  Pencatatan koordinat lokasi.
8.  Peta Leaflet.js dengan OpenStreetMap.
9.  Verifikasi data usaha.
10. Estimasi potensi pajak berdasarkan parameter simulasi.
11. Laporan dan ekspor data.
12. Riwayat aktivitas.
13. Aplikasi mobile untuk pendataan lapangan.

### 5.2 Nice-to-Have

-   Filter dan pencarian lanjutan pada peta.
-   Unggah beberapa foto per usaha.
-   Grafik tren pendataan.
-   Notifikasi status verifikasi.
-   Analisis perbandingan potensi antarwilayah.
-   Analisis spasial menggunakan PostGIS.
-   Impor data CSV atau Excel.

## 6. Platform dan Teknologi

  Komponen              Teknologi
  --------------------- ----------------------------
  Web frontend          React.js + TypeScript
  Mobile frontend       Flutter
  Backend               Rust
  Framework backend     Axum
  Database              PostgreSQL
  Akses database        SQLx
  API                   REST API
  Autentikasi           JWT dan refresh token
  Peta                  Leaflet.js + OpenStreetMap
  Grafik                Chart.js atau Recharts
  Analisis geospasial   PostGIS (opsional)

Web dan mobile menggunakan backend serta database yang sama melalui REST
API. PostGIS tidak wajib untuk MVP; koordinat dasar dapat disimpan
sebagai data numerik PostgreSQL.

## 7. Struktur Navigasi

### Web

-   Dashboard
-   Data Usaha
-   Peta Persebaran
-   Kategori Pajak
-   Estimasi Pajak
-   Verifikasi Data
-   Laporan
-   Manajemen Pengguna
-   Data Wilayah
-   Riwayat Aktivitas
-   Pengaturan

Menu yang tampil menyesuaikan peran pengguna.

### Mobile

Navigasi utama: Beranda, Data Usaha, Peta, dan Profil. Fitur mobile
diprioritaskan untuk pendataan lapangan, pengambilan foto, pencatatan
GPS, dan pemeriksaan status data.

## 8. Kebutuhan Fungsional

### 8.1 Autentikasi dan Hak Akses

-   Pengguna masuk menggunakan email/username dan kata sandi.
-   Sistem memvalidasi kredensial.
-   Sistem menerapkan RBAC pada sisi backend.
-   Admin dapat membuat, mengubah, menonaktifkan, dan mengelola akun.
-   Pengguna hanya dapat mengakses fitur sesuai perannya.
-   Sistem menyediakan logout dan mekanisme refresh token.

### 8.2 Dashboard

Dashboard menampilkan: - Jumlah seluruh data usaha. - Jumlah data
menunggu verifikasi. - Jumlah data terverifikasi. - Jumlah data perlu
perbaikan. - Estimasi total potensi pajak berdasarkan data simulasi. -
Grafik usaha berdasarkan kategori. - Grafik persebaran usaha berdasarkan
kecamatan. - Peta ringkas lokasi usaha.

Seluruh angka harus berasal dari data tersimpan dan mengikuti filter
yang diterapkan.

### 8.3 Pengelolaan Data Usaha

Pengguna berwenang dapat melihat, menambah, melihat detail, mengubah,
dan menonaktifkan data usaha serta melakukan pencarian dan filter.

Data minimum usaha: - ID usaha dari sistem. - Nama usaha. - Nama
pemilik/penanggung jawab (bila tersedia). - Kategori usaha. - Alamat
atau deskripsi lokasi. - Kecamatan dan desa/kelurahan. - Latitude dan
longitude. - Nomor kontak (opsional). - Status operasional. - Foto
usaha. - Status verifikasi. - Tanggal pendataan. - Petugas pendata.

Sistem memvalidasi data wajib, rentang koordinat, dan potensi duplikasi
data.

### 8.4 Data Wilayah

-   Admin mengelola kecamatan dan desa/kelurahan.
-   Setiap desa/kelurahan terhubung dengan kecamatan.
-   Data usaha terhubung dengan wilayah yang valid.
-   Sistem menyediakan filter wilayah.

### 8.5 Kategori Usaha dan Kategori Pajak

-   Admin dapat menambah, mengubah, dan menonaktifkan kategori usaha
    serta kategori pajak.
-   Kategori digunakan untuk pencarian, filter, pemetaan, dan laporan.
-   Hubungan antara usaha dan kategori pajak harus mengikuti ketentuan
    peraturan yang relevan.
-   Kategori pajak menyimpan nama, deskripsi, catatan dasar aturan, dan
    status aktif.

Tidak semua usaha otomatis merupakan objek pajak. Pemetaan tidak boleh
hanya didasarkan pada nama kategori usaha.

### 8.6 Peta Persebaran

-   Menampilkan usaha dengan koordinat valid pada peta Leaflet.
-   Menggunakan OpenStreetMap sebagai peta dasar.
-   Marker dapat dipilih untuk melihat ringkasan usaha.
-   Filter berdasarkan kecamatan, desa, kategori usaha, kategori pajak,
    dan status verifikasi.
-   Menyediakan pencarian usaha/wilayah dan legenda marker.
-   Untuk jumlah marker besar, gunakan clustering atau pemuatan
    bertahap.

### 8.7 Verifikasi Data

Alur: 1. Petugas pendataan menyimpan data. 2. Data berstatus Menunggu
Verifikasi. 3. Petugas verifikasi memeriksa data, foto, dan lokasi. 4.
Petugas menyetujui atau meminta perbaikan. 5. Petugas pendataan
memperbaiki data jika diperlukan. 6. Data dapat diajukan kembali.

Status minimal: Draft, Menunggu Verifikasi, Terverifikasi, dan Perlu
Perbaikan.

Setiap keputusan menyimpan pemeriksa, waktu, status, dan catatan.

### 8.8 Estimasi Potensi Pajak

-   Estimasi dihitung berdasarkan kategori pajak dan parameter simulasi.
-   Parameter dapat mencakup tarif, dasar perhitungan, periode, dan
    asumsi.
-   Admin mengelola parameter.
-   Hasil estimasi menampilkan dasar/asumsi perhitungan.
-   Riwayat estimasi disimpan agar perubahan parameter dapat ditelusuri.
-   Perhitungan hanya dilakukan untuk data yang memenuhi aturan pemetaan
    dan kelengkapan.

Rumus harus disesuaikan dengan karakteristik masing-masing kategori
pajak. Tarif dan dasar pengenaan wajib divalidasi terhadap peraturan
yang berlaku sebelum menggunakan data nyata.

**Penting:** estimasi bukan penetapan pajak resmi, tagihan, bukti
pembayaran, atau keputusan hukum. PBB-P2 dan BPHTB memiliki kebutuhan
data objek tersendiri dan tidak boleh dipaksakan ke model data usaha
umum tanpa rancangan khusus.

### 8.9 Laporan dan Ekspor

Laporan mencakup: - Data usaha berdasarkan kecamatan. - Data usaha
berdasarkan desa/kelurahan. - Data usaha berdasarkan kategori. - Rekap
status verifikasi. - Rekap estimasi potensi pajak. - Rekap berdasarkan
periode.

Laporan dapat difilter dan diekspor minimal ke CSV atau Excel. Hak
ekspor mengikuti peran pengguna.

### 8.10 Riwayat Aktivitas

Sistem mencatat login/logout, penambahan dan perubahan data,
penghapusan/penonaktifan, perubahan verifikasi, perubahan parameter,
serta ekspor laporan. Log mencakup pengguna, aktivitas, waktu, dan objek
yang terdampak. Informasi sensitif tidak dicatat secara berlebihan.

### 8.11 Fitur Mobile

-   Login dan dashboard sesuai peran.
-   Menambahkan dan memperbarui data usaha.
-   Mengambil/mengunggah foto.
-   Mengambil koordinat GPS dengan izin perangkat.
-   Melihat lokasi usaha pada peta.
-   Melihat status verifikasi.

Aplikasi menampilkan pesan yang jelas jika izin kamera/lokasi belum
diberikan atau koordinat tidak tersedia.

## 9. Rancangan Database Awal

  -----------------------------------------------------------------------
  Tabel                               Fungsi
  ----------------------------------- -----------------------------------
  `users`                             Akun pengguna

  `roles`                             Daftar peran

  `user_roles`                        Relasi pengguna dan peran

  `kecamatan`                         Data kecamatan

  `desa`                              Data desa/kelurahan

  `business_categories`               Kategori usaha

  `businesses`                        Data usaha dan koordinat

  `tax_categories`                    Kategori pajak

  `business_tax_mappings`             Pemetaan usaha/kategori usaha ke
                                      kategori pajak

  `tax_parameters`                    Parameter estimasi

  `tax_estimations`                   Hasil estimasi

  `verifications`                     Riwayat verifikasi

  `business_photos`                   Metadata foto usaha

  `activity_logs`                     Riwayat aktivitas
  -----------------------------------------------------------------------

Relasi utama: - Satu kecamatan memiliki banyak desa. - Satu desa
memiliki banyak usaha. - Satu kategori usaha dapat digunakan banyak
usaha. - Satu usaha dapat memiliki banyak foto dan riwayat verifikasi. -
Pemetaan pajak menghubungkan usaha/kategori usaha dengan kategori
pajak. - Estimasi terhubung dengan usaha, kategori pajak, dan parameter
yang digunakan. - Pengguna dapat memiliki beberapa peran.

Detail kolom, tipe data, indeks, constraint, dan foreign key ditentukan
pada tahap desain database teknis.

## 10. Kebutuhan Nonfungsional

### Keamanan

-   Kata sandi disimpan dalam bentuk hash.
-   Endpoint terlindungi memvalidasi token.
-   Pemeriksaan hak akses dilakukan di backend.
-   Validasi input dilakukan di frontend dan backend.
-   Query database menggunakan parameterisasi SQLx.
-   Produksi menggunakan HTTPS.
-   File unggahan divalidasi tipe dan ukurannya.
-   Rahasia aplikasi disimpan dalam environment variables.
-   Aktivitas penting dicatat dalam audit log.

### Kinerja

-   Daftar data menggunakan pagination.
-   Pencarian dan filter dioptimalkan.
-   Query dashboard tidak memuat data berlebihan.
-   Peta menggunakan clustering/pemuatan bertahap jika diperlukan.

### Kemudahan Penggunaan

-   Bahasa antarmuka Bahasa Indonesia.
-   Navigasi konsisten dan responsif.
-   Form memiliki label serta pesan validasi yang jelas.
-   Status menggunakan label dan warna yang konsisten.

### Keandalan dan Pemeliharaan

-   Kode web, mobile, backend, dan database terstruktur.
-   API memiliki format respons dan error yang konsisten.
-   Database memiliki backup.
-   Perubahan skema dikelola melalui migration.
-   Tersedia dokumentasi instalasi dan konfigurasi.

## 11. Struktur Backend Rust yang Disarankan

``` text
backend/
├── Cargo.toml
├── .env.example
├── migrations/
└── src/
    ├── main.rs
    ├── config/
    ├── db/
    ├── middleware/
    ├── routes/
    ├── handlers/
    ├── models/
    ├── services/
    ├── repositories/
    ├── validators/
    └── utils/
```

-   `config`: konfigurasi aplikasi.
-   `db`: koneksi PostgreSQL.
-   `middleware`: autentikasi dan pemeriksaan hak akses.
-   `routes`: definisi endpoint.
-   `handlers`: pemrosesan request/response.
-   `models`: struktur data.
-   `services`: logika bisnis.
-   `repositories`: akses database.
-   `validators`: validasi input.
-   `utils`: fungsi pendukung.

## 12. Gambaran REST API

  -----------------------------------------------------------------------------
  Modul                               Contoh endpoint
  ----------------------------------- -----------------------------------------
  Auth                                `POST /api/auth/login`,
                                      `POST /api/auth/refresh`,
                                      `POST /api/auth/logout`

  Dashboard                           `GET /api/dashboard/summary`

  Users                               `GET /api/users`, `POST /api/users`

  Wilayah                             `GET /api/kecamatan`, `GET /api/desa`

  Kategori usaha                      `GET /api/business-categories`

  Usaha                               `GET /api/businesses`,
                                      `POST /api/businesses`,
                                      `GET /api/businesses/{id}`,
                                      `PUT /api/businesses/{id}`

  Peta                                `GET /api/map/businesses`

  Kategori pajak                      `GET /api/tax-categories`

  Estimasi                            `GET /api/tax-estimations`,
                                      `POST /api/tax-estimations/calculate`

  Verifikasi                          `GET /api/verifications`,
                                      `POST /api/verifications/{id}/decision`

  Laporan                             `GET /api/reports/businesses`,
                                      `GET /api/reports/tax-potential`

  Aktivitas                           `GET /api/activity-logs`
  -----------------------------------------------------------------------------

Endpoint merupakan rancangan awal dan harus disesuaikan dengan hak akses
serta kebutuhan implementasi.

## 13. Identitas Visual dan Antarmuka

### Konsep Desain

-   Profesional, bersih, modern, dan mudah digunakan.
-   Warna utama navy blue.
-   Warna pendukung biru, putih, dan abu-abu.
-   Hijau untuk terverifikasi.
-   Kuning untuk menunggu verifikasi.
-   Merah untuk perlu perbaikan/peringatan.

### Halaman Login

-   Nama aplikasi Lamsel Tax Mapping.
-   Area logo Pemerintah Kabupaten Lampung Selatan.
-   Area logo Universitas Teknokrat Indonesia.
-   Form email/username dan kata sandi.
-   Tombol masuk.
-   Footer proyek.

Sebelum file logo resmi tersedia, gunakan placeholder. Jangan membuat
ulang atau mengklaim logo tidak resmi sebagai logo resmi.

### Dashboard

-   Sidebar navigasi.
-   Kartu ringkasan data usaha dan status verifikasi.
-   Ringkasan estimasi potensi pajak.
-   Grafik berdasarkan kategori dan kecamatan.
-   Peta ringkas persebaran usaha.

### Data Usaha

-   Tabel data, pencarian, filter, dan tombol tambah.
-   Aksi detail, ubah, serta hapus/nonaktifkan sesuai hak akses.

### Peta

-   Peta interaktif, marker lokasi, filter wilayah/kategori/status, dan
    popup ringkasan.

### Verifikasi

-   Daftar data menunggu pemeriksaan.
-   Detail usaha, foto, dan lokasi.
-   Aksi setujui atau minta perbaikan.
-   Catatan verifikasi.

### Mobile

-   Antarmuka sederhana dan responsif.
-   Form pendataan lapangan.
-   Integrasi kamera dan GPS.
-   Navigasi bawah: Beranda, Data Usaha, Peta, Profil.

## 14. Footer dan Logo

Teks footer harus ditampilkan persis:

**Copyright©2026 by Genta dan Dr. Erliyan Redy Susanto, M.Kom**

Logo yang direncanakan: 1. Logo Pemerintah Kabupaten Lampung Selatan. 2.
Logo Universitas Teknokrat Indonesia.

File logo akan ditambahkan atau diganti sendiri oleh pengguna pada tahap
implementasi. Penggunaan logo pada prototipe tidak berarti aplikasi
telah diadopsi, disahkan, atau didukung secara resmi oleh instansi
terkait.

## 15. Batasan dan Asumsi

-   Cakupan wilayah seluruh Kabupaten Lampung Selatan.
-   Data awal berupa data simulasi dan/atau data publik yang sesuai.
-   Aplikasi adalah prototipe demonstrasi/penelitian, bukan sistem resmi
    pemerintah.
-   Aplikasi tidak memproses pembayaran atau menerbitkan tagihan pajak.
-   Estimasi berdasarkan parameter dan asumsi yang ditampilkan.
-   Kategori dan tarif pajak harus mengacu pada peraturan yang berlaku
    jika menggunakan data nyata.
-   Sinkronisasi API dan pemuatan peta daring membutuhkan internet.
-   Integrasi dengan sistem resmi pemerintah tidak termasuk cakupan
    awal.

## 16. Kriteria Keberhasilan MVP

1.  Pengguna dapat login sesuai perannya.
2.  Admin dapat mengelola pengguna, wilayah, kategori, dan parameter.
3.  Petugas dapat menambah serta memperbarui data usaha.
4.  Data usaha tampil pada daftar dan peta.
5.  Petugas verifikasi dapat menyetujui atau meminta perbaikan.
6.  Sistem menghasilkan estimasi berdasarkan parameter simulasi.
7.  Dashboard menampilkan ringkasan yang sesuai dengan data.
8.  Laporan dapat difilter dan diekspor.
9.  Aktivitas penting tercatat.
10. Aplikasi mobile dapat mengakses API dan mendukung pendataan.
11. Pengguna tidak dapat mengakses data/fitur di luar hak aksesnya.

## 17. Tahapan Pengembangan

### Tahap 1 -- Persiapan

Finalisasi kebutuhan, repository, lingkungan pengembangan, rancangan
database, dan desain antarmuka.

### Tahap 2 -- Backend

Membuat proyek Rust/Axum, koneksi PostgreSQL dengan SQLx, migration,
model, autentikasi, RBAC, serta API wilayah, kategori, dan usaha.

### Tahap 3 -- Web

Membuat login, dashboard, pengelolaan usaha, peta Leaflet, verifikasi,
estimasi, dan laporan.

### Tahap 4 -- Mobile

Membuat aplikasi Flutter, menghubungkannya ke REST API, serta
mengembangkan pendataan, kamera, GPS, dan peta.

### Tahap 5 -- Pengujian

Melakukan pengujian fungsional, hak akses, validasi, perhitungan
estimasi, tampilan responsif, perbaikan bug, dan dokumentasi.

## 18. Hal yang Perlu Dikonfirmasi Saat Implementasi

1.  Daftar kategori pajak dan pemetaan jenis usaha sesuai peraturan
    Kabupaten Lampung Selatan yang berlaku.
2.  Rumus dan parameter estimasi setiap kategori pajak.
3.  Sumber data wilayah kecamatan dan desa/kelurahan.
4.  Apakah foto usaha wajib untuk seluruh kategori.
5.  Format final laporan dan kolom ekspor.
6.  Kebutuhan PostGIS untuk analisis spasial.
7.  Kebijakan retensi data, backup, dan pengelolaan akun.

------------------------------------------------------------------------

**Akhir Dokumen PRD -- Lamsel Tax Mapping**
