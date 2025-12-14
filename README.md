# FP-PWEB

| Name           | NRP        | Jobdesk    |
| ---            | ---        | ----------|
| Dwinanda Rakhish Baley | 5025241198 | Frontend |
| Bima Novrifa Ananditya | 5025241194 | Frontend |
| Brilian Kurniawan Prasisto | 5025241213 | Backend : Pembuatan Tabel SQL, API (Payment Gateway), Page Admin Panel, Integrasi dari Backend/Database ke Frontend|

## 1. Frontend & Backend Develelopment

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

### B. Backend Development
1. Arsitektur & Teknologi
   Bahasa Pemrograman : PHP.
   Database : MySQL
   Server Environment : Pada tahap pengembangan menggunakan *Apache*. Saat sudah final, hosting menggunakan infinityfree
2. Konfigurasi `koneksi.php`
   Di tahap ini, kami membuat file khusus untuk menghubungkan semua file ke database, yaitu file `koneksi.php`. Pendekatan ini digunakan agar penulisan kode pada setiap file lebih rapih.
   Adapun variabel-variabel yang digunakan di file `koneksi.php` adalah : 
   a. `$host` (Database Host/Server) : Alamat (IP Address atau Domain) di mana server database MySQL berjalan.
   b. `$user` (Database Username) : Nama pengguna yang memiliki hak akses untuk masuk ke server database.
   c. `$pass` (Database Password) : Kata sandi yang berpasangan dengan username di atas.
   d. `$db` (Database Name) : Nama spesifik dari database yang ingin kita kelola.
3. Implementasi Logika Bisnis : 
   a. Sistem Autentikasi (Login Session) :
   b. Manajemen Konten (CRUD & File Handling) :
       Create: Bagaimana admin menambah menu baru dan logika upload gambar (move_uploaded_file) ke folder uploads/.
       Read: Mengambil data dari database (SELECT * FROM...) dan menampilkannya (Looping while).
       Update/Delete: Bagaimana admin mengedit atau menghapus data berdasarkan ID (WHERE id = ...).
   c. Integrasi Payment Gateway (API Logic)
       File: process_payment.php.
       Alur:
       1. Menerima data JSON dari Frontend (file_get_contents('php://input')).
       2. Menyimpan order ke database dengan status 'pending'.
       3. Menyiapkan parameter request (Gross Amount, Customer Details).
       4. Mengirim request ke Server Midtrans menggunakan cURL.
       5. Menerima balasan berupa Snap Token.
       6. Mengirim Token kembali ke Frontend untuk memicu popup pembayaran.
   d. Logika Bisnis Tambahan (Franchise & Cabang)
       Data ditangkap dengan $_POST, disanitasi (dibersihkan), lalu disimpan ke tabel franchise_leads agar bisa direview admin.
   
## 2. Database Implementation
  A. Environment : 
      DBMS (Database Management System): MySQL / MariaDB.
      Tools Manajemen: phpMyAdmin (melalui CPanel InfinityFree).
      Nama Database: if0_40628472_tetra (Sesuaikan dengan nama DB hostingmu).
      
  B. Struktur Tabel : 
      Website ini terdiri dari 5 tabel utama yang saling mendukung operasional sistem. Berikut adalah detail struktur masing-masing tabel:
      <img width="1989" height="650" alt="image" src="https://github.com/user-attachments/assets/eb43bc70-c8f9-4dd4-a2f8-76be11b59c73" />
      
   a. Tabel `Admins` :  Digunakan untuk menyimpan kredensial autentikasi administrator. Password disimpan dalam bentuk hash (MD5) untuk keamanan.
          <img width="1920" height="450" alt="image" src="https://github.com/user-attachments/assets/7af3cdc1-9452-4670-89d2-2c90367ae94d" />
      
   b. Tabel `products` : Menyimpan seluruh katalog menu yang dijual, termasuk jalur (path) lokasi file gambar yang diunggah.
          <img width="1965" height="668" alt="image" src="https://github.com/user-attachments/assets/8a5623b0-2cb8-4522-90dc-f5eafb59405d" />
    
   c.  Tabel `orders` : Tabel transaksional yang mencatat setiap pesanan masuk, nilai transaksi, dan token integrasi dengan Payment Gateway.
          <img width="2384" height="777" alt="image" src="https://github.com/user-attachments/assets/bf6fc497-9705-4e8e-994f-b010cda19ad0" />
       
   d. Tabel `franchise_leads` Menyimpan data prospek atau calon mitra yang mengisi formulir pendaftaran di website.
          <img width="2479" height="689" alt="image" src="https://github.com/user-attachments/assets/a2e6de0a-1186-4d9f-b3a6-3b5d8f0317c9" />
       
   e. Tabel `branches` Menyimpan data lokasi fisik cabang Tetra Coffee untuk fitur Store Locator.
          <img width="1994" height="583" alt="image" src="https://github.com/user-attachments/assets/8e735640-81e6-4cde-8d86-8cddc08f1bac" />

      C. Query Pembentukan Database
         ```
        -- Implementasi Tabel Transaksi
        CREATE TABLE orders (
          id INT AUTO_INCREMENT PRIMARY KEY,
          order_id VARCHAR(50) NOT NULL UNIQUE,
          customer_name VARCHAR(100),
          total_amount INT NOT NULL, 
          status ENUM('pending', 'success', 'failed') DEFAULT 'pending',
          snap_token VARCHAR(255),
          created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
          );
          
          -- Implementasi Tabel Franchise
          CREATE TABLE franchise_leads (
            id INT AUTO_INCREMENT PRIMARY KEY,
            fullname VARCHAR(100) NOT NULL,
            phone VARCHAR(20) NOT NULL,
            city VARCHAR(50) NOT NULL,
            budget_range ENUM('Dibawah 100jt', '100jt - 250jt', 'Diatas 250jt'),
            status ENUM('pending', 'contacted') DEFAULT 'pending'
            );
        ```


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

