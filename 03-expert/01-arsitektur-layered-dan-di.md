# Task E01 — Arsitektur Layered & Dependency Injection

> **Level:** Expert · **Estimasi:** 3 jam · **Topik:** layered architecture, dependency inversion, repository pattern, composition root, testability

## Tujuan

Merancang aplikasi kasir yang **tidak bergantung pada detail implementasi**. Domain tidak boleh tahu tentang file, HTTP, atau database. Service menerima dependency dari luar, sehingga bisa diuji dengan fake.

## Studi Kasus

Kopi Senja akan memakai satu logika pesanan untuk tiga channel: CLI, API, dan aplikasi web. Jika logika bisnis ditulis langsung di handler, setiap channel akan menduplikasi aturan diskon, pajak, dan validasi. Tim meminta arsitektur berlapis dengan dependency injection.

## Struktur Wajib

```text
e01-architecture/
├── src/
│   ├── domain/
│   │   ├── order.js
│   │   └── pricing.js
│   ├── ports/
│   │   ├── menuRepository.js
│   │   └── orderRepository.js
│   ├── adapters/
│   │   ├── inMemoryMenuRepository.js
│   │   └── inMemoryOrderRepository.js
│   ├── services/
│   │   └── orderService.js
│   ├── composition.js
│   └── index.js
└── README.md
```

## Aturan Layer

| Layer | Boleh Bergantung Pada | Tidak Boleh |
| --- | --- | --- |
| `domain` | tidak ada (pure JavaScript) | fs, HTTP, DOM, database |
| `ports` | domain (tipe/JSDoc) | implementasi konkret |
| `services` | domain + ports | adapter, fs, HTTP |
| `adapters` | ports + domain | service |
| `composition` | semua layer | logika bisnis |

Gunakan JSDoc untuk mendefinisikan kontrak port:

```js
/**
 * @typedef {Object} MenuRepository
 * @property {(id: number) => Promise<Object|null>} findById
 * @property {() => Promise<Object[]>} findAll
 */
```

## Domain

`pricing.js` harus menyediakan fungsi murni:

- `hitungSubtotal(items)`
- `hitungDiskon(subtotal, voucher)`
- `hitungPajak(setelahDiskon)`
- `hitungTotal({ subtotal, diskon, pajak })`

Aturan:

- `SENJA10`: 10% jika subtotal ≥ 50000.
- `SENJA20`: 20% jika subtotal ≥ 100000.
- Pajak 11% dari `subtotal - diskon`.
- Semua pembulatan memakai `Math.round`.

## Service

`createOrderService({ menuRepo, orderRepo, clock })` mengembalikan:

| Method | Tugas |
| --- | --- |
| `buatPesanan({ pelanggan, items, voucher })` | validasi, hitung, simpan, kembalikan order |
| `ambilPesanan(id)` | mengambil order dari repository |
| `daftarPesanan()` | semua order |

Aturan validasi:

- `pelanggan` wajib diisi.
- `items` minimal 1 dan setiap `qty > 0`.
- Menu harus ada dan `tersedia !== false`.
- Qty tidak boleh melebihi `stok` jika stok tersedia.
- ID order dibuat dari `clock`/repository, bukan `Date.now()` di dalam service.
- Service tidak boleh mencetak ke console.

## Dependency Injection

- `orderService.js` hanya menerima objek dependency; tidak melakukan `new InMemoryMenuRepository()`.
- `composition.js` adalah satu-satunya tempat merangkai adapter + service.
- `index.js` memanggil `composition.js` dan mencetak hasil.

## Ekspektasi Output

Gunakan `clock` tetap yang menghasilkan ID `KS-1001` dan waktu `2026-11-11T14:30:00Z`.

```text
Pesanan KS-1001 dibuat
Pelanggan: Nadia
Subtotal: Rp60000
Diskon: Rp6000
Pajak: Rp5940
Total: Rp59940
Tersimpan: 1 pesanan
```

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| Item tidak ada di menu | error validasi, tidak tersimpan |
| Menu `tersedia: false` | error validasi |
| Qty `0` | error validasi |
| Voucher tidak valid | diskon `0`, pesanan tetap dibuat |
| Repository gagal menyimpan | error diteruskan, tidak ada order setengah jadi |
| Service diuji dengan fake repo | tidak perlu file/DB nyata |

## Ketentuan

- Domain tidak boleh memakai `async` kecuali memang diperlukan; pricing harus sinkron dan pure.
- Service hanya bergantung pada port, bukan adapter.
- Tidak boleh ada `import fs` atau `import http` di domain/service.
- ID dan waktu harus bisa ditentukan dari luar (deterministik).
- Jangan memakai singleton global.
- Semua error validasi harus jelas dan konsisten.

## Checklist Sebelum Kumpul

- [ ] Batas layer dipatuhi.
- [ ] Port didefinisikan dan dipakai service.
- [ ] Adapter bisa diganti tanpa mengubah service.
- [ ] Service bisa diuji tanpa filesystem.
- [ ] ID/waktu deterministik.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Buat `composition.production.js` dan `composition.test.js` dengan adapter berbeda.
2. Tambahkan decorator logging pada service tanpa mengubah domain.
3. Buat test yang mengganti `orderRepo` dengan fake yang melempar error.
