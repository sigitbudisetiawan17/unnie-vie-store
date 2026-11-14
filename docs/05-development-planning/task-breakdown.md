# Task Breakdown — Unnie Vie Store

**Versi:** 0.1  
**Status:** Draft rencana implementasi  
**Tanggal:** 14 November 2026

## Prinsip pengerjaan
- Ikuti urutan Specification → Planning → Task Breakdown → Implementation → Verification.
- Selesaikan fondasi teknis sebelum fitur bisnis.
- Setiap milestone ditutup dengan pemeriksaan kode, pengujian, dan review.
- Kerjakan pada feature branch dan gabungkan melalui Pull Request.
- Jangan mengubah `main` secara langsung.

## M-01 — Project foundation
**Tujuan:** memastikan struktur Laravel, environment, standar kode, autentikasi admin, RBAC, dan Activity Log siap.

Tugas:
1. Audit struktur Laravel 13, PHP 8.5, dependency, dan konfigurasi.
2. Periksa `.env.example`, `.gitignore`, README, AGENTS, dan panduan agent.
3. Pastikan koneksi MySQL dan migration bawaan berjalan.
4. Tetapkan struktur folder dan konvensi kode.
5. Tentukan pendekatan admin authentication dan RBAC setelah audit dependency.
6. Implementasikan Activity Log dasar.
7. Siapkan testing baseline dan CI yang sesuai kebutuhan.

**Verifikasi:** aplikasi dapat dijalankan, test baseline lulus, migration bawaan aman, login admin/RBAC teruji, Activity Log tidak menyimpan rahasia.

## M-02 — Product catalog
**Tujuan:** pengelolaan kelompok, kategori, produk, varian, SKU, foto, dan diskon.

**Verifikasi:** CRUD, validasi, unique SKU, upload foto, nonaktif produk historis, dan snapshot harga teruji.

## M-03 — Supplier dan inventory
**Tujuan:** supplier, purchase, goods receipt parsial, saldo stok, stock movement, adjustment, dan low-stock alert.

**Verifikasi:** penerimaan parsial, pencegahan receipt ganda, row locking, stok tidak negatif, dan adjustment terhadap reserved teruji.

## M-04 — Offline sales
**Tujuan:** transaksi toko fisik, pembayaran, pengurangan stok, dan struk.

**Verifikasi:** perhitungan backend, stok berkurang satu kali, metode pembayaran tersimpan, dan laporan transaksi sesuai.

## M-05 — Online order
**Tujuan:** customer auth, cart, address, checkout, reservation, payment proof, verifikasi, dan shipping.

**Verifikasi:** alokasi atomik, batas 12 jam, pengecualian bukti menunggu verifikasi, idempotency, dan status order teruji.

## M-06 — Reporting dan QA
**Tujuan:** dashboard, laporan penjualan/keuntungan/stok, ekspor, integrasi, dan perbaikan bug.

**Verifikasi:** hasil laporan cocok dengan data sumber; seluruh test suite relevan lulus.

## M-07 — CRM dan fitur lanjutan
**Tujuan:** poin, membership, voucher, wishlist, review, retur/refund lengkap, CMS, notifikasi, backup/restore.

**Verifikasi:** ledger poin, aturan inaktivitas, voucher, moderasi, alur retur, akses file privat, dan backup/restore teruji.

## Definition of Done
Sebuah tugas dinyatakan selesai jika:
- Implementasi memenuhi acceptance criteria.
- Validasi dan otorisasi backend tersedia.
- Operasi data kritis aman dari duplikasi dan partial commit.
- Automated tests ditambahkan dan lulus.
- Pint/formatting dan pemeriksaan kode lulus.
- Dokumentasi/API contract diperbarui bila relevan.
- Pull Request telah direview dan tidak menyertakan `.env`, kredensial, `vendor`, `node_modules`, atau database lokal.
