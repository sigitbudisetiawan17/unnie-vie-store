# Business Rules — Unnie Vie Store

**Versi:** 0.1  
**Status:** Draft kompilasi  
**Tanggal:** 14 November 2026

Aturan berikut merangkum keputusan bisnis yang telah dibahas. Kode aplikasi wajib menegakkannya di backend; menyembunyikan tombol pada UI saja tidak cukup.

## BRS-01 — Produk dan katalog
1. Kelompok produk (impor, lokal premium, lokal terjangkau) berbeda dari kategori model tas.
2. Produk memiliki satu atau lebih varian; stok dikelola per varian.
3. Harga jual awal dan HPP berlaku sama untuk seluruh varian dari produk yang sama.
4. SKU dibuat otomatis dan harus unik secara global.
5. Produk dapat memiliki foto umum dan foto khusus varian.
6. Diskon dapat berupa persentase atau nominal tetap; harga asli, diskon, dan harga akhir disimpan pada transaksi.
7. Produk yang pernah digunakan dalam transaksi tidak boleh dihapus permanen melalui dashboard; produk dinonaktifkan.
8. Produk yang belum pernah digunakan dalam transaksi dapat dihapus oleh pengguna berwenang.
9. Produk nonaktif tidak tampil pada katalog pelanggan.
10. Perubahan produk dan diskon dicatat di Activity Log.

## BRS-02 — Inventaris
1. Stok dicatat per varian.
2. `available = on_hand - reserved`.
3. Alokasi pesanan online mengurangi stok tersedia melalui penambahan reserved, bukan pengurangan stok fisik.
4. Saat pesanan dikirim, on_hand berkurang dan reserved dilepas.
5. Saat pesanan dibatalkan, reserved dilepas.
6. Penjualan offline mengurangi on_hand saat transaksi dikonfirmasi.
7. Stok tidak boleh negatif.
8. Alokasi stok harus atomik menggunakan transaksi database dan row lock.
9. Stok masuk hanya dicatat setelah barang secara fisik diterima dan dikonfirmasi.
10. Penerimaan pembelian dapat dilakukan sebagian.
11. Setiap penerimaan barang hanya boleh menambah stok satu kali.
12. Penyesuaian stok wajib memiliki alasan.
13. Penyesuaian tidak boleh menurunkan on_hand di bawah jumlah yang sedang reserved.
14. Ambang stok rendah default 3 unit per varian dan dapat diubah pemilik.
15. Stok tersedia pada atau di bawah ambang memicu peringatan; nol berarti habis.
16. Stok retur hanya kembali ke stok layak jual setelah pemeriksaan menyatakan barang dapat dijual kembali.

## BRS-03 — Penjualan dan pesanan
1. Harga, diskon, ongkir, dan total akhir dihitung/divalidasi oleh backend.
2. Item transaksi menyimpan snapshot nama produk, varian, SKU, harga, diskon, harga akhir, dan HPP.
3. Pesanan online mengalokasikan stok saat pesanan berhasil dibuat.
4. Pesanan yang belum dibayar memiliki batas pembayaran 12 jam.
5. Pesanan yang telah mengunggah bukti dan menunggu verifikasi tidak dibatalkan otomatis hanya karena batas 12 jam lewat.
6. Pembatalan harus melepaskan alokasi stok dan tercatat di riwayat.
7. Status pesanan mengikuti alur Menunggu Pembayaran → Menunggu Verifikasi → Diproses → Dikirim → Selesai, dengan status tambahan Dibatalkan dan Pengajuan Pengembalian.
8. Pelanggan dapat membatalkan sendiri saat Menunggu Pembayaran; status berikutnya memerlukan proses admin.
9. Pesanan yang sudah Dikirim tidak menggunakan pembatalan biasa; gunakan proses retur.
10. Jika pelanggan belum mengonfirmasi penerimaan selama 3 hari setelah pengiriman, sistem mengirim pengingat dan memberi notifikasi admin; pesanan tidak otomatis selesai.

## BRS-04 — Akun dan checkout
1. Akun pelanggan terpisah dari akun admin/staf.
2. Katalog dapat dilihat tanpa login; checkout wajib login.
3. Email dan nomor WhatsApp pelanggan wajib dan unik.
4. Email harus diverifikasi sebelum akun digunakan sepenuhnya.
5. Login pelanggan menggunakan email atau WhatsApp dengan satu kata sandi.
6. Kata sandi minimal 8 karakter dan mengandung huruf serta angka.
7. Lima percobaan login gagal berturut-turut mengunci login selama 15 menit.
8. Reset kata sandi melalui email.
9. Keranjang tetap tersimpan setelah logout dan tidak kedaluwarsa otomatis.
10. Keranjang guest digabungkan saat login; varian yang sama menjumlahkan kuantitas.
11. Stok dan harga diperiksa ulang saat keranjang dibuka dan sebelum checkout.
12. Perubahan alamat profil tidak mengubah snapshot alamat pesanan yang sudah dibuat.

