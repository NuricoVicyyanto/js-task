# Task E07 — Database & Transaksi

> **Level:** Expert · **Estimasi:** 5 jam · **Topik:** `node:sqlite`, migration, prepared statement, foreign key, transaction, index

## Tujuan

Menyimpan data menu dan pesanan secara persisten dengan skema yang benar, transaksi atomik, dan query yang ter-index.

## Studi Kasus

Kopi Senja beralih dari file JSON ke SQLite. Setiap pesanan harus mengurangi stok dan mencatat item secara **atomik**: jika satu item gagal, tidak boleh ada stok yang terlanjur berkurang atau order setengah jadi.

Gunakan `node:sqlite` (Node.js 22+).

## Yang Harus Dibuat (Struktur)

```text
e07-database/
├── db.js
├── migrations/
│   ├── 001_init.sql
│   └── 002_index.sql
├── seed.js
└── demo.js
```

## Skema

```sql
CREATE TABLE menu (
  id INTEGER PRIMARY KEY,
  nama TEXT NOT NULL UNIQUE,
  kategori TEXT NOT NULL CHECK (kategori IN ('Minuman', 'Makanan')),
  harga INTEGER NOT NULL CHECK (harga > 0),
  stok INTEGER NOT NULL DEFAULT 0 CHECK (stok >= 0)
);

CREATE TABLE orders (
  id TEXT PRIMARY KEY,
  pelanggan TEXT NOT NULL,
  total INTEGER NOT NULL CHECK (total >= 0),
  created_at TEXT NOT NULL
);

CREATE TABLE order_items (
  order_id TEXT NOT NULL REFERENCES orders(id) ON DELETE CASCADE,
  menu_id INTEGER NOT NULL REFERENCES menu(id),
  qty INTEGER NOT NULL CHECK (qty > 0),
  harga INTEGER NOT NULL CHECK (harga > 0),
  PRIMARY KEY (order_id, menu_id)
);
```

Tambahkan index:

```sql
CREATE INDEX idx_menu_kategori ON menu(kategori);
```

## Migration

- Tabel `schema_migrations(versi INTEGER PRIMARY KEY, nama TEXT, dijalankan_at TEXT)`.
- Migration dijalankan berurutan dan hanya sekali.
- Jika migration gagal, transaksi di-rollback.
- `db.js` mengekspor `jalankanMigrasi(db)`.

## Fungsi Wajib

| Fungsi | Tugas |
| --- | --- |
| `tambahMenu(db, menu)` | insert prepared statement |
| `cariMenuKategori(db, kategori)` | select dengan index |
| `buatPesanan(db, { id, pelanggan, items })` | transaksi: insert order, insert items, kurangi stok |
| `ambilPesanan(db, id)` | join order + items |
| `rollbackDemo(db)` | simulasi kegagalan di tengah transaksi |

## Aturan Transaksi

`buatPesanan` harus:

1. `BEGIN IMMEDIATE`.
2. Insert ke `orders`.
3. Untuk setiap item: cek stok, insert `order_items`, kurangi `stok`.
4. `COMMIT`.
5. Jika ada error (stok kurang, constraint, dll), `ROLLBACK` dan lempar error.

Tidak boleh ada pengurangan stok yang tersimpan saat transaksi gagal.

## Data Seed

5 menu seperti task sebelumnya. Stok awal Espresso `10`.

## Ekspektasi Output

```text
Migrasi: 3 tabel domain + schema_migrations
Insert menu: 5
Order KS-001 total: Rp60000
Stok Espresso: 8
Rollback: stok tetap 8
Query plan: SEARCH menu USING INDEX idx_menu_kategori
Foreign key aktif: true
```

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| Pesanan valid | order + items tersimpan, stok berkurang |
| Stok kurang | rollback, stok tidak berubah |
| Qty 0 | constraint gagal, rollback |
| Menu tidak ada | foreign key gagal, rollback |
| Migration dijalankan 2× | tidak menduplikasi tabel/data |
| Hapus order | `order_items` ikut terhapus |
| Query kategori | memakai index |

## Ketentuan

- Semua query berparameter memakai prepared statement (`?`), bukan string interpolation.
- Aktifkan `PRAGMA foreign_keys = ON`.
- Gunakan `PRAGMA journal_mode = WAL`.
- Jangan memakai `db.exec()` untuk input pengguna.
- Tutup database di akhir program.
- Jangan menyimpan harga sebagai float; gunakan integer rupiah.
- Jangan menelan error transaksi.

## Checklist Sebelum Kumpul

- [ ] Skema memiliki constraint yang sesuai.
- [ ] Migration berjalan idempoten.
- [ ] Transaksi rollback saat gagal.
- [ ] Stok tidak negatif.
- [ ] Foreign key aktif.
- [ ] Query plan memakai index.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Buat migration runner dengan perintah `up` dan `down`.
2. Tambahkan laporan pendapatan per kategori memakai `GROUP BY`.
3. Buat backup database dan verifikasi integritas dengan `PRAGMA integrity_check`.
