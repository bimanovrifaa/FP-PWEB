# FP-PWEB

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
