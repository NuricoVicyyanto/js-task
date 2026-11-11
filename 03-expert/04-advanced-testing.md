# Task E04 — Advanced Testing: Unit, Integration, Mock

> **Level:** Expert · **Estimasi:** 4 jam · **Topik:** test pyramid, `node:test`, mock, integration test, coverage gate, test isolation

## Tujuan

Membangun test suite yang cepat, deterministik, dan memberi kepercayaan pada level yang berbeda: unit untuk logika, integration untuk HTTP + repository, serta mock untuk waktu dan kegagalan.

## Studi Kasus

Tim Kopi Senja ingin merilis aturan diskon dan endpoint pesanan baru. Sebelum rilis, pipeline harus membuktikan bahwa:

- aturan harga benar di semua batas,
- endpoint mengembalikan status dan bentuk response yang benar,
- kegagalan repository tidak menghasilkan pesanan setengah jadi,
- test tidak bergantung pada internet, waktu nyata, atau port tetap.

## Yang Harus Dibuat (Struktur)

```text
e04-testing/
├── src/
│   ├── service.js
│   ├── repository.js
│   └── server.js
├── test/
│   ├── unit.test.js
│   └── integration.test.js
└── package.json
```

## Aplikasi yang Diuji

- `service.js`: `createOrderService({ repo, clock })`.
- `repository.js`: in-memory atau JSON repository.
- `server.js`: HTTP handler dengan endpoint:
  - `GET /health`
  - `POST /orders`
  - `GET /orders/:id`

Bentuk response sukses `POST /orders`:

```json
{
  "id": "KS-1001",
  "total": 59940,
  "status": "baru"
}
```

Error:

```json
{ "error": "Menu tidak ditemukan", "code": "MENU_NOT_FOUND" }
```

## Test Wajib

### Unit test

1. Subtotal benar untuk beberapa item.
2. Diskon `SENJA10` tepat di batas 50000.
3. Diskon `SENJA20` tepat di batas 100000.
4. Voucher tidak valid menghasilkan diskon 0.
5. Pajak dihitung setelah diskon.
6. Qty 0 ditolak.
7. Menu tidak tersedia ditolak.
8. Repository gagal menyimpan → error, tidak ada order tersimpan.

Gunakan fake repository dan `clock` tetap. Jangan memakai `Date.now()` nyata.

### Integration test

9. `GET /health` → 200 `{ status: "ok" }`.
10. `POST /orders` valid → 201 dan bentuk response benar.
11. `POST /orders` dengan menu tidak ada → 404.
12. `POST /orders` body tidak valid → 422.
13. `GET /orders/:id` tidak ada → 404.
14. Dua request paralel tidak menghasilkan ID duplikat.

Server harus listen di port `0` (ephemeral), lalu ditutup di `after()`.

## Mock yang Wajib Dipakai

- `t.mock.method()` untuk repository yang melempar error.
- `t.mock.timers` untuk clock/id, bukan `setTimeout` nyata.
- Jangan memakai sleep untuk menunggu test.

## Ekspektasi Output

```text
✔ unit: subtotal beberapa item
✔ unit: diskon SENJA10 tepat batas
✔ unit: repository gagal menyimpan
✔ integration: POST /orders 201
✔ integration: POST /orders 422
✔ integration: GET /orders/xxx 404
ℹ tests 14
ℹ pass 14
ℹ fail 0
ℹ coverage line 90.1%
```

Jumlah test minimal **14** dan coverage line minimal **85%**.

## Ketentuan

- Gunakan `node:test` dan `node:assert/strict`.
- Jangan memakai internet atau API eksternal.
- Setiap test harus bisa berjalan sendiri dan berulang.
- Data test harus dibuat di dalam test/fixture, bukan state global yang dipakai bersama.
- Server dan resource harus ditutup di `after`/`afterEach`.
- Jangan menguji detail implementasi privat.
- Test harus gagal jika perilaku bisnis berubah.

## Kasus Batas

| Kasus | Harapan |
| --- | --- |
| Body kosong | 422, pesan jelas |
| JSON tidak valid | 400 |
| Item qty negatif | 422 |
| ID order duplikat | dicegah, bukan menimpa |
| Repository error | 500, tidak ada order setengah jadi |
| Request paralel | ID unik |

## Checklist Sebelum Kumpul

- [ ] Minimal 14 test lulus.
- [ ] Unit dan integration terpisah.
- [ ] Fake repo dan mock timer dipakai.
- [ ] Port ephemeral dan server ditutup.
- [ ] Coverage ≥ 85%.
- [ ] Tidak ada test yang bergantung urutan.
- [ ] Output dan coverage sesuai target.

## Bonus

1. Tambahkan test properti sederhana untuk aturan diskon (100 kombinasi acak dengan seed tetap).
2. Tambahkan contract test yang memvalidasi bentuk JSON response.
3. Ukur durasi test dan pastikan seluruh suite < 5 detik.
