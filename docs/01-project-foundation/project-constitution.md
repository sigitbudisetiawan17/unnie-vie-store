# Project Constitution

## Unnie Vie Store --- Integrated E-Commerce, Store Management, and CRM System

**Status:** Draf untuk ditinjau dan disetujui\
**Versi:** 0.1\
**Tanggal penyusunan:** 14 November 2026

> Dokumen ini merangkum keputusan yang telah disepakati dalam diskusi.
> Bagian yang belum diputuskan ditandai sebagai **Perlu diputuskan**.
> Dokumen ini menjadi dasar bersama sebelum penyusunan spesifikasi
> fitur, desain database, dan implementasi.

------------------------------------------------------------------------

## 1. Visi dan tujuan proyek

Unnie Vie Store adalah toko tas wanita yang berlokasi di Jl. Ali
Syahbana Mutiara, Kisaran, Kabupaten Asahan, Sumatera Utara. Produk yang
dijual meliputi tas impor, tas lokal premium, dan tas lokal terjangkau.

Penjualan saat ini berlangsung melalui Facebook, Instagram, TikTok,
WhatsApp, toko fisik, dan website. Pencatatan stok dan transaksi yang
masih dilakukan secara manual berisiko menimbulkan perbedaan antara
catatan dan kondisi barang sebenarnya.

Sistem ini dibangun untuk mengintegrasikan kegiatan penjualan,
pengelolaan produk dan persediaan, transaksi, laporan, serta pengelolaan
hubungan pelanggan (CRM) ke dalam satu sistem terpusat.

Tujuan utama: - Menyediakan website e-commerce bagi pelanggan. -
Memusatkan data produk, varian, stok, pesanan, dan transaksi. -
Mendukung penjualan online dan offline. - Membantu pemilik memantau
operasional, penjualan, dan keuntungan. - Menyediakan fitur CRM, poin
loyalitas, membership, voucher, dan ulasan. - Menyediakan pencatatan
aktivitas agar perubahan penting dapat ditelusuri.

## 2. Prinsip dasar proyek

1.  **Satu sumber data utama.** MySQL menjadi sumber data terpusat bagi
    sistem.
2.  **Backend mengendalikan aturan bisnis.** Validasi, autentikasi,
    otorisasi, dan proses bisnis dijalankan oleh backend Laravel.
3.  **Frontend pelanggan tidak mengakses database secara langsung.**
    Komunikasi dilakukan melalui REST API berbasis JSON.
4.  **Akses sesuai tanggung jawab.** Pemilik memiliki akses penuh,
    sedangkan staf memperoleh akses berdasarkan role dan permission.
5.  **Riwayat penting harus dapat ditelusuri.** Perubahan stok,
    transaksi, pembayaran, retur, akun, dan aktivitas penting dicatat.
6.  **Spesifikasi mendahului implementasi.** Keputusan bisnis dan
    spesifikasi fitur disepakati sebelum pembuatan tabel, model, atau
    fitur terkait.
7.  **Pengembangan bertahap.** Fitur yang ditunda dicatat agar dapat
    dikembangkan kemudian tanpa mengganggu fitur versi awal.

## 3. Arsitektur dan teknologi

### 3.1 Arsitektur

Sistem menggunakan arsitektur hybrid: - Website pelanggan merupakan
frontend terpisah. - Laravel menjadi backend/API sekaligus dashboard
admin. - Dashboard admin dibangun menggunakan Laravel Blade dan Tailwind
CSS. - Frontend pelanggan berkomunikasi dengan backend melalui REST API
dan JSON. - MySQL menjadi database utama.

Teknologi frontend pelanggan **belum diputuskan**.

### 3.2 Teknologi yang telah ditetapkan

-   Laravel Framework 13.
-   PHP 8.5.
-   MySQL.
-   Laravel Blade dan Tailwind CSS untuk dashboard admin.
-   REST API berbasis JSON untuk integrasi frontend pelanggan.

### 3.3 Aturan arsitektur

-   Frontend pelanggan tidak boleh mengakses database secara langsung.
-   Backend Laravel bertanggung jawab atas validasi, aturan bisnis,
    autentikasi, otorisasi, dan akses database.
