# Task E10 — Caching & Rate Limiting

> **Level:** Expert · **Estimasi:** 4 jam · **Topik:** LRU cache, TTL, invalidation, sliding window, `429`, `Retry-After`

## Tujuan

Mengurangi beban server dengan cache yang terbatas dan melindungi endpoint dengan rate limit yang adil, tanpa membocorkan memori.

## Studi Kasus

Endpoint menu Kopi Senja dipanggil ratusan kali per menit, padahal data hanya berubah beberapa kali sehari. Sebaliknya, endpoint login sering diserang percobaan berulang. Tim meminta cache untuk menu dan rate limit untuk login.

## Yang Harus Dibuat (File)

```text
e10-cache/
├── lru-cache.js
├── rate-limit.js
├── server.js
└── demo.js
```

## 1. `LRUCache`

Class dengan konfigurasi `{ maxSize, ttlMs, clock }`.

| Method | Tugas |
| --- | --- |
| `get(key)` | mengembalikan nilai atau `undefined`; perbarui urutan LRU |
| `set(key, value)` | menyimpan; evict item paling lama jika penuh |
| `delete(key)` | menghapus key |
| `clear()` | mengosongkan cache |
| `stats()` | `{ hits, misses, evictions, size }` |

Aturan:

- `maxSize` wajib positif.
- Item kedaluwarsa dianggap miss dan dihapus saat diakses.
- `get` yang berhasil menaikkan `hits`; gagal menaikkan `misses`.
- Eviction terjadi saat ukuran melebihi `maxSize`.
- Gunakan `Map` agar urutan insertion dapat dimanfaatkan.
- `clock` dapat diinjeksi agar test deterministik.

## 2. `rateLimit({ limit, windowMs, clock })`

Mengembalikan fungsi `(key) => { allowed, remaining, retryAfterSec }`.

- Gunakan sliding window berbasis timestamp.
- Maksimal `limit` request per `key` dalam `windowMs`.
- Request ke-`limit + 1` → `allowed: false`, `retryAfterSec` dibulatkan ke atas.
- Simpan timestamp di `Map<key, number[]>`.
- Bersihkan timestamp lama agar memori tidak tumbuh tanpa batas.
- `key` bisa IP atau user ID.

## 3. Integrasi Server

- `GET /api/menu` memakai cache.
  - Cache hit → header `X-Cache: HIT`.
  - Cache miss → `X-Cache: MISS`, simpan hasil.
- `POST /api/admin/menu` menginvalidasi cache.
- `POST /api/login` memakai rate limit 5 request per 60 detik per IP.
- Saat limit terlampaui → `429` + `Retry-After`.

## Ekspektasi Output

```text
Cache miss: 120 ms
Cache hit: 1 ms
Hits: 1, Misses: 1
X-Cache: HIT
Rate limit 1-5: allowed
Rate limit 6: blocked, retry after 60s
Setelah invalidasi: cache miss
Evictions: 1
```

Angka milidetik adalah simulasi; yang dinilai adalah status HIT/MISS dan hitungan.

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| `maxSize: 2`, set 3 key | key tertua ter-evict |
| `get` item kedaluwarsa | miss, item dihapus |
| `get` key sama 2× | hits `1` |
| 5 request diizinkan, ke-6 | `429` |
| Setelah 60 detik | diizinkan lagi |
| 10.000 key rate limit | memori dibersihkan, tidak tumbuh terus |
| Update menu | cache invalid, request berikutnya miss |

## Ketentuan

- Jangan memakai `Map` tanpa batas untuk cache/rate limit.
- Jangan memakai `Date.now()` langsung di dalam class; gunakan `clock` yang diinjeksi.
- Jangan menyimpan response body besar tanpa batas ukuran.
- Jangan menambahkan `X-Cache` palsu saat request gagal.
- Jangan memakai `setInterval` global untuk cleanup jika bisa dibersihkan saat akses.
- Rate limit harus per key, bukan global untuk semua pengguna.

## Checklist Sebelum Kumpul

- [ ] LRU benar-benar meng-evict item paling lama.
- [ ] TTL bekerja dan tidak membocorkan item kedaluwarsa.
- [ ] Statistik hits/misses/evictions akurat.
- [ ] Rate limit memakai sliding window.
- [ ] `429` menyertakan `Retry-After`.
- [ ] Cache diinvalidasi saat data berubah.
- [ ] Output sesuai contoh.

## Bonus

1. Tambahkan `stale-while-revalidate`: sajikan data kedaluwarsa sementara refresh di background.
2. Buat token bucket sebagai alternatif sliding window.
3. Rancang strategi cache terdistribusi (Redis) dan jelaskan konsistensinya.
