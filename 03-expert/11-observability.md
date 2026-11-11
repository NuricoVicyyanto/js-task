# Task E11 — Observability: Logging, Metrics, Health

> **Level:** Expert · **Estimasi:** 4 jam · **Topik:** structured logging, correlation ID, metrics Prometheus, readiness, redaction

## Tujuan

Membuat aplikasi yang bisa dioperasikan: log terstruktur, metrik yang bisa dibaca mesin, dan health check yang membedakan “hidup” dan “siap melayani”.

## Studi Kasus

Insiden Kopi Senja tidak bisa ditelusuri karena log berupa teks bebas dan tidak ada request ID. Tim meminta observability minimal: setiap request punya ID, durasi, status; log berbentuk JSON; metrik tersedia di `/metrics`; readiness gagal jika database tidak bisa diakses.

## Yang Harus Dibuat (File)

```text
e11-observability/
├── logger.js
├── metrics.js
├── server.js
└── demo.js
```

## 1. `logger.js`

`log(level, message, fields)` mencetak **satu baris JSON** ke stdout:

```json
{"level":"info","time":"2026-11-11T14:30:00.000Z","requestId":"req-1","message":"request selesai","method":"GET","path":"/api/menu","status":200,"durationMs":12}
```

Aturan:

- Field wajib: `level`, `time`, `message`.
- `requestId` disertakan jika tersedia.
- Field sensitif (`password`, `token`, `authorization`, `cookie`) diredaksi menjadi `"***"` secara rekursif.
- Error diserialisasi menjadi `{ name, message, stack }`; stack hanya pada level `error`.
- Jangan memakai `console.log` dengan string bebas untuk log aplikasi.

Level yang didukung: `debug`, `info`, `warn`, `error`.

## 2. `metrics.js`

Implementasikan:

| Fungsi | Tugas |
| --- | --- |
| `counter(name, labels)` | menambah 1 |
| `gauge(name, value, labels)` | menetapkan nilai |
| `histogram(name, value, labels, buckets)` | mencatat distribusi |
| `renderPrometheus()` | menghasilkan teks format Prometheus |

Contoh output:

```text
kopi_http_requests_total{method="GET",route="/api/menu",status="200"} 1
kopi_http_request_duration_ms_bucket{route="/api/menu",le="50"} 1
kopi_http_request_duration_ms_bucket{route="/api/menu",le="100"} 1
kopi_http_request_duration_ms_bucket{route="/api/menu",le="+Inf"} 1
kopi_http_request_duration_ms_sum{route="/api/menu"} 12
kopi_http_request_duration_ms_count{route="/api/menu"} 1
```

Aturan:

- Label tidak boleh memakai ID mentah (cardinality meledak). Gunakan pola route `"/api/orders/:id"`.
- Nama metrik mengikuti `snake_case`.
- Bucket default: `[10, 25, 50, 100, 250, 500, 1000]` ms.
- Escape `"` dan `\` pada nilai label.

## 3. `server.js`

Middleware mencatat:

- `requestId` dari header `x-request-id` atau dibuat acak.
- Waktu mulai dan durasi.
- Method, route pattern, status.
- Log satu baris setelah response selesai.
- Metrik `http_requests_total` dan histogram durasi.

Endpoint:

| Path | Perilaku |
| --- | --- |
| `/health/live` | 200 selama proses hidup, tanpa dependency |
| `/health/ready` | 200 jika DB ping berhasil, 503 jika gagal |
| `/metrics` | teks Prometheus |

## Ekspektasi Output

Log:

```json
{"level":"info","time":"...","requestId":"req-1","message":"request selesai","method":"GET","path":"/api/menu","status":200,"durationMs":12}
```

Metrics:

```text
kopi_http_requests_total{method="GET",route="/api/menu",status="200"} 1
kopi_http_request_duration_ms_count{route="/api/menu"} 1
```

Health:

```text
GET /health/live -> 200 {"status":"ok"}
GET /health/ready -> 200 {"status":"ready"}
DB mati -> 503 {"status":"not_ready"}
```

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| Request dengan `x-request-id` | ID yang sama muncul di log |
| Request tanpa ID | ID acak dibuat |
| Field password di nested object | diredaksi |
| 100 request ke route yang sama | satu time series, bukan 100 |
| Route dengan ID | label memakai pola `:id` |
| DB gagal | readiness 503, liveness tetap 200 |
| Metrics setelah request | counter dan histogram bertambah |

## Ketentuan

- Jangan mencatat body request mentah.
- Jangan mencatat token/password.
- Jangan memakai `console.log` untuk log terstruktur.
- Jangan memakai ID pengguna sebagai label metrik.
- Jangan mengembalikan HTML dari endpoint JSON.
- Jangan membuat metrics endpoint bergantung pada database.

## Checklist Sebelum Kumpul

- [ ] Log berupa JSON valid per baris.
- [ ] Correlation ID diteruskan.
- [ ] Redaksi rekursif bekerja.
- [ ] Counter, gauge, histogram tersedia.
- [ ] Route label tidak memakai ID mentah.
- [ ] Liveness dan readiness berbeda.
- [ ] Output sesuai contoh.

## Bonus

1. Teruskan `traceparent` (W3C Trace Context) dan tampilkan di log.
2. Tambahkan sampling log debug 10%.
3. Buat aturan alert: error rate > 5% selama 5 menit.