-   Kontrak API (endpoint, format request/response, dan autentikasi)
    harus disepakati sebelum integrasi kedua frontend/backend dilakukan.

## 4. Tim dan pembagian tanggung jawab

Proyek dikerjakan oleh dua developer.

### Developer 1 --- Backend dan dashboard admin

Bertanggung jawab atas: - Backend Laravel, database, migration, dan
seeder. - Autentikasi dan otorisasi/role. - Dashboard admin. - Produk,
kategori, varian, dan inventaris. - Pemasok dan pembelian. - Transaksi,
pesanan, pembayaran, dan penjualan offline. - Pengiriman, pembatalan,
retur, dan refund. - Laporan. - CRM, poin, membership, voucher, dan
ulasan. - REST API dan integrasi backend.

### Developer 2 --- Frontend pelanggan

Bertanggung jawab atas: - Halaman Home, katalog, kategori, pencarian,
dan filter. - Detail produk dan pilihan varian. - Keranjang dan
checkout. - Halaman pesanan dan riwayat transaksi. - Profil, alamat,
wishlist, poin, membership, voucher, dan ulasan pada sisi pelanggan. -
Integrasi dengan REST API backend.

### 4.1 Kolaborasi Git

-   Menggunakan satu repository GitHub privat.
-   `main` menjadi branch stabil.
-   Pekerjaan dilakukan pada branch terpisah, misalnya `feature/*` dan
    `fix/*`.
-   Perubahan digabungkan melalui Pull Request.
-   Developer tidak melakukan pekerjaan langsung pada `main`.
-   Kedua developer melakukan sinkronisasi sebelum mulai bekerja.
-   `.env`, `vendor/`, dan `node_modules/` tidak dikomit.
-   `composer.lock` dikomit agar dependensi konsisten.
-   Hindari mengedit file yang sama secara bersamaan tanpa koordinasi.
-   Perubahan ditinjau dan diuji sebelum digabungkan.

## 5. Pengguna, autentikasi, dan hak akses

### 5.1 Jenis pengguna

-   **Pemilik toko:** memiliki akses penuh ke seluruh fungsi
    administrasi.
-   **Staf:** akses dibatasi berdasarkan role dan permission, misalnya
    kasir, inventaris, atau CRM.
-   **Pelanggan:** menggunakan akun pelanggan pada website publik,
    terpisah dari akun admin/staf.

Pelanggan dapat melihat katalog tanpa login, tetapi harus login atau
registrasi sebelum menyelesaikan checkout. Fitur akun seperti riwayat
pesanan, wishlist tersimpan, dan pengelolaan profil memerlukan login.

### 5.2 Akun admin dan staf

-   Pemilik mengelola akun staf melalui dashboard admin.
-   Pemilik dapat membuat, mengubah, memberi atau mengubah
    role/permission, menonaktifkan, dan mengaktifkan kembali akun staf.
-   Staf yang dinonaktifkan tidak dapat login.
-   Riwayat aktivitas dan transaksi yang dibuat staf tetap dipertahankan
    setelah akun dinonaktifkan.

### 5.3 Akun pelanggan

-   Registrasi wajib menggunakan email dan nomor WhatsApp.
-   Email dan nomor WhatsApp harus unik untuk setiap akun pelanggan.
-   Pelanggan dapat login menggunakan email **atau** nomor WhatsApp
    dengan kata sandi yang sama.
-   Email harus diverifikasi melalui tautan sebelum akun dapat digunakan
    sepenuhnya.
-   Sistem menyediakan pengiriman ulang tautan verifikasi.
-   Nomor WhatsApp menjadi kontak utama pelanggan, tetapi verifikasi OTP
    WhatsApp ditunda.
-   Pelanggan dapat memperbarui email dan nomor WhatsApp melalui
    pengaturan akun dengan validasi yang sesuai.
-   Forgot Password/Reset Password tersedia melalui email terdaftar.
-   Kata sandi minimal 8 karakter dan mengandung kombinasi huruf dan
    angka.
-   Setelah 5 percobaan login gagal berturut-turut, proses login dikunci
    sementara selama 15 menit.
-   Fitur Remember Me tersedia dengan pengelolaan sesi yang aman.
-   Percobaan login gagal, penguncian, perubahan kata sandi, dan
    aktivitas keamanan penting dicatat.

