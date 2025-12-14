# FP-PWEB

| Name           | NRP        | Jobdesk    |
| ---            | ---        | ----------|
| Dwinanda Rakhish Baley | 5025241198 | Frontend |
| Bima Novrifa Ananditya | 5025241194 | Frontend |
| Brilian Kurniawan Prasisto | 5025241213 | Backend |

## 1 Frontend & Backend Develelopment

### A. Frontend Development
Frontend dikembangkan sebagai antarmuka utama yang berinteraksi langsung dengan pengguna. Tujuan utama pengembangan frontend adalah menyediakan tampilan yang menarik, responsif, dan mudah digunakan.

Fitur utama frontend meliputi:
- Halaman Home sebagai landing page yang menampilkan informasi singkat Tetra Coffee
- Halaman Menu yang menampilkan daftar produk lengkap dengan kategori, pencarian, dan harga
- Fitur keranjang (cart) untuk menampung menu yang dipilih pengguna
- Halaman Order Online untuk proses pemesanan
- Halaman Franchise yang menyediakan formulir pengajuan mitra
- Halaman Tentang yang memberikan informasi tentang Tetra Coffee
- Halaman Lokasi yang memberikan lokasi dari Cafe Tetra Coffee
- Halaman Kontak yang menyediakan kontak-kontak dari Tetra Coffee

Frontend dirancang dengan pendekatan user-friendly, menggunakan navigasi yang konsisten serta tombol aksi yang jelas seperti Pesan Sekarang, Lihat Menu, Tentang, Lokasi, Franchise, dan Tambah ke Cart.

## 3. Integrasi Layanan Pihak Ketiga (API)
Sistem ini dirancang dengan arsitektur terintegrasi yang menghubungkan backend PHP Native dengan layanan eksternal melalui REST API. Integrasi ini bertujuan untuk menangani fungsi kompleks seperti pembayaran digital dan geolokasi tanpa membebani server utama.

### Midtrans Payment API (Snap)
- Untuk menangani transaksi finansial, sistem menggunakan Midtrans Snap API dalam lingkungan Sandbox (uji coba). Alur integrasi data dirancang sebagai berikut:
- Inisiasi Transaksi (Backend): Ketika pengguna melakukan checkout, sistem backend (order.php) mengumpulkan data pesanan (nama pelanggan, total harga, dan detail item) dari Local Storage.
- Permintaan Token (API Request): Server mengirimkan permintaan HTTP POST ke endpoint API Midtrans (app.sandbox.midtrans.com/snap/v1/transactions) beserta Server Key rahasia untuk otentikasi.
- Respon Token (API Response): Midtrans memvalidasi permintaan dan mengembalikan snap_token unik. Token ini disimpan sementara di database tabel orders untuk pelacakan.
- Tampilan Pembayaran (Frontend): Token dikirim kembali ke browser pengguna. Pustaka Javascript snap.js menggunakan token ini untuk memunculkan antarmuka pembayaran (iframe popup) di atas website tanpa mengalihkan halaman, sehingga pengalaman pengguna (UX) tetap terjaga.

### Google Maps Platform
- Fitur peta pada modul Store Locator menggunakan integrasi berbasis tautan dinamis (Dynamic Linking) untuk efisiensi resource:
- Penyimpanan Data: Koordinat atau tautan spesifik lokasi (contoh: https://goo.gl/maps/...) disimpan dalam tabel branches kolom maps_link.
- Visualisasi Data: Pada halaman locations.php, sistem melakukan query ke database untuk mengambil seluruh data cabang. Tautan tersebut kemudian dirender menjadi tombol navigasi interaktif ("Petunjuk Arah").
- Navigasi Eksternal: Ketika tombol ditekan, API akan mengarahkan pengguna langsung ke aplikasi Google Maps (pada mobile) atau situs web Maps (pada desktop) dengan titik tujuan yang sudah terkunci pada lokasi cabang yang dipilih.






## 4. Testing

### Tujuan Pengujian
Pengujian dilakukan untuk memastikan bahwa seluruh fitur pada sistem berjalan sesuai dengan kebutuhan yang telah didefinisikan. Fokus utamanya adalah memastikan backend dapat berfungsi dengan benar, data tersimpan pada database, dan API berjalan stabil.

### Lingkup Pengujian
- fungsi backend
- interaksi backend dengan database
- integrasi API

### Metode Pengujian
- Unit testing
Bertujuan untuk menguji setiap fungsi dan memastikan bahwa setiap fungsi menghasilkan output yang sesuai dengan input.
- Integration Testing
Bertujuan untuk memasttikan bahwa semuanya saling terhubung dan berkerja dengan baik. Testing ini berfokus pada interaksi backend dengan database dan integrasi API.
- Functional Testing
Menguji setiap fitur dari segi fungsionalitasnya untuk memastikan sistem bekerja sesuai dengan alur pengerjaan.

### Hasil Pengujian
- Seluruh endpoint API dapat diakses dengan hasil response yang sesuai
- data berhasil disimpan, diubah, dan dihapus pada database

## Diagram Sistem

### Order online
<img width="741" height="415" alt="image" src="https://github.com/user-attachments/assets/a9a039f5-c7bb-4894-b1dd-ae6f7d93d46d" />

### Franchise
<img width="748" height="415" alt="image" src="https://github.com/user-attachments/assets/a181fc7f-d95f-4ee9-af23-fea59038b3cf" />

## User Guide
Berikut panduan penggunaan Website kami

1. Home
Pengguna akan diarahkan pada halaman utama. Pada Home terdapat navigation bar yang mempunyai fungsi berbeda-beda.
- Home
Pada `Home` akan menampilkan landing page sebagai halaman utama pada home juga memperlihatkan menu signature dari Tetra Coffee, Informasi singkat mengenai Tetra Coffee, dan lokasi singkat dari Tetra Coffee Surabaya.
- Tentang
Pada `Tentang` berisikan informasi-informasi lebih lengkap tentang Tetra Coffee.
- Menu
Pada `Menu` menampilkan beberapa menu makanan dan juga minuman yang tersedia pada Tetra Coffee. Disini juga bisa untuk menambahkan menu ke cart yang akan di proses pada `Order Online`
- Lokasi
Pada `Lokasi` akan berisikan lokasi dari Tetra Coffee.
- Franchise
Pada `Franchise` akan menampilkan formulir untuk mengajukan franchise kepada pihak Tetra Coffee. Isi dari form yang harus diisi :
  - Nama Lengkap
  - Kota Target
  - WhatsApp
  - Email
  - Modal
  - Alasan
- Kontak
Pada `Kontak` menampilkan contact person dari beberapa sosial media dan juga cabang dari Tetra Coffee.
- Order Online
Pada `Order Online` menampilkan form untuk data pemesan yang berisikan:
  - Nama Lengkap
  - Nomor HP/ WhatsApp
  - Alamat Pengiriman / Meja
  - Catatan Tambahan
Setelah Mengisi form, Pemesan diminta untuk membayar pemasanannya dengan Payment method yang tersedia.
