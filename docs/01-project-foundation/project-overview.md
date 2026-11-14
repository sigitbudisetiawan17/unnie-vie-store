# PROJECT OVERVIEW
## Unnie Vie Store
### Integrated E-Commerce, Store Management, and CRM System

**Status:** Draft untuk ditinjau  
**Versi:** 0.1  
**Tanggal:** 14 November 2026

## 1. Gambaran Umum Proyek

Unnie Vie Store merupakan usaha toko tas wanita yang berlokasi di Jl. Ali Syahbana Mutiara, Kisaran, Kabupaten Asahan, Sumatera Utara. Toko ini menyediakan berbagai pilihan tas, mulai dari produk impor, produk lokal premium, hingga produk lokal dengan harga terjangkau.

Dalam menjalankan kegiatan bisnisnya, Unnie Vie Store memanfaatkan beberapa saluran penjualan, seperti Facebook, Instagram, TikTok, WhatsApp, toko fisik, dan website.

Seiring berkembangnya kegiatan penjualan, kebutuhan terhadap pengelolaan data yang terpusat menjadi semakin penting. Pencatatan produk, stok, transaksi, dan pelanggan yang masih dilakukan secara manual berpotensi menimbulkan ketidaksesuaian data serta menyulitkan pemilik dalam memantau kondisi bisnis.

Oleh karena itu, dikembangkan sebuah sistem terintegrasi bernama **Unnie Vie Store — Integrated E-Commerce, Store Management, and CRM System**. Sistem ini dirancang untuk menggabungkan layanan e-commerce pelanggan dengan pengelolaan operasional toko dan Customer Relationship Management (CRM) dalam satu ekosistem.

## 2. Latar Belakang Permasalahan

Beberapa permasalahan yang menjadi dasar pengembangan sistem ini adalah:

1. **Pencatatan stok belum terpusat.** Pengelolaan stok secara manual berisiko menyebabkan perbedaan antara jumlah barang yang tercatat dan kondisi fisik di toko.
2. **Data transaksi tersebar.** Penjualan melalui berbagai saluran membutuhkan pencatatan yang lebih terstruktur agar seluruh transaksi dapat dipantau.
3. **Pengelolaan pelanggan belum terintegrasi.** Riwayat pembelian, informasi pelanggan, dan aktivitas transaksi perlu dikumpulkan agar dapat dimanfaatkan untuk meningkatkan pelayanan.
4. **Pemantauan bisnis membutuhkan proses tambahan.** Pemilik memerlukan informasi penjualan, keuntungan, dan kondisi persediaan yang lebih mudah diakses.
5. **Program loyalitas membutuhkan pengelolaan terstruktur.** Poin, membership, voucher, dan penghargaan pelanggan perlu dikelola secara konsisten.
6. **Pelayanan digital perlu dikembangkan.** Website e-commerce dapat memberikan kemudahan kepada pelanggan untuk melihat produk, melakukan pemesanan, dan memantau transaksi.

## 3. Tujuan Pengembangan

Pengembangan sistem Unnie Vie Store memiliki tujuan sebagai berikut:

- Membangun website e-commerce sebagai sarana penjualan online.
- Memusatkan pengelolaan produk, kategori, varian, dan persediaan.
- Mengintegrasikan pencatatan transaksi online maupun offline.
- Mempermudah pengelolaan pesanan, pembayaran, pengiriman, pembatalan, dan pengembalian barang.
- Menyediakan laporan penjualan dan keuntungan untuk membantu pemilik memantau bisnis.
- Mengembangkan pengelolaan hubungan pelanggan melalui CRM.
- Menerapkan program poin dan membership untuk meningkatkan loyalitas pelanggan.
- Menyediakan pencatatan aktivitas agar perubahan penting dalam sistem dapat ditelusuri.
- Membantu meningkatkan efisiensi operasional dan kualitas pelayanan toko.

## 4. Ruang Lingkup Sistem

Sistem dibagi menjadi tiga bagian utama.

### 4.1 Customer E-Commerce