### 5.4 Fitur autentikasi yang ditunda

-   Verifikasi nomor WhatsApp menggunakan OTP ditunda ke tahap
    pengembangan berikutnya.

## 6. Produk, kategori, harga, dan promosi

### 6.1 Kategori produk

Kategori/jenis produk utama: - Tas impor. - Tas lokal premium. - Tas
lokal terjangkau.

Produk dapat memiliki beberapa model atau warna. Stok dikelola terpisah
untuk setiap varian.

### 6.2 Data produk

Data produk sekurang-kurangnya mencakup: - Nama dan deskripsi. -
Kategori. - Harga jual. - Harga pokok penjualan (HPP). - Foto produk. -
Varian/model/warna. - Status aktif atau tidak aktif.

Keputusan awal: harga jual dan HPP sama untuk seluruh varian dari satu
produk. Kebijakan ini dapat dievaluasi kembali jika kebutuhan bisnis
berubah.

### 6.3 Diskon produk

-   Diskon produk mendukung persentase dan potongan nominal.
-   Pemilik mengelola diskon; staf hanya dapat mengelola jika diberi
    izin.
-   Diskon tidak berakhir otomatis. Pemilik/staf berizin menonaktifkan
    atau menghapusnya secara manual.
-   Harga asli, nilai diskon, dan harga akhir harus disimpan pada detail
    transaksi.
-   Pembuatan, perubahan, dan penghapusan diskon dicatat dalam Activity
    Log.

### 6.4 Aturan kombinasi diskon dan voucher

-   Diskon produk dan voucher tidak dapat digunakan bersamaan pada satu
    transaksi.
-   Jika produk memperoleh diskon, voucher tidak dapat diterapkan pada
    transaksi tersebut.
-   Jika pelanggan menggunakan voucher, sistem menerapkan harga normal
    pada produk yang memenuhi ketentuan voucher.
-   Promo gratis ongkir boleh digabungkan dengan diskon produk **atau**
    voucher.
-   Diskon produk + voucher + gratis ongkir tidak diperbolehkan karena
    diskon produk dan voucher tidak boleh digabungkan.

Detail penerapan voucher terhadap produk yang memenuhi syarat perlu
dirinci pada spesifikasi promosi.

## 7. Inventaris, stok, pemasok, dan pembelian

### 7.1 Pengelolaan stok

-   Stok dicatat per varian produk.
-   Ambang minimum stok awal adalah 3 unit per varian.
-   Jika stok mencapai 3 atau kurang, sistem memberikan notifikasi stok
    rendah.
-   Stok 0 berarti habis.
-   Pemilik dapat mengubah ambang minimum stok.

### 7.2 Stok masuk

Fitur Stock In wajib tersedia. Data minimal: - Varian produk. -
Jumlah. - Tanggal penerimaan. - Pemasok/sumber barang. - HPP/biaya per
unit (opsional sesuai kebutuhan). - Catatan (opsional).

Setelah disimpan, stok bertambah otomatis. Pergerakan stok dan
aktivitasnya dicatat.

### 7.3 Penyesuaian stok

-   Stock Adjustment wajib tersedia untuk mengoreksi perbedaan stok
    fisik dan sistem.
-   Alasan penyesuaian wajib diisi.
-   Perubahan dicatat pada riwayat pergerakan stok dan Activity Log.

### 7.4 Pemasok

Data pemasok mencakup nama, WhatsApp, alamat, dan catatan. Pemilik/staf
berizin dapat membuat, mengubah, dan menonaktifkan pemasok. Riwayat
pemasok tetap dipertahankan setelah dinonaktifkan. Sistem menampilkan
riwayat barang masuk yang terkait dengan pemasok.

### 7.5 Pembelian dari pemasok

Pembelian mencatat: - Pemasok dan tanggal pembelian. - Produk/varian dan
kuantitas. - Biaya per unit dan total. - Status pembayaran: belum
dibayar, sebagian, atau lunas. - Catatan.

Pembelian yang dikonfirmasi menambah stok secara otomatis tepat satu
kali. Sistem harus mencegah penambahan stok ganda. Data pembelian
terhubung dengan laporan keuangan.

### 7.6 Pengeluaran operasional

