# Database Specification — Unnie Vie Store

**Versi:** 0.1  
**Status:** Draft konseptual; belum menjadi migration  
**Tanggal:** 14 November 2026

## 1. Standar database
- DBMS: MySQL.
- Engine: InnoDB.
- Charset: `utf8mb4`.
- Collation: `utf8mb4_unicode_ci`.
- Primary key umum: `BIGINT UNSIGNED`.
- Foreign key digunakan untuk relasi yang membutuhkan integritas referensial.
- Nilai uang disimpan sebagai integer Rupiah (`BIGINT`), bukan floating point.
- Kuantitas stok menggunakan integer non-negatif.
- Timestamp menggunakan waktu server yang konsisten.
- Status bisnis dikendalikan aplikasi dengan validasi terpusat; hindari ENUM yang menyulitkan evolusi status.
- Master data yang perlu dipertahankan dapat menggunakan soft delete/nonaktif.
- Ledger, stock movement, dan histori transaksi tidak dihapus sebagai cara koreksi.

## 2. Kelompok tabel konseptual

### Akun dan akses
- `users` — akun pemilik/admin/staf (mengikuti Laravel).
- `customers` — akun pelanggan terpisah.
- `roles`, `permissions`, `role_user`, `permission_role` — RBAC konseptual; sesuaikan dengan package yang dipilih setelah audit.
- `customer_addresses` — alamat pelanggan.

### Katalog
- `product_groups` — impor, lokal premium, lokal terjangkau.
- `product_categories` — model tas.
- `products` — data produk, harga dasar, HPP, deskripsi, status.
- `product_variants` — varian dan SKU.
- `product_images` — foto umum produk.
- `variant_images` — foto khusus varian.
- `product_discounts` — konfigurasi diskon.

### Supplier dan pembelian
- `suppliers` — data pemasok.
- `purchases` — dokumen pembelian dan status pembayaran.
- `purchase_items` — item/varian yang dibeli.
- `goods_receipts` — penerimaan barang; dapat lebih dari satu untuk pembelian parsial.
- `goods_receipt_items` — detail kuantitas yang diterima.

### Inventaris
- `stock_balances` — saldo on_hand dan reserved per varian.
- `stock_movements` — riwayat stok fisik masuk/keluar/adjustment.
- `stock_reservations` — alokasi stok untuk pesanan.

### Keranjang dan wishlist
- `carts`, `cart_items` — keranjang pelanggan/guest.
- `wishlists` — wishlist akun pelanggan.

### Pesanan dan pembayaran
- `orders`, `order_items` — header dan snapshot item transaksi.
- `order_status_histories` — riwayat status.
- `payments` — percobaan dan catatan pembayaran.
- `payment_proofs` — bukti transfer/QRIS/e-wallet.
- `refunds` — catatan refund.

### Pengiriman dan retur
- `shipments`, `shipment_status_histories`.
- `return_requests`, `return_items`, `return_evidences`.

### CRM
- `membership_tiers`.
- `customer_points` — saldo/rekap poin.
- `point_transactions` — ledger poin.
- `vouchers`, `customer_vouchers`, `voucher_redemptions`.
- `reviews`, `review_images`.

### Sistem dan CMS
- `activity_logs`.
- `notifications` — pertimbangkan pola Laravel database notifications.
- `store_settings`, `banners`, `content_pages`, `backup_logs`.

## 3. Aturan relasi dan integritas
- Setiap produk memiliki satu atau lebih varian.
- SKU varian harus unique.
- Satu saldo stok per varian (`stock_balances` unique per `product_variant_id`).
- Setiap order memiliki satu atau lebih order item.
- Order item menyimpan snapshot nama produk, varian, SKU, harga satuan, diskon, harga akhir, dan HPP.
- Alamat pengiriman disalin sebagai snapshot pada order; jangan hanya mengandalkan relasi ke alamat profil yang dapat berubah.
- Purchase dapat memiliki beberapa goods receipt untuk penerimaan parsial.
- Setiap goods receipt harus memiliki identitas/idempotency yang mencegah penerimaan ganda.
- Setiap stock reservation terkait order dan varian.
- Stock movement merekam perubahan fisik; reservation bukan stock movement fisik.
- Setiap perubahan poin direkam sebagai point transaction.
- File bukti dan video disimpan di private storage; database menyimpan metadata dan lokasi file, bukan konten biner.
- Relasi transaksi historis harus tetap tersedia walaupun master product/customer dinonaktifkan.

## 4. Aturan stok
- `available = on_hand - reserved`.
- Update saldo stok harus berada dalam DB transaction.
- Gunakan row-level lock saat alokasi atau perubahan stok yang bersaing.
- Jangan izinkan `on_hand < reserved` dan jangan izinkan saldo negatif.
- Pada pengiriman, kurangi on_hand dan lepaskan reserved dalam satu transaksi.
- Pada pembatalan, lepaskan reserved satu kali.
- Pada retur, barang baru menambah stok layak jual setelah pemeriksaan.

## 5. Catatan desain yang wajib diselesaikan sebelum migration
1. Tetapkan foreign key lengkap untuk purchase → receipt → receipt items.
2. Tentukan package RBAC dan sesuaikan tabel role/permission agar tidak duplikat.
3. Tentukan apakah notifikasi memakai tabel Laravel polymorphic notifications.
4. Rancang constraint/idempotency untuk payment verification, stock allocation, receipt posting, dan point awarding.
5. Tentukan relasi satu order ke banyak shipment.
6. Pisahkan alamat profil dari snapshot alamat pengiriman order.
7. Tetapkan aturan soft delete dan unique index ketika record dinonaktifkan.
8. Tentukan strategi penyimpanan uang, pajak/ongkir (jika relevan), dan pembulatan.
9. Tetapkan format SKU dan kebijakan perubahan SKU.
10. Review semua index untuk query laporan dan pencarian katalog.

## 6. Batas dokumen
Dokumen ini merupakan rancangan awal berdasarkan kebutuhan yang dibahas. Jangan membuat migration bisnis hanya dari daftar tabel; selesaikan relasi, constraint, index, dan aturan historis pada tahap desain implementasi.