Bagian ini merupakan website yang digunakan pelanggan untuk berinteraksi dengan Unnie Vie Store.

Fitur utamanya meliputi:
- Halaman utama dan katalog produk.
- Kategori, pencarian, dan filter produk.
- Detail produk dan pilihan varian.
- Keranjang belanja dan checkout.
- Registrasi, login, dan pengelolaan akun.
- Pengelolaan beberapa alamat pengiriman.
- Riwayat pesanan dan status pengiriman.
- Wishlist.
- Poin, membership, dan voucher.
- Ulasan serta rating produk.
- Pusat notifikasi pelanggan.
- Halaman Tentang Kami dan informasi kebijakan toko.
- Tombol komunikasi langsung melalui WhatsApp.

Pelanggan dapat melihat katalog tanpa login, tetapi harus memiliki akun untuk menyelesaikan pembelian.

### 4.2 Admin and Store Management

Bagian ini merupakan dashboard internal yang digunakan pemilik dan staf untuk menjalankan operasional toko.

Fitur utamanya meliputi:
- Dashboard ringkasan bisnis.
- Pengelolaan produk, kategori, dan varian.
- Pengelolaan stok dan riwayat pergerakan barang.
- Stok masuk dan penyesuaian stok.
- Pengelolaan pemasok dan pembelian.
- Pencatatan penjualan online dan offline.
- Pengelolaan pesanan dan pembayaran.
- Pengelolaan pengiriman.
- Pembatalan, retur, penukaran, dan refund.
- Laporan penjualan dan keuntungan.
- Pengelolaan akun staf dan hak akses.
- Activity Log.
- Notifikasi operasional.
- Backup dan pemulihan data.
- Pengelolaan konten website.

### 4.3 Customer Relationship Management (CRM)

Bagian CRM berfungsi membantu toko mengelola informasi pelanggan dan membangun hubungan jangka panjang.

Fitur utamanya meliputi:
- Profil dan informasi pelanggan.
- Riwayat pembelian.
- Informasi total belanja.
- Saldo dan riwayat poin.
- Membership Bronze, Silver, dan Gold.
- Pengelolaan voucher dan reward.
- Segmentasi pelanggan.
- Ulasan dan umpan balik.
- Informasi aktivitas pelanggan.

Ketiga bagian tersebut saling terhubung melalui backend dan database terpusat.

## 5. Pengguna Sistem

Sistem memiliki tiga kelompok pengguna utama.

### 5.1 Pemilik Toko

Pemilik merupakan pengguna dengan hak akses tertinggi. Pemilik dapat mengelola seluruh aktivitas administrasi, memantau laporan, mengatur staf, mengelola promosi, dan melakukan konfigurasi sistem.

### 5.2 Staf

Staf menggunakan dashboard admin sesuai tugas dan tanggung jawabnya. Hak akses diberikan berdasarkan role dan permission, sehingga tidak seluruh staf memiliki akses ke semua fitur.

### 5.3 Pelanggan

Pelanggan menggunakan website publik untuk melihat produk, melakukan pembelian, mengelola akun, memantau pesanan, dan memanfaatkan program loyalitas.

Akun pelanggan terpisah dari akun pemilik dan staf.

## 6. Gambaran Proses Bisnis

Secara umum, sistem mendukung proses bisnis berikut:

1. **Pengelolaan produk:** pemilik atau staf berwenang memasukkan produk, harga, foto, kategori, dan varian.
2. **Pengelolaan persediaan:** stok diperbarui melalui stok masuk, pembelian, penjualan, dan penyesuaian stok.
3. **Pembelian pelanggan:** pelanggan memilih produk, memasukkannya ke keranjang, login, lalu menyelesaikan checkout.
4. **Pemrosesan pesanan:** admin memeriksa pembayaran, memproses barang, dan memperbarui informasi pengiriman.
5. **Penyelesaian transaksi:** pelanggan mengonfirmasi penerimaan barang atau admin menyelesaikan pesanan sesuai prosedur.
6. **Pengelolaan retur:** jika terjadi kerusakan, kecacatan, atau ketidaksesuaian barang, pelanggan dapat mengajukan retur sesuai ketentuan.
7. **Pengelolaan pelanggan:** sistem menyimpan riwayat pembelian, poin, membership, voucher, dan ulasan.
8. **Pemantauan bisnis:** pemilik menggunakan dashboard dan laporan untuk memantau penjualan, keuntungan, serta persediaan.