Pencatatan biaya listrik, air, sewa, gaji, kemasan, transportasi, dan
biaya lainnya ditunda ke tahap berikutnya. Struktur laporan keuangan
sebaiknya dapat diperluas untuk mendukung pengeluaran tersebut.

## 8. Penjualan, pesanan, pembayaran, dan pengiriman

### 8.1 Kanal penjualan

Sistem mendukung pencatatan penjualan online dan offline. Kanal bisnis
yang ada meliputi website, Facebook, Instagram, TikTok, WhatsApp, dan
toko fisik. Penjualan offline perlu dapat dicatat melalui
dashboard/admin.

### 8.2 Metode pembayaran

Metode awal: - Transfer bank. - QRIS. - E-wallet. - Tunai untuk
transaksi toko fisik.

Belum menggunakan payment gateway. Pembayaran online diverifikasi secara
manual oleh admin. Pelanggan mengunggah bukti pembayaran untuk transfer
bank, QRIS, atau e-wallet. Admin dapat menyetujui atau menolak bukti.
Status dan riwayat pembayaran dicatat.

### 8.3 Batas waktu pembayaran

-   Pesanan online memiliki batas waktu pembayaran 12 jam sejak pesanan
    dibuat.
-   Jika belum dibayar setelah 12 jam, pesanan dibatalkan otomatis.
-   Pengecualian: jika pelanggan sudah mengunggah bukti pembayaran dan
    bukti tersebut masih menunggu verifikasi admin, pesanan tidak boleh
    dibatalkan hanya karena batas 12 jam terlewati.
-   Saat pesanan dibatalkan, stok yang dialokasikan/reservasi untuk
    pesanan dilepaskan kembali.
-   Pembatalan dan pelepasan stok dicatat.

### 8.4 Status pesanan

Alur utama: 1. Menunggu Pembayaran. 2. Menunggu Verifikasi. 3. Diproses.
4. Dikirim. 5. Selesai.

Status tambahan: - Dibatalkan. - Pengajuan Pengembalian.

Setiap perubahan status disimpan dalam riwayat pesanan dan Activity Log.

### 8.5 Pengiriman

-   Kurir lokal melayani Kisaran dan wilayah sekitarnya.
-   Ekspedisi eksternal dapat mencakup J&T, JNE, SiCepat, dan layanan
    lain.
-   Pengelolaan kurir dilakukan secara manual pada versi awal; integrasi
    API ekspedisi ditunda.
-   Data pengiriman mencakup penerima/alamat, jenis pengiriman, kurir,
    nomor resi jika tersedia, biaya, status, dan tanggal terkait.
-   Biaya pengiriman ditanggung pelanggan dan ditampilkan terpisah dari
    harga produk sebelum checkout.
-   Biaya dihitung dan dikelola manual oleh admin pada versi awal.
-   Promo gratis ongkir dapat dibuat pemilik, dengan ketentuan minimum
    pembelian, periode, wilayah, atau jenis pengiriman sesuai pengaturan
    promo.

### 8.6 Konfirmasi penerimaan

-   Pelanggan dapat mengonfirmasi penerimaan barang.
-   Jika pelanggan belum mengonfirmasi dalam 3 hari setelah status
    Dikirim, sistem mengirim pengingat kepada pelanggan dan notifikasi
    kepada admin.
-   Pesanan tidak otomatis berubah menjadi Selesai hanya karena 3 hari
    berlalu.
-   Admin dapat memeriksa dan mengubah status menjadi Selesai secara
    manual.

### 8.7 Pembatalan pesanan

-   Menunggu Pembayaran: pelanggan dapat membatalkan sendiri.
-   Menunggu Verifikasi: pembatalan harus melalui admin karena bukti
    pembayaran telah diunggah.
-   Diproses: pelanggan mengajukan pembatalan dan admin memutuskan
    persetujuan.
-   Dikirim: tidak dapat dibatalkan melalui pembatalan biasa; pelanggan
    mengikuti prosedur retur jika memenuhi syarat.
-   Pelanggan wajib memilih alasan pembatalan. Pilihan "Alasan lainnya"
    menyediakan keterangan tambahan.
-   Alasan dan waktu pembatalan dicatat.
-   Stok yang dialokasikan dikembalikan sesuai hasil pembatalan.

## 9. Retur, penukaran, dan refund

