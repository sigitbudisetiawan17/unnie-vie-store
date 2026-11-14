# Business Requirements — Unnie Vie Store

**Versi:** 0.1  
**Status:** Draft kompilasi untuk implementasi bertahap  
**Tanggal:** 14 November 2026

## 1. Tujuan

Dokumen ini merangkum kebutuhan sistem yang mendukung website e-commerce pelanggan, operasional toko, inventaris, transaksi online/offline, pelaporan, dan CRM. Fitur diprioritaskan agar proses inti toko dapat berjalan lebih dahulu.

## 2. Kebutuhan fungsional

### BR-01 — Produk dan katalog
- Sistem menyediakan pengelompokan produk: tas impor, tas lokal premium, dan tas lokal terjangkau.
- Sistem menyediakan kategori model tas yang terpisah dari kelompok produk.
- Admin berwenang dapat mengelola produk, kategori, kelompok, varian, foto, harga jual, HPP, diskon, dan status aktif.
- Setiap varian memiliki SKU unik yang dibuat otomatis.
- Produk dan varian yang memiliki riwayat transaksi harus tetap dapat ditelusuri.

### BR-02 — Inventaris
- Sistem mencatat stok per varian.
- Sistem membedakan stok fisik, stok yang dialokasikan, dan stok tersedia.
- Sistem mencatat stok masuk, penerimaan pembelian, penyesuaian, dan pergerakan stok.
- Sistem memberi peringatan stok rendah berdasarkan ambang yang dapat diatur.
- Sistem mencegah stok negatif dan mencegah alokasi melebihi stok tersedia.

### BR-03 — Penjualan dan transaksi
- Sistem mendukung transaksi penjualan toko fisik dan pesanan online.
- Sistem menghitung subtotal, diskon, ongkir, dan total secara konsisten di backend.
- Sistem menyimpan snapshot informasi barang dan harga pada saat transaksi.
- Sistem mencatat pembayaran, status pesanan, pembatalan, dan riwayat perubahan.
- Sistem menyediakan bukti/struk transaksi.

### BR-04 — E-commerce dan pelanggan
- Pengunjung dapat melihat katalog tanpa login.
- Pelanggan harus login untuk menyelesaikan checkout.
- Pelanggan dapat mengelola profil, beberapa alamat, keranjang, wishlist, pesanan, dan notifikasi.
- Pelanggan dapat mengunggah bukti pembayaran dan memantau status pesanan/pengiriman.
- Pelanggan dapat mengajukan retur sesuai kebijakan yang berlaku.

### BR-05 — CRM dan loyalitas
- Sistem menyimpan profil dan riwayat transaksi pelanggan.
- Sistem mendukung poin, membership, voucher, ulasan, dan segmentasi pelanggan.
- Perubahan poin harus memiliki ledger/riwayat yang dapat diaudit.
- Perhitungan membership dan pengurangan poin karena inaktivitas mengikuti aturan yang dapat dikonfigurasi.

### BR-06 — Pembayaran, pengiriman, dan retur
- Sistem mendukung transfer bank, QRIS, e-wallet, dan pembayaran tunai di toko.
- Verifikasi pembayaran online dilakukan manual oleh admin pada tahap awal.
- Sistem mencatat jenis pengiriman, kurir, biaya, nomor resi bila tersedia, dan status.
- Sistem mendukung pembatalan, retur, penukaran, dan refund sesuai status dan bukti yang valid.

### BR-07 — Laporan dan pemantauan
- Sistem menyediakan ringkasan dashboard dan filter periode.
- Sistem menyediakan laporan penjualan, keuntungan kotor, dan persediaan.
- Sistem mendukung ekspor laporan ke Excel/PDF.
- Angka laporan harus berasal dari transaksi dan pergerakan stok yang tercatat, bukan data contoh.

### BR-08 — Administrasi dan keamanan
- Sistem memisahkan akun pelanggan dari akun admin/staf.
- Pemilik memiliki akses penuh; staf memperoleh role dan permission.
- Sistem mencatat aktivitas penting dalam Activity Log.
- Sistem menyediakan notifikasi internal dan backup database.
- Sistem menerapkan validasi dan otorisasi di backend.

## 3. Prioritas implementasi

**MVP/core:** autentikasi admin dan RBAC, dashboard dasar, katalog admin, supplier/pembelian, inventaris, penjualan offline, pesanan online dan verifikasi pembayaran, pengiriman/pembatalan, retur dasar, laporan penjualan/stok.

**Tahap lanjutan:** CRM/loyalty lengkap, voucher tingkat lanjut, wishlist/review, CMS lanjutan, notifikasi tambahan, dan integrasi eksternal yang sebelumnya ditunda.

## 4. Kebutuhan nonfungsional
- Backend menjadi sumber kebenaran untuk harga, stok, status, dan hak akses.
- Data penting harus konsisten dan dapat ditelusuri.
- Operasi yang mengubah stok atau transaksi harus atomik.
- Antarmuka admin responsif dan mudah digunakan.
- Aplikasi produksi menggunakan HTTPS.
- Lingkungan development, staging, dan production dipisahkan.
- Sistem harus memiliki automated tests untuk alur bisnis penting.
