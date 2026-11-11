# Task E06 — Node HTTP REST API

> **Level:** Expert · **Estimasi:** 5 jam · **Topik:** `node:http`, routing, middleware, error envelope, request ID, graceful shutdown

## Tujuan

Membangun REST API tanpa framework, dengan routing, validasi, status code, error yang konsisten, dan shutdown yang bersih.

## Studi Kasus

Kopi Senja membutuhkan API internal untuk aplikasi kasir. Tim memilih `node:http` agar tidak menambah dependency dan agar setiap lapisan terlihat jelas. API harus siap dipanggil oleh frontend dan mudah diuji.

## Yang Harus Dibuat (File)

```text
e06-http-api/
├── server.js
├── router.js
├── handlers.js
└── data.js
```

## Endpoint Wajib

| Method | Path | Sukses | Error yang diuji |
| --- | --- | --- | --- |
| GET | `/health` | 200 `{ "status": "ok" }` | — |
| GET | `/api/menu` | 200 array menu | 405 jika method lain |
| POST | `/api/orders` | 201 `{ id, total }` | 400, 404, 422, 413 |
| GET | `/api/orders/:id` | 200 detail order | 404 |

### Contoh request

```bash
curl -i http://localhost:3000/health
```

```http
HTTP/1.1 200 OK
content-type: application/json; charset=utf-8
x-request-id: req-1

{"status":"ok"}
```

### `POST /api/orders`

```json
{
  "pelanggan": "Nadia",
  "items": [
    { "menuId": 1, "qty": 2 },
    { "menuId": 2, "qty": 1 }
  ],
  "voucher": "SENJA10"
}
```

Response `201`:

```json
{
  "id": "KS-1001",
  "total": 59940
}
```

## Perilaku Wajib

### Routing

- Dukung path parameter `:id`.
- Query string diabaikan untuk routing.
- Trailing slash dinormalisasi.
- Method tidak didukung → `405` + header `Allow`.

### Request body

- Hanya `application/json` yang diterima untuk `POST`; selain itu `415`.
- Batas body **1 MB**; lebih dari itu `413`.
- JSON tidak valid → `400`.
- Field wajib divalidasi → `422`.

### Error envelope

Semua error memakai bentuk:

```json
{
  "error": "Pesan yang aman ditampilkan",
  "code": "KODE_MESIN",
  "requestId": "req-123"
}
```

Jangan pernah mengirim stack trace ke client. Log stack trace di server.

### Request ID

- Ambil dari header `x-request-id` jika ada dan valid.
- Jika tidak ada, buat ID acak.
- Sertakan di response header dan body error.
- ID yang mengandung karakter aneh harus diganti, bukan dipakai mentah.

### Graceful shutdown

- Tangani `SIGINT` dan `SIGTERM`.
- Berhenti menerima koneksi baru.
- Tunggu request aktif selesai maksimal 5 detik.
- Tutup server, lalu keluar dengan kode `0`.

## Ekspektasi Output

```text
GET /health -> 200 {"status":"ok"}
GET /api/menu -> 200 4 menu
POST /api/orders -> 201 {"id":"KS-1001","total":59940}
GET /api/orders/KS-1001 -> 200
POST /api/orders (menu 999) -> 404 MENU_NOT_FOUND
POST /api/orders (qty 0) -> 422 VALIDATION_ERROR
POST /api/orders (JSON rusak) -> 400 INVALID_JSON
PUT /api/menu -> 405 METHOD_NOT_ALLOWED (Allow: GET)
```

## Kasus Uji

| Skenario | Status |
| --- | --- |
| Body > 1 MB | 413 |
| Content-Type `text/plain` | 415 |
| Request ID berisi `<script>` | diganti ID aman |
| Route tidak ada | 404 |
| Server dimatikan saat request berjalan | request selesai, lalu proses berhenti |

## Ketentuan

- Dilarang memakai Express/Fastify/Koa.
- Jangan memakai `eval` atau `new Function` untuk routing.
- Jangan menulis seluruh response dengan string concatenation manual tanpa `JSON.stringify`.
- Handler tidak boleh mengakses `req`/`res` secara global.
- Error tak terduga → `500` dengan pesan generik.
- Jangan mencatat body yang mengandung password/token.

## Checklist Sebelum Kumpul

- [ ] Semua endpoint berjalan.
- [ ] Status code dan error envelope konsisten.
- [ ] Batas body dan content-type diterapkan.
- [ ] Request ID aman dan diteruskan.
- [ ] 405 menyertakan header `Allow`.
- [ ] Graceful shutdown bekerja.
- [ ] Output sesuai contoh.

## Bonus

1. Tambahkan ETag dan `304 Not Modified` untuk `GET /api/menu`.
2. Tambahkan kompresi gzip untuk response besar.
3. Tambahkan pagination dan filter kategori pada `/api/menu`.