-   Retur hanya diterima untuk produk rusak, cacat, atau tidak sesuai
    pesanan.
-   Pelanggan wajib memberikan bukti video unboxing yang valid.
-   Pengajuan retur maksimal 2 × 24 jam setelah pelanggan menerima
    barang.
-   Admin memeriksa bukti dan menyetujui atau menolak pengajuan.
-   Jika kesalahan berasal dari toko (barang rusak/cacat atau salah
    kirim), biaya pengiriman retur ditanggung toko.
-   Jika pengajuan ditolak, biaya pengiriman tidak menjadi tanggungan
    toko.
-   Pelanggan dapat memilih penukaran barang atau refund, dengan
    keputusan akhir dan pemeriksaan oleh admin.
-   Penukaran bergantung pada ketersediaan stok.
-   Refund diproses setelah disetujui dan pemeriksaan barang selesai.
-   Refund diutamakan melalui metode pembayaran awal. Jika tidak
    memungkinkan, pelanggan dapat memberikan rekening bank atau metode
    penerimaan dana lain yang disetujui admin.
-   Admin memverifikasi data penerima refund.
-   Status proses refund dapat dilihat pelanggan melalui My Account.
-   Semua proses retur, perubahan stok, penukaran, dan refund dicatat
    dalam riwayat transaksi dan Activity Log.

**Perlu diputuskan pada spesifikasi fitur:** batas waktu penyelesaian
refund, alur pengiriman barang retur ke toko, dan rincian kondisi barang
setelah diterima kembali.

## 10. CRM, poin, membership, voucher, dan wishlist

### 10.1 Data CRM

Sistem menyimpan profil pelanggan, kontak, riwayat pesanan, total
belanja, membership, poin, voucher, segmentasi, ulasan, dan umpan balik.
Penggunaan data pribadi harus sesuai kebijakan privasi dan persetujuan
pelanggan yang relevan.

### 10.2 Program poin

-   Konversi awal: setiap Rp100.000 pembelian yang memenuhi syarat
    menghasilkan 1 poin.
-   Poin diberikan setelah status pesanan yang memenuhi syarat tercapai.
-   Sistem mencegah pemberian poin ganda untuk transaksi yang sama.
-   Poin dikoreksi jika pesanan dibatalkan atau diretur.
-   Pelanggan dapat menukar poin menjadi voucher diskon saat checkout.
-   Pemilik dapat mengatur nilai konversi dan nilai voucher.
-   Sistem menyediakan ledger/riwayat poin.

**Perlu diputuskan:** status pesanan yang menjadi pemicu final pemberian
poin dan rumus perhitungan pembelian yang memenuhi syarat (misalnya
sebelum/sesudah ongkir, diskon, atau refund).

### 10.3 Membership

Tingkat membership: - Bronze. - Silver. - Gold.

Keputusan yang telah disepakati: - Rank membership ditentukan
berdasarkan saldo poin pelanggan saat ini, bukan total belanja sepanjang
masa. - Total belanja tetap disimpan sebagai data riwayat dan
analitik. - Jika tidak ada transaksi selama 3 bulan, pengurangan poin
bertahap mulai diterapkan. - Pengurangan poin dapat menurunkan rank
secara bertahap. - Poin dari transaksi baru dapat meningkatkan kembali
saldo dan rank. - Pengurangan tidak dilakukan sekaligus tepat pada bulan
ketiga; mekanismenya bertahap.

**Perlu diputuskan:** ambang poin setiap rank, jumlah poin yang
dikurangi, interval pengurangan, dan cara sistem menentukan awal periode
tidak aktif.

### 10.4 Voucher

-   Voucher dapat diperoleh melalui penukaran poin.
-   Pemilik mengatur nilai voucher dan minimum pembelian.
-   Setiap voucher memiliki tanggal mulai dan tanggal kedaluwarsa yang
    diatur pemilik.
-   Voucher kedaluwarsa tidak dapat digunakan.
-   Setiap pelanggan hanya dapat menggunakan jenis voucher yang sama
    satu kali.
-   Jenis voucher yang sama dapat digunakan oleh banyak pelanggan
    berbeda.
