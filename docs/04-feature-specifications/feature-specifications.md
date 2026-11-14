# Feature Specifications — Unnie Vie Store

**Versi:** 0.1  
**Status:** Draft spesifikasi MVP dan tahap lanjutan  
**Tanggal:** 14 November 2026

## Standar umum semua fitur
- Validasi dilakukan di backend.
- Otorisasi dilakukan di backend untuk setiap aksi sensitif.
- Operasi yang melibatkan stok/transaksi menggunakan DB transaction dan mekanisme idempotency.
- Perubahan penting tercatat di Activity Log.
- Error disampaikan dengan aman dan tidak membocorkan detail internal.
- Fitur memiliki automated tests untuk alur normal, gagal, dan kondisi bersamaan.
- UI admin responsif.
- Data dummy tidak boleh menjadi pengganti implementasi fungsional.

## FS-01 — Admin authentication dan RBAC (MVP)
**Fungsi:** login/logout admin, reset password, pengelolaan staf, role, permission, dan status akun.

**Acceptance criteria:**
- Pemilik dapat login ke area admin.
- Pemilik dapat membuat/mengubah/menonaktifkan akun staf dan menetapkan permission.
- Staf nonaktif tidak dapat login.
- Lima kegagalan login berturut-turut mengunci login 15 menit.
- Aksi login dan perubahan akses tercatat tanpa merekam password.
- Akses endpoint diperiksa di backend.

## FS-02 — Dashboard admin (MVP)
**Fungsi:** ringkasan omzet, transaksi, produk terjual, pesanan tertunda, produk terlaris, stok rendah/habis, dan aktivitas.

**Acceptance criteria:**
- Filter tanggal memengaruhi seluruh metrik terkait.
- Angka berasal dari data transaksi aktual.
- Pengguna hanya melihat data/aksi sesuai permission.
- Kondisi data kosong ditangani dengan benar.

## FS-03 — Katalog, kategori, varian, SKU (MVP)
**Fungsi:** CRUD kelompok, kategori, produk, varian, foto, harga, HPP, diskon, dan status.

**Acceptance criteria:**
- Produk wajib memiliki nama, kelompok, kategori, harga, HPP, minimal satu foto, dan minimal satu varian.
- SKU dibuat otomatis dan unik.
- Foto umum dan foto varian dapat dikelola.
- Produk yang telah memiliki transaksi tidak dapat dihapus permanen.
- Diskon dapat diaktif/nonaktifkan dan nilai transaksi menyimpan snapshot harga.

## FS-04 — Supplier dan pembelian (MVP)
**Fungsi:** pengelolaan supplier, purchase, item, pembayaran, dan penerimaan parsial.

**Acceptance criteria:**
- Pembelian mencatat supplier, tanggal, item/varian, kuantitas, biaya satuan, total, status pembayaran, dan catatan.
- Status pembayaran: unpaid, partial, paid.
- Penerimaan barang dapat dilakukan sebagian.
- Stok bertambah hanya ketika goods receipt dikonfirmasi.
- Goods receipt tidak dapat diposting dua kali.

## FS-05 — Inventaris (MVP)
**Fungsi:** saldo stok, stock movement, adjustment, dan peringatan stok rendah.

**Acceptance criteria:**
- Stok per varian menampilkan on_hand, reserved, dan available.
- Adjustment wajib memiliki alasan.
- Sistem menolak stok negatif dan adjustment yang melanggar reservation.
- Semua perubahan saldo memiliki movement/riwayat.
- Ambang stok rendah default 3 dan dapat diubah pemilik.

## FS-06 — Penjualan offline (MVP)
**Fungsi:** pencatatan penjualan langsung di toko.

**Acceptance criteria:**
- Admin memilih varian dan kuantitas.
- Sistem memeriksa stok dan menghitung total di backend.
- Pelanggan walk-in boleh tidak memiliki akun.
- Stok berkurang saat transaksi dikonfirmasi.
- Sistem menyimpan metode pembayaran dan menyediakan struk.
- Transaksi yang sudah tercatat tidak boleh diproses ganda.

