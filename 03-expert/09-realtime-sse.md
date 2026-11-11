# Task E09 — Realtime: Server-Sent Events (SSE)

> **Level:** Expert · **Estimasi:** 4 jam · **Topik:** `text/event-stream`, broadcast, heartbeat, cleanup, `EventSource`

## Tujuan

Membangun kanal realtime satu arah dari server ke browser tanpa library, dengan koneksi yang dibersihkan saat client putus.

## Studi Kasus

Layar dapur Kopi Senja harus menampilkan pesanan baru secara langsung tanpa refresh. Frontend memakai `EventSource`; backend mengirim event saat pesanan dibuat. Koneksi harus tetap hidup, tetapi tidak boleh bocor memori ketika banyak client membuka dan menutup tab.

## Yang Harus Dibuat (File)

```text
e09-sse/
├── server.js
└── public/
    ├── index.html
    └── app.js
```

## Endpoint

| Method | Path | Tugas |
| --- | --- | --- |
| GET | `/events` | membuka koneksi SSE |
| POST | `/api/orders` | membuat pesanan dan broadcast |
| GET | `/` | halaman layar dapur |

## Format SSE

Saat client terhubung:

```text
event: connected
data: {"clientId":"c-1","jumlahClient":1}

```

Saat pesanan dibuat:

```text
event: order.created
data: {"id":"KS-001","total":60000,"pelanggan":"Nadia"}

```

Heartbeat setiap 15 detik:

```text
: heartbeat

```

## Perilaku Wajib

### Server

- Response header:
  - `Content-Type: text/event-stream`
  - `Cache-Control: no-cache, no-transform`
  - `Connection: keep-alive`
  - `X-Accel-Buffering: no`
- Kirim event `connected` segera setelah koneksi dibuat.
- Simpan daftar client di `Set`.
- Saat `req` ditutup, hapus client dari `Set` dan `clearInterval` heartbeat.
- `POST /api/orders` memvalidasi body, membuat order, lalu broadcast ke semua client.
- Jika client lambat (`res.write` mengembalikan `false`), jangan menumpuk data tanpa batas; putuskan koneksi atau lewati event dengan log.
- Maksimal 100 client; lebih dari itu balas `503`.

### Client

- Gunakan `new EventSource("/events")`.
- Tampilkan status `terhubung` / `terputus`.
- Tambahkan pesanan ke daftar saat `order.created` diterima.
- EventSource harus reconnect otomatis; tampilkan percobaan koneksi ulang.

## Ekspektasi Output

Server:

```text
[SSE] client connected: 1
[SSE] order.created -> 1 client
[SSE] client disconnected: 0
```

Browser:

```text
Status: terhubung
Pesanan baru: KS-001 — Rp60000
Pesanan baru: KS-002 — Rp24000
```

Uji dengan `curl -N http://localhost:3000/events`:

```text
event: connected
data: {"clientId":"c-1","jumlahClient":1}

: heartbeat
```

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| Client terhubung | event `connected` diterima |
| Dua client terhubung | keduanya menerima order baru |
| Client menutup tab | dihapus dari `Set`, heartbeat berhenti |
| 101 client | client ke-101 mendapat `503` |
| Server mengirim 100 event | tidak ada `MaxListenersExceededWarning` |
| Client lambat | server tidak kehabisan memori |

## Ketentuan

- Jangan memakai library WebSocket/SSE.
- Jangan mengirim event sebelum header di-flush.
- Jangan membiarkan interval heartbeat berjalan setelah client putus.
- Jangan menyimpan client di array tanpa kemampuan hapus efisien.
- Jangan menaruh data sensitif di payload SSE.
- Gunakan `res.write()` dengan format SSE yang benar, termasuk baris kosong di akhir event.

## Checklist Sebelum Kumpul

- [ ] Header SSE lengkap.
- [ ] Event `connected` terkirim.
- [ ] Broadcast ke semua client.
- [ ] Cleanup saat disconnect.
- [ ] Heartbeat berjalan dan berhenti.
- [ ] Batas client diterapkan.
- [ ] Output server dan browser sesuai contoh.

## Bonus

1. Tambahkan dukungan `Last-Event-ID` untuk mengirim event yang terlewat.
2. Buat room per outlet (contoh `/events?outlet=bandung`).
3. Tambahkan autentikasi token pada koneksi SSE dan uji token kedaluwarsa.