-   Riwayat perolehan dan penggunaan voucher dicatat.
-   Voucher tidak dapat digabungkan dengan diskon produk, tetapi dapat
    digabungkan dengan promo gratis ongkir.

### 10.5 Wishlist

-   Pelanggan dapat menambah dan menghapus produk favorit.
-   Produk wishlist dapat dipindahkan ke keranjang.
-   Wishlist tersimpan pada akun pelanggan dan memerlukan login untuk
    penyimpanan permanen.
-   Katalog tetap dapat dilihat tanpa login.

## 11. Keranjang dan checkout pelanggan

-   Pelanggan dapat menjelajahi katalog dan memasukkan produk ke
    keranjang tanpa login.
-   Pelanggan wajib login atau registrasi sebelum menyelesaikan
    checkout.
-   Keranjang pelanggan tetap tersimpan setelah logout dan dapat diakses
    kembali setelah login.
-   Keranjang tidak memiliki batas waktu pengosongan otomatis; produk
    tetap tersimpan sampai dihapus pelanggan atau checkout diselesaikan.
-   Sistem memeriksa ulang harga dan stok saat keranjang dibuka dan
    sebelum checkout.
-   Jika stok habis atau harga berubah, pelanggan diberi informasi
    sebelum melanjutkan.
-   Keranjang guest yang dibuat sebelum login digabungkan dengan
    keranjang akun setelah login.
-   Produk dan varian yang berbeda ditambahkan; produk/varian yang sama
    menggabungkan jumlahnya.
-   Jika jumlah gabungan melebihi stok, sistem menyesuaikan jumlah yang
    tersedia dan memberi tahu pelanggan.
-   Sistem harus memastikan stok tidak terjual melebihi ketersediaan
    ketika pesanan diproses.

## 12. Dashboard pelanggan dan alamat

### 12.1 My Account

Dashboard pelanggan memuat: - Ringkasan pesanan. - Riwayat transaksi. -
Status pengiriman. - Saldo poin dan membership. - Wishlist. - Profil dan
alamat. - Riwayat voucher. - Pusat notifikasi.

### 12.2 Alamat pengiriman

-   Pelanggan dapat menyimpan lebih dari satu alamat.
-   Pelanggan dapat menambah, mengubah, dan menghapus alamat.
-   Alamat dapat diberi label, misalnya Rumah, Kos, atau Kantor.
-   Pelanggan dapat menentukan satu alamat utama.
-   Saat checkout, pelanggan memilih alamat tujuan.
-   Data alamat wajib mencakup nama penerima, nomor telepon/WhatsApp,
    provinsi, kabupaten/kota, kecamatan, kode pos, dan detail alamat.
-   Alamat yang dipakai dalam transaksi disimpan sebagai snapshot data
    pesanan agar riwayat tidak berubah jika alamat profil diedit
    kemudian.

## 13. Ulasan dan rating produk

-   Ulasan hanya dapat diberikan oleh pelanggan yang membeli produk dan
    pesanan berstatus Selesai.
-   Satu pelanggan memiliki satu ulasan aktif untuk setiap produk.
-   Ulasan berisi rating 1--5 bintang dan komentar.
-   Pelanggan dapat mengedit atau menghapus ulasannya sendiri.
-   Admin dapat memoderasi atau menyembunyikan ulasan yang mengandung
    spam, kata kasar, atau konten tidak pantas.
-   Ulasan tersembunyi tetap disimpan untuk administrasi.
-   Sistem menampilkan rata-rata rating produk.
-   Pelanggan dapat mengunggah maksimal 3 foto untuk setiap ulasan.
-   Pelanggan dapat menambah, mengganti, atau menghapus foto selama
    ulasan dapat diedit.
-   Admin dapat memoderasi foto yang tidak pantas atau tidak relevan.

## 14. Notifikasi dan komunikasi

### 14.1 Notifikasi admin

Notifikasi dashboard admin wajib mencakup: - Pesanan baru. - Konfirmasi
pembayaran. - Stok rendah dan stok habis. - Pembatalan. - Pengajuan
retur. - Perubahan poin atau membership.

Notifikasi memiliki jumlah belum dibaca, waktu dan sumber, tautan ke
halaman terkait, serta penerima berdasarkan role/permission. Ambang stok
dapat dikonfigurasi.

### 14.2 Notifikasi pelanggan