## FS-07 — Pesanan online dan verifikasi pembayaran (MVP)
**Fungsi:** pesanan, alokasi stok, bukti pembayaran, verifikasi admin.

**Acceptance criteria:**
- Pembuatan order mengalokasikan stok secara atomik.
- Pelanggan dapat mengunggah bukti pembayaran.
- Admin dapat menerima/menolak bukti; penolakan wajib memiliki alasan.
- Order yang menunggu verifikasi setelah bukti diunggah tidak otomatis dibatalkan hanya karena 12 jam berlalu.
- Verifikasi ganda dicegah.
- Status dan riwayat perubahan tersimpan.

## FS-08 — Pengiriman dan pembatalan (MVP)
**Fungsi:** data penerima, jenis pengiriman, kurir, ongkir, resi, dan status.

**Acceptance criteria:**
- Admin dapat mengubah status menjadi Dikirim dan mencatat informasi kurir.
- Nomor resi dapat kosong untuk kurir lokal yang tidak menyediakan resi.
- Saat pengiriman dikonfirmasi, on_hand berkurang dan reservation dilepas satu kali.
- Pembatalan mengikuti batas status dan alasan wajib.
- Pembatalan melepaskan reservation satu kali.
- Tidak ada auto-complete setelah 3 hari; sistem hanya mengirim pengingat/notifikasi.

## FS-09 — Retur dan refund dasar (MVP terbatas)
**Fungsi:** pengajuan retur, bukti video unboxing, review admin, penukaran/refund.

**Acceptance criteria:**
- Pengajuan hanya untuk rusak, cacat, atau barang tidak sesuai.
- Pengajuan maksimal 2 x 24 jam setelah penerimaan.
- Video unboxing valid wajib diunggah.
- Admin dapat menyetujui/menolak dengan alasan.
- Penukaran memeriksa ketersediaan stok.
- Refund dilakukan setelah persetujuan dan pemeriksaan.
- Barang retur hanya masuk stok layak jual setelah inspeksi.
- Semua keputusan dan perubahan stok dicatat.

## FS-10 — Laporan (MVP)
**Fungsi:** laporan penjualan, keuntungan kotor, dan persediaan.

**Acceptance criteria:**
- Filter tanggal bekerja.
- Perhitungan keuntungan menggunakan snapshot HPP transaksi.
- Laporan dapat diekspor Excel/PDF.
- Hasil ekspor konsisten dengan data pada layar.

## FS-11 — CRM, poin, membership (tahap lanjutan)
- Profil pelanggan dan riwayat belanja.
- Poin diberikan setelah order Selesai: Rp100.000 nilai produk setelah diskon = 1 poin, ongkir tidak dihitung, dibulatkan ke bawah.
- Ledger poin mencegah pemberian ganda dan mencatat koreksi.
- Membership berdasarkan saldo poin; ambang dapat dikonfigurasi.
- Inaktivitas 3 bulan memulai pengurangan default 1 poin per bulan, dapat dikonfigurasi.

## FS-12 — Voucher, wishlist, dan ulasan (tahap lanjutan)
- Voucher dikonfigurasi pemilik dan dapat ditukarkan menggunakan poin.
- Wishlist memerlukan login dan tersimpan pada akun.
- Ulasan hanya untuk pembelian selesai; rating 1–5, teks, maksimal 3 foto.
- Admin dapat moderasi ulasan dengan menyimpan histori.

## FS-13 — CMS dan notifikasi lanjutan (tahap lanjutan)
- Pemilik mengelola banner, hero, About Us, kebijakan, alamat, jam toko, WhatsApp, dan tautan sosial tanpa perubahan kode.
- Notifikasi pelanggan/admin memiliki status baca, waktu, sumber, dan tautan terkait.
- Email konfirmasi dikirim saat pembayaran berhasil dikonfirmasi.
- WhatsApp otomatis dan live chat internal tidak termasuk tahap awal.
