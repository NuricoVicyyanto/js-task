# Task E15 — Capstone: Production-Ready Order API

> **Level:** Expert · **Estimasi:** 12–16 jam · **Topik:** arsitektur, HTTP API, SQLite, auth, cache, SSE, observability, testing, Docker, dokumentasi

## Tujuan

Membangun layanan pesanan Kopi Senja yang layak dioperasikan: aman, teruji, teramati, terdokumentasi, dan bisa dijalankan dengan satu perintah.

## Studi Kasus

Setelah melewati task arsitektur, API, database, keamanan, dan observability, Kopi Senja membutuhkan satu layanan pesanan yang benar-benar bisa dijalankan di server. Layanan ini dipakai kasir, admin, dan layar dapur, serta harus aman, terukur, dan bisa dilacak saat bermasalah.

Task ini menggabungkan **seluruh materi expert**. Kamu bebas memilih struktur internal, tetapi semua perilaku dan bukti kualitas di bawah wajib dipenuhi.

## Deliverable

```text
e15-order-api/
├── src/
│   ├── domain/
│   ├── ports/
│   ├── adapters/
│   ├── services/
│   ├── http/
│   └── index.js
├── migrations/
├── test/
├── openapi.yaml
├── Dockerfile
├── .env.example
├── .github/workflows/ci.yml
├── package.json
└── README.md
```

`README.md` milikmu memuat: cara menjalankan, variabel environment, daftar endpoint, contoh curl, arsitektur singkat, dan keputusan desain.

## Fitur Wajib

### 1. Menu

- `GET /api/menu` — daftar menu, bisa difilter `?kategori=`.
- `POST /api/admin/menu` — tambah menu (role admin).
- `PATCH /api/admin/menu/:id` — ubah harga/stok (role admin).
- Data tersimpan di SQLite, bukan JSON.

### 2. Pesanan

- `POST /api/orders` — role kasir/admin.
  - Validasi pelanggan, item, qty, stok.
  - Diskon `SENJA10` (10%, min 50.000) dan `SENJA20` (20%, min 100.000).
  - Pajak 11% setelah diskon.
  - Transaksi database: order, item, pengurangan stok.
- `GET /api/orders/:id` — detail order.
- `GET /api/admin/reports/sales` — total pendapatan per kategori (role admin).

### 3. Auth & keamanan

- `POST /api/auth/register`, `POST /api/auth/login`.
- Password scrypt + salt, verifikasi constant-time.
- Token HMAC dengan expiry; secret dari environment.
- RBAC: `kasir`, `admin`.
- Rate limit login 5/menit per IP.
- Security headers dan error envelope konsisten.
- Tidak ada secret di log, response, atau repository.

### 4. Realtime & cache

- `GET /events` — SSE untuk `order.created`.
- Cache `GET /api/menu` dengan TTL 30 detik dan invalidasi saat menu berubah.
- `X-Cache: HIT|MISS`.
- Batas client SSE 100; cleanup saat disconnect.

### 5. Operasional

- `GET /health/live`, `GET /health/ready`, `GET /metrics`.
- Log JSON dengan `requestId`, route pattern, status, durasi.
- Graceful shutdown `SIGTERM`/`SIGINT`.
- Environment: `PORT`, `DATABASE_PATH`, `AUTH_SECRET`, `LOG_LEVEL`.
- Jangan pernah memakai default secret di production; gagal start jika `AUTH_SECRET` tidak ada.

### 6. Kualitas

- Unit + integration test, coverage line ≥ 85%.
- Lint dan format check di CI.
- OpenAPI 3.1 mendokumentasikan semua endpoint.
- Dockerfile multi-stage, image non-root, healthcheck.
- CI menjalankan test, coverage, build image (atau minimal `docker build`).

## Kontrak API

### Login

```http
POST /api/auth/login
Content-Type: application/json

{"username":"kasir","password":"rahasia"}
```

```json
{ "token": "<token>", "role": "kasir" }
```

### Buat pesanan