Pusat notifikasi website wajib tersedia dan mencakup: - Pesanan berhasil
dibuat. - Pembayaran diterima atau ditolak. - Pesanan diproses atau
dikirim. - Nomor resi diperbarui. - Pengajuan retur disetujui atau
ditolak. - Poin bertambah atau berkurang. - Voucher diperoleh atau
mendekati kedaluwarsa.

Pelanggan dapat melihat waktu notifikasi dan menandainya sebagai sudah
dibaca.

### 14.3 Email dan WhatsApp

-   Email otomatis hanya dikirim untuk pembayaran yang berhasil
    dikonfirmasi admin.
-   Email konfirmasi berisi nomor pesanan, rincian pembayaran, total
    transaksi, dan informasi bahwa pembayaran berhasil.
-   Jika pembayaran ditolak, notifikasi hanya melalui website.
-   Email otomatis untuk peristiwa lain belum termasuk versi awal.
-   Integrasi notifikasi WhatsApp otomatis ditunda.
-   Website menyediakan tombol "Hubungi Kami melalui WhatsApp" yang
    mengarahkan pelanggan ke WhatsApp toko.
-   Nomor WhatsApp tujuan dikelola pemilik melalui dashboard admin atau
    konfigurasi sistem.
-   Live chat internal tidak termasuk versi awal.
-   Notifikasi stok tersedia kembali tidak dibuat; informasi stok baru
    dapat diumumkan melalui media sosial.

## 15. Halaman publik dan pengelolaan konten

Website pelanggan mencakup halaman: - Home. - Katalog, kategori,
pencarian, dan filter. - Detail produk. - Keranjang dan checkout. - My
Account. - Tentang Kami. - Syarat dan Ketentuan. - Kebijakan Privasi. -
Kebijakan Pengiriman. - Kebijakan Pembatalan dan Pengembalian Barang. -
Kontak/Hubungi Kami.

Halaman Tentang Kami memuat profil singkat, cerita toko, lokasi toko
fisik, kontak, media sosial, serta foto toko/aktivitas jika tersedia.

Pemilik dapat memperbarui konten tertentu melalui dashboard tanpa
mengubah kode program, termasuk: - Banner utama Home. - Gambar dan
informasi promosi. - Profil/Tentang Kami. - Nomor WhatsApp toko. -
Tautan media sosial. - Alamat dan jam operasional. - Konten halaman
informasi dan kebijakan.

Pemilik memiliki akses pengelolaan konten. Akses kepada staf dapat
diberikan melalui permission.

## 16. Activity Log dan audit

Activity Log wajib tersedia dan mencatat aktivitas operasional serta
keamanan, termasuk: - Login berhasil/gagal, logout, dan perubahan kata
sandi. - Perubahan permission dan role. - Pembuatan, perubahan, dan
penghapusan produk. - Stok masuk, stok keluar, dan penyesuaian stok. -
Transaksi, pembayaran, pembatalan, retur, penukaran, dan refund. -
Perubahan profil pelanggan, poin, membership, dan voucher. - Pembuatan,
perubahan, dan penonaktifan akun staf.

Setiap catatan minimal memuat aktor, jenis tindakan, waktu, dan
perubahan relevan sebelum/sesudah. Informasi sensitif seperti kata sandi
tidak boleh disimpan dalam log. Log harus dilindungi dari perubahan yang
tidak berwenang dan tetap tersedia setelah akun staf dinonaktifkan.
Pemilik dapat melihat seluruh log; akses staf mengikuti permission.

## 17. Backup dan pemulihan

-   Backup database otomatis dilakukan setiap minggu.
-   Pemilik dapat memicu backup manual melalui dashboard.
-   Backup disimpan secara aman dan tidak dapat diakses pelanggan.
-   Sistem mencatat waktu serta keberhasilan/kegagalan backup.
-   Sistem menyimpan 4 backup mingguan terbaru.
-   Backup lama hanya dihapus setelah backup baru berhasil dan
    diverifikasi.
-   Pemilik atau role yang diberi wewenang dapat melakukan pemulihan
    data.

Jadwal teknis, lokasi penyimpanan, enkripsi, dan prosedur pemulihan
rinci ditetapkan pada spesifikasi teknis.

## 18. Laporan