Selain transaksi online, sistem juga mendukung pencatatan penjualan yang terjadi secara langsung di toko fisik.

## 7. Gambaran Arsitektur Sistem

Sistem menggunakan pendekatan hybrid dengan pemisahan frontend pelanggan dan backend.

- Website pelanggan menggunakan teknologi frontend terpisah yang akan ditentukan pada tahap perencanaan teknis.
- Backend menggunakan Laravel 13 dan PHP 8.5.
- Dashboard admin menggunakan Laravel Blade dan Tailwind CSS.
- Komunikasi antara frontend pelanggan dan backend menggunakan REST API dengan format JSON.
- Database utama menggunakan MySQL.

Backend bertanggung jawab atas validasi, aturan bisnis, autentikasi, otorisasi, serta pengelolaan data. Frontend pelanggan tidak mengakses database secara langsung.

## 8. Pembagian Pengembangan

Proyek dikerjakan oleh dua developer dengan pembagian tanggung jawab sebagai berikut:

**Developer 1 — Backend dan Admin**

Bertanggung jawab atas pengembangan backend Laravel, database, dashboard admin, autentikasi, pengelolaan produk, inventaris, transaksi, laporan, CRM, serta API.

**Developer 2 — Customer Frontend**

Bertanggung jawab atas pengembangan website pelanggan, meliputi halaman utama, katalog, detail produk, keranjang, checkout, profil, pesanan, wishlist, dan fitur pelanggan lainnya.

Kedua developer bekerja dalam satu repository GitHub menggunakan branch terpisah dan Pull Request. Integrasi dilakukan berdasarkan kontrak API yang disepakati bersama.

## 9. Target Hasil Pengembangan

Hasil akhir yang diharapkan dari proyek ini adalah:

1. Website e-commerce yang dapat digunakan pelanggan untuk melakukan pembelian secara online.
2. Dashboard admin yang mempermudah pemilik dan staf mengelola kegiatan operasional.
3. Database terpusat yang menyimpan data produk, stok, transaksi, dan pelanggan.
4. Sistem pencatatan penjualan online dan offline.
5. Sistem laporan yang membantu pemilik memahami kondisi bisnis.
6. Sistem CRM dan loyalitas yang mendukung hubungan jangka panjang dengan pelanggan.
7. Sistem pencatatan aktivitas dan backup untuk mendukung keamanan serta keberlanjutan data.

## 10. Batasan dan Pengembangan Bertahap

Pengembangan awal difokuskan pada fitur yang telah ditetapkan dalam Project Constitution.

Beberapa fitur yang belum menjadi prioritas versi awal antara lain:
- Verifikasi nomor WhatsApp menggunakan OTP.
- Integrasi payment gateway.
- Integrasi API ekspedisi.
- Notifikasi WhatsApp otomatis.
- Live chat internal.
- Notifikasi stok tersedia kembali.
- Pencatatan pengeluaran operasional.

Fitur tersebut dapat dikembangkan pada tahap berikutnya sesuai kebutuhan dan kesiapan sistem.

## 11. Dokumen Acuan

Project Overview ini disusun berdasarkan dokumen **Project Constitution — Unnie Vie Store** yang telah disetujui sebagai pedoman dasar proyek.

Dokumen berikutnya akan menjabarkan kebutuhan sistem, aturan bisnis, arsitektur, rancangan database, spesifikasi fitur, dan pembagian tugas implementasi secara lebih terperinci.

---

**Status dokumen:** Draft untuk ditinjau dan disetujui.

**Catatan:** Project Overview ini menjelaskan gambaran proyek secara umum. Ketentuan operasional yang lebih rinci tetap mengacu pada Project Constitution dan dokumen spesifikasi terkait.