## BRS-05 — CRM dan loyalitas
1. Setiap Rp100.000 nilai produk yang memenuhi syarat menghasilkan 1 poin.
2. Ongkir tidak dihitung; dasar poin adalah nilai produk setelah diskon.
3. Pecahan poin dibulatkan ke bawah.
4. Poin diberikan setelah pesanan berstatus Selesai.
5. Pemberian poin harus idempotent dan tidak boleh ganda.
6. Pembatalan/retur yang memenuhi ketentuan harus mengoreksi poin melalui transaksi ledger, bukan menghapus riwayat.
7. Membership Bronze/Silver/Gold ditentukan berdasarkan saldo poin saat ini; total belanja tetap dicatat terpisah.
8. Tiga bulan tanpa transaksi yang memenuhi syarat memulai pengurangan poin bertahap.
9. Default pengurangan adalah 1 poin per bulan dan dapat dikonfigurasi.
10. Transaksi baru yang memenuhi syarat mereset periode inaktivitas.
11. Ambang rank dan konversi poin ke voucher dapat dikonfigurasi pemilik.
12. Ulasan hanya dapat dibuat pelanggan yang menyelesaikan pembelian produk terkait.
13. Ulasan berisi rating 1–5 dan teks; maksimal 3 foto.
14. Pelanggan dapat mengedit/menghapus ulasannya sendiri.
15. Admin dapat menyembunyikan ulasan spam/tidak pantas tanpa menghapus catatan database.
16. Wishlist membutuhkan login agar tersimpan pada akun.

## BRS-06 — Pembayaran, pengiriman, retur
1. Metode pembayaran awal: transfer bank, QRIS, e-wallet, dan tunai di toko.
2. Tidak ada payment gateway pada tahap awal.
3. Bukti pembayaran online diunggah pelanggan dan diverifikasi admin.
4. Penolakan pembayaran wajib menyertakan alasan dan diinformasikan melalui website.
5. Email dikirim untuk pembayaran yang berhasil dikonfirmasi admin.
6. Pengiriman lokal menggunakan kurir lokal; luar area menggunakan ekspedisi eksternal secara manual.
7. Ongkir dibayar pelanggan terpisah kecuali ada promo gratis ongkir yang memenuhi syarat.
8. Retur hanya untuk barang rusak, cacat, atau tidak sesuai.
9. Pengajuan retur maksimal 2 x 24 jam setelah barang diterima.
10. Video unboxing yang valid wajib menjadi bukti pengajuan.
11. Jika kesalahan berasal dari toko, biaya pengiriman retur ditanggung toko.
12. Pelanggan memilih penukaran atau refund; keputusan akhir mengikuti pemeriksaan admin.
13. Penukaran bergantung pada ketersediaan stok.
14. Refund dilakukan setelah retur disetujui dan pemeriksaan selesai.
15. Refund diutamakan melalui metode pembayaran asal; alternatif memerlukan detail rekening/metode payout yang diverifikasi admin.
16. Status refund harus terlihat oleh pelanggan.
17. Barang retur tidak menambah stok layak jual sebelum inspeksi.
18. Semua perubahan pembayaran, pengiriman, retur, dan refund dicatat.

## BRS-07 — Admin, keamanan, dan operasional
1. Pemilik memiliki akses penuh.
2. Staf hanya dapat melakukan tindakan sesuai role dan permission.
3. Akun staf nonaktif tidak dapat login; riwayat tindakannya tetap ada.
4. Pemilik dapat membuat, mengubah, menonaktifkan, dan menetapkan role staf.
5. Activity Log mencatat aktor, tindakan, waktu, dan perubahan relevan sebelum/sesudah.
6. Password dan rahasia autentikasi tidak boleh masuk log.
7. Backup database otomatis mingguan dan dapat dijalankan manual oleh pemilik.
8. Sistem menyimpan 4 backup mingguan terbaru.
9. Backup lama baru dihapus setelah backup baru berhasil dan terverifikasi.
10. Backup disimpan aman dan tidak dapat diakses pelanggan.
11. Proses restore hanya untuk pemilik atau role berwenang.
12. Notifikasi admin bersifat role-aware dan dapat ditandai telah dibaca.
13. Kontak WhatsApp toko dapat diatur; belum ada live chat internal.
14. Email otomatis pada tahap awal hanya untuk konfirmasi pembayaran berhasil.

## Aturan lintas fitur
- Operasi pembayaran/pesanan harus tahan terhadap request duplikat (idempotency).
- Kegagalan proses tidak boleh meninggalkan stok atau status transaksi dalam kondisi setengah tersimpan.
- Koreksi transaksi harus meninggalkan jejak audit.
- Gunakan waktu server yang konsisten.
- Hak akses diverifikasi di server pada setiap endpoint/action sensitif.