Laporan awal mencakup penjualan dan keuntungan. Data transaksi harus
menyimpan informasi harga, HPP, diskon, voucher, ongkir, dan
pengembalian agar laporan dapat dihitung secara konsisten.

Modul pengeluaran operasional ditunda, tetapi rancangan laporan harus
dapat diperluas untuk memasukkan pengeluaran tersebut di tahap
berikutnya.

## 19. Fitur versi awal dan fitur yang ditunda

### 19.1 Termasuk versi awal

-   Website e-commerce pelanggan dan dashboard admin.
-   Autentikasi pelanggan, verifikasi email, reset password, login
    dengan email/WhatsApp, Remember Me, dan pembatasan login gagal.
-   Produk, kategori, varian, harga, foto, dan diskon.
-   Inventaris, stok masuk, stock adjustment, pemasok, dan pembelian.
-   Penjualan online dan offline.
-   Pesanan, pembayaran manual, pengiriman manual, pembatalan, retur,
    penukaran, dan refund.
-   Laporan penjualan dan keuntungan.
-   CRM, poin, membership, voucher, wishlist, dan ulasan.
-   Keranjang tersimpan, checkout wajib login, beberapa alamat
    pengiriman.
-   Pusat notifikasi pelanggan dan admin.
-   Email konfirmasi pembayaran berhasil.
-   Tombol Hubungi Kami melalui WhatsApp.
-   Halaman Tentang Kami dan halaman kebijakan.
-   Pengelolaan konten website.
-   Activity Log.
-   Backup mingguan dan backup manual.

### 19.2 Ditunda untuk pengembangan berikutnya

-   Verifikasi nomor WhatsApp menggunakan OTP.
-   Integrasi payment gateway.
-   Integrasi API kurir/ekspedisi.
-   Notifikasi WhatsApp otomatis.
-   Live chat internal website.
-   Notifikasi otomatis saat stok tersedia kembali.
-   Pencatatan pengeluaran operasional.
-   Fitur tambahan lain yang belum disepakati.

## 20. Hal yang masih perlu diputuskan

Daftar berikut sengaja belum diisi dengan asumsi agar keputusan bisnis
tidak dibuat secara sepihak.

1.  Teknologi frontend pelanggan.
2.  Ambang poin Bronze, Silver, dan Gold.
3.  Jumlah serta interval pengurangan poin setelah 3 bulan tanpa
    transaksi.
4.  Status pesanan yang memicu pemberian poin dan dasar perhitungan
    pembelian yang memenuhi syarat.
5.  Batas waktu dan prosedur penyelesaian refund.
6.  Rincian alur penerimaan dan pemeriksaan barang retur.
7.  Detail teknis tarif pengiriman manual dan pengaturan wilayah/kurir.
8.  Detail teknis penyimpanan backup dan prosedur restore.
9.  Batas ukuran/format file untuk foto produk, bukti pembayaran, video
    unboxing, dan foto ulasan.
10. Detail endpoint dan kontrak API untuk integrasi frontend pelanggan.
11. Ketentuan rinci promo gratis ongkir, termasuk apakah promo dapat
    menanggung seluruh ongkir atau dibatasi nominal tertentu.

Butir-butir tersebut dapat dibahas pada spesifikasi fitur terkait. Tidak
semuanya harus diselesaikan dalam Project Constitution.

## 21. Tahapan kerja setelah Constitution disetujui

Urutan kerja yang disarankan: 1. Finalisasi dan persetujuan Project
Constitution. 2. Project Overview dan kebutuhan sistem. 3. Business
Requirements dan Business Rules. 4. System Architecture dan kontrak
integrasi. 5. Database Specification/ERD. 6. Feature Specifications
beserta acceptance criteria. 7. Task Breakdown dan pembagian pekerjaan.
8. Implementasi bertahap. 9. Pengujian dan verifikasi setiap fitur. 10.
Integrasi frontend pelanggan dengan backend dan persiapan deployment.

------------------------------------------------------------------------

**Persetujuan**

Dokumen ini masih berstatus draf. Perubahan hanya dilakukan setelah
dibahas dan disepakati oleh pihak proyek. Setelah disetujui, dokumen
menjadi acuan utama untuk spesifikasi dan implementasi berikutnya.
