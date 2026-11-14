# ERD Konseptual — Unnie Vie Store

**Versi:** 0.1  
**Status:** Konseptual, perlu validasi sebelum migration

Diagram berikut menunjukkan relasi inti, bukan seluruh kolom atau seluruh tabel pendukung.

```mermaid
erDiagram
    PRODUCT_GROUPS ||--o{ PRODUCTS : groups
    PRODUCT_CATEGORIES ||--o{ PRODUCTS : categorizes
    PRODUCTS ||--|{ PRODUCT_VARIANTS : has
    PRODUCT_VARIANTS ||--|| STOCK_BALANCES : balance
    PRODUCT_VARIANTS ||--o{ STOCK_MOVEMENTS : movement
    PRODUCT_VARIANTS ||--o{ STOCK_RESERVATIONS : reserved

    SUPPLIERS ||--o{ PURCHASES : supplies
    PURCHASES ||--|{ PURCHASE_ITEMS : contains
    PURCHASES ||--o{ GOODS_RECEIPTS : receives
    GOODS_RECEIPTS ||--|{ GOODS_RECEIPT_ITEMS : contains
    PRODUCT_VARIANTS ||--o{ PURCHASE_ITEMS : purchased
    PRODUCT_VARIANTS ||--o{ GOODS_RECEIPT_ITEMS : received

    CUSTOMERS ||--o{ CUSTOMER_ADDRESSES : owns
    CUSTOMERS ||--o{ ORDERS : places
    ORDERS ||--|{ ORDER_ITEMS : contains
    PRODUCT_VARIANTS ||--o{ ORDER_ITEMS : ordered
    ORDERS ||--o{ ORDER_STATUS_HISTORIES : history
    ORDERS ||--o{ PAYMENTS : payment
    PAYMENTS ||--o{ PAYMENT_PROOFS : evidence
    ORDERS ||--o{ SHIPMENTS : ships
    ORDERS ||--o{ RETURN_REQUESTS : returns
    RETURN_REQUESTS ||--o{ RETURN_ITEMS : includes
    RETURN_REQUESTS ||--o{ RETURN_EVIDENCES : evidence

    CUSTOMERS ||--o{ POINT_TRANSACTIONS : earns
    CUSTOMERS ||--o{ CUSTOMER_VOUCHERS : receives
    VOUCHERS ||--o{ CUSTOMER_VOUCHERS : assigned
    CUSTOMERS ||--o{ REVIEWS : writes
    PRODUCTS ||--o{ REVIEWS : reviewed
```

## Catatan
- ERD ini sengaja berfokus pada hubungan domain inti.
- `stock_reservations` terpisah dari `stock_movements` karena alokasi bukan pergerakan fisik.
- Order item menyimpan snapshot produk/varian/harga/HPP untuk menjaga histori.
- Alamat pengiriman order harus disimpan sebagai snapshot pada order.
- Implementasi final perlu menambahkan relasi akun admin, role/permission, cart, wishlist, voucher redemption, shipment history, CMS, notification, activity log, dan backup log.
- Semua foreign key, unique constraint, nullable rule, cascade behavior, dan index harus ditentukan pada desain migration.