```http
POST /api/orders
Authorization: Bearer <token>
Content-Type: application/json

{
  "pelanggan": "Nadia",
  "items": [
    { "menuId": 1, "qty": 2 },
    { "menuId": 2, "qty": 1 }
  ],
  "voucher": "SENJA10"
}
```

```json
{
  "id": "KS-1001",
  "subtotal": 60000,
  "diskon": 6000,
  "pajak": 5940,
  "total": 59940,
  "status": "baru"
}
```

### Error envelope

```json
{
  "error": "Pesan aman",
  "code": "KODE_MESIN",
  "requestId": "req-123"
}
```

## Ekspektasi & Skenario Penerimaan

| No | Skenario | Hasil |
| --- | --- | --- |
| 1 | Login kasir | 200, token dan role |
| 2 | Login password salah | 401, pesan generik |
| 3 | `GET /api/menu` tanpa token | 200 (publik) |
| 4 | `POST /api/orders` tanpa token | 401 |
| 5 | Buat order valid | 201, total `59940` |
| 6 | Stok berkurang | stok Espresso `10 → 8` |
| 7 | Stok tidak cukup | 409, tidak ada perubahan stok |
| 8 | Voucher `SENJA20` di bawah minimum | diskon `0` |
| 9 | Kasir akses endpoint admin | 403 |
| 10 | Login ke-6 dalam 1 menit | 429 + `Retry-After` |
| 11 | `GET /events` | event `connected`, lalu `order.created` |
| 12 | `GET /api/menu` dua kali | `X-Cache` MISS lalu HIT |
| 13 | `GET /health/ready` saat DB mati | 503 |
| 14 | `GET /metrics` | counter dan histogram bertambah |
| 15 | `SIGTERM` saat request aktif | request selesai, proses berhenti bersih |
| 16 | `AUTH_SECRET` tidak diset | proses menolak start |
| 17 | Coverage | ≥ 85% |
| 18 | `docker build` | image berhasil dibuat |

## Rubrik Penilaian

| Komponen | Bobot | Indikator |
| --- | --- | --- |
| Arsitektur & pemisahan layer | 15 | Domain bersih, port/adapter, service dapat diuji |
| Fungsionalitas pesanan | 25 | Perhitungan, stok, transaksi, voucher benar |
| Database & konsistensi | 15 | Skema, constraint, migration, rollback |
| Keamanan & auth | 15 | Hash, token, RBAC, secret, rate limit |
| Operasional | 10 | Log, metrics, health, shutdown, Docker |
| Testing | 10 | Unit + integration, coverage ≥ 85% |
| Dokumentasi | 10 | README + OpenAPI akurat dan bisa dijalankan |

Nilai maksimal **100**. Bonus maksimal **+10**.

## Ketentuan Non-Fungsional

- p95 latency endpoint lokal < 100 ms untuk 1.000 request berurutan.
- 100 request paralel tidak menghasilkan error 5xx.
- Tidak ada kebocoran memori setelah 1.000 request (heap stabil).
- Semua input divalidasi di boundary HTTP.
- Tidak ada `console.log` untuk log aplikasi.
- Tidak ada query string concatenation.
- Tidak ada data sensitif di response/list log.
- Build dan test berjalan dari checkout bersih.

## Checklist Sebelum Kumpul

- [ ] Semua endpoint pada kontrak berjalan.
- [ ] Transaksi rollback saat stok kurang.
- [ ] Voucher dan pajak benar.
- [ ] Auth + RBAC + rate limit bekerja.
- [ ] SSE broadcast dan cleanup.
- [ ] Cache hit/miss dan invalidasi.
- [ ] Log JSON, metrics, health.
- [ ] Graceful shutdown.
- [ ] Coverage ≥ 85%.
- [ ] `openapi.yaml` valid.
- [ ] Dockerfile non-root + healthcheck.
- [ ] README bisa diikuti dari nol.
- [ ] CI hijau.

## Bonus

1. Tambahkan load test (autocannon/k6) dan laporkan p95/p99.
2. Tambahkan tracing `traceparent` dan dashboard metrik.
3. Tambahkan backup/restore SQLite dan uji integritas.
4. Terapkan strategi deployment blue-green dan rollback.
5. Tambahkan audit log untuk aksi admin.
