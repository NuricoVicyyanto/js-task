# Level 03 — Expert — 15 Task JavaScript Produksi

Folder ini berisi **15 task** untuk siswa yang sudah nyaman dengan JavaScript modern dan ingin membangun sistem yang aman, teruji, dan bisa dioperasikan. Fokusnya bukan sintaks baru, melainkan **engineering judgment**: arsitektur, konkurensi, performa, keamanan, observabilitas, dan rilis.

## Prasyarat

Siswa sudah mampu:

- Menulis ES Modules dan memisahkan layer.
- Menggunakan class, closure, higher-order function, dan functional pipeline.
- Menangani error, retry, Promise combinator, dan `fetch`.
- Menulis unit test dengan `node:test`.
- Membuat CLI dengan file I/O.
- Membangun state management DOM sederhana.

Jika belum, selesaikan [Level 02 — Intermediate](../02-intermediate/README.md).

## Prasyarat Tooling

| Kebutuhan | Keterangan |
| --- | --- |
| Node.js | **22+** untuk `node:sqlite` dan `node:test` modern |
| npm | Untuk Task E12 dan E14 (dependency build tooling) |
| Docker | Untuk Task E15 (opsional saat latihan, wajib untuk penerimaan) |
| Git & GitHub | Untuk CI/CD dan review |
| Editor | VS Code dengan integrasi terminal |

## Hasil Belajar

Setelah 15 task, siswa mampu:

1. Merancang arsitektur berlapis dengan dependency injection.
2. Menangani pekerjaan CPU-bound dan konkurensi tanpa memblokir event loop.
3. Mengukur dan mengoptimalkan performa berdasarkan data.
4. Menulis test unit, integration, dan mock yang deterministik.
5. Menerapkan pertahanan terhadap XSS, prototype pollution, dan SQL injection.
6. Membangun REST API, autentikasi, RBAC, database transaksional, SSE, cache, dan rate limit.
7. Menyediakan logging, metrics, health check, CI/CD, dan build produksi.
8. Mengoperasikan aplikasi lewat Docker dengan dokumentasi yang jelas.

## Peta 15 Task

| No | Task | Topik Inti | Estimasi |
| --- | --- | --- | --- |
| 01 | [Arsitektur Layered & DI](./01-arsitektur-layered-dan-di.md) | layer, port/adapter, DI, composition root | 3 jam |
| 02 | [Worker Threads & Backpressure](./02-worker-threads-dan-backpressure.md) | worker, bounded queue, event loop | 3–4 jam |
| 03 | [Performance & Memory](./03-performance-dan-memory.md) | benchmark, Big-O, index, memori | 3 jam |
| 04 | [Advanced Testing](./04-advanced-testing.md) | unit, integration, mock, coverage | 4 jam |
| 05 | [Security Hardening](./05-security-hardening.md) | XSS, prototype pollution, SQLi, secret | 4 jam |
| 06 | [Node HTTP REST API](./06-http-rest-api.md) | routing, middleware, error envelope | 5 jam |
| 07 | [Database & Transaksi](./07-database-dan-transaksi.md) | SQLite, migration, transaksi, index | 5 jam |
| 08 | [Auth & RBAC](./08-auth-dan-rbac.md) | scrypt, HMAC, expiry, role | 5 jam |
| 09 | [Realtime SSE](./09-realtime-sse.md) | `text/event-stream`, broadcast, cleanup | 4 jam |
| 10 | [Caching & Rate Limiting](./10-caching-dan-rate-limiting.md) | LRU, TTL, sliding window, 429 | 4 jam |
| 11 | [Observability](./11-observability.md) | log JSON, metrics, health | 4 jam |
| 12 | [CI/CD & Code Quality](./12-ci-cd-dan-code-quality.md) | GitHub Actions, lint, coverage, artifact | 3–4 jam |
| 13 | [Design Patterns](./13-design-patterns.md) | strategy, factory, observer, adapter | 4 jam |
| 14 | [Build Tooling & Bundling](./14-build-tooling-dan-bundling.md) | Vite, env, code splitting, budget | 4 jam |
| 15 | [Capstone: Production API](./15-capstone-production-api.md) | gabungan seluruh materi | 12–16 jam |

**Total estimasi:** ±70 jam.

## Rencana Kelas 10 Sesi

| Sesi | Materi | Fokus |
| --- | --- | --- |
| 1 | E01–E02 | Arsitektur dan konkurensi |
| 2 | E03 | Performa terukur |
| 3 | E04 | Testing lanjutan |
| 4 | E05 | Keamanan |
| 5 | E06–E07 | HTTP API dan database |
| 6 | E08 | Auth dan RBAC |
| 7 | E09–E10 | Realtime, cache, rate limit |
| 8 | E11–E12 | Observability dan CI/CD |
| 9 | E13–E14 | Design pattern dan build |
| 10 | E15 | Presentasi dan review capstone |

## Standar Pengerjaan

- Setiap task harus punya `README.md` proyek yang bisa diikuti dari nol.
- Sertakan perintah menjalankan, environment variable, dan contoh output.
- Jangan menaruh secret di repository.
- Jangan mengklaim performa/keamanan tanpa bukti pengukuran atau test.
- Gunakan dependency seminimal mungkin; setiap dependency harus dijelaskan alasannya.
- Semua error harus punya pesan yang aman ditampilkan dan kode mesin yang konsisten.
- Kode yang tidak bisa diuji ulang di checkout bersih dianggap belum selesai.

## Penilaian

Rubrik lengkap ada di [docs/rubrik-penilaian.md](../docs/rubrik-penilaian.md). Komponen khusus expert:

| Komponen | Bobot |
| --- | --- |
| Perilaku dan output | 35 |
| Arsitektur & pemisahan tanggung jawab | 20 |
| Keamanan & penanganan error | 15 |
| Testing & bukti kualitas | 15 |
| Operasional & dokumentasi | 15 |

Capstone E15 memiliki rubrik tersendiri dan dihitung **2×** dalam nilai level expert.

## Peringatan Etika

Materi keamanan (E05, E08) hanya boleh diuji pada sistem milik sendiri atau lab yang diizinkan. Jangan memakai teknik di sini terhadap layanan orang lain tanpa izin tertulis.
