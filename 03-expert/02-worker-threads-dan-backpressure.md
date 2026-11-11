# Task E02 — Worker Threads & Backpressure

> **Level:** Expert · **Estimasi:** 3–4 jam · **Topik:** `node:worker_threads`, event loop, bounded queue, backpressure, error propagation

## Tujuan

Memindahkan pekerjaan CPU-bound dari main thread ke worker, dengan antrean terbatas agar memori tidak meledak. Membuktikan bahwa event loop tetap responsif selama pemrosesan.

## Studi Kasus

Kopi Senja mengimpor 100.000 baris penjualan setiap malam. Perhitungan total dan rekap kategori memblokir server selama beberapa detik. Tim meminta pemrosesan dilakukan di worker thread dengan **backpressure**: produsen berhenti mengirim data ketika antrean penuh.

## File yang Dibuat

```text
e02-worker/
├── main.js
├── worker.js
└── data.js
```

## Data

`data.js` menghasilkan 100.000 baris deterministik:

```js
export function buatData(jumlah = 100000) {
  return Array.from({ length: jumlah }, (_, i) => ({
    id: i + 1,
    qty: 1,
    harga: 1000,
  }));
}
```

Total yang benar: `100000000`.

## Arsitektur

- `main.js` membuat worker dan membagi data menjadi **chunk** berisi 1.000 baris (total 100 chunk).
- Antrean maksimal **4 chunk**.
- Jika antrean penuh, produsen menunggu (`await`) sampai worker selesai memproses satu chunk.
- Worker mengirim pesan `{ type: "selesai", total }` atau `{ type: "error", message }`.
- Main thread menghitung total pembanding secara sinkron setelah worker selesai.
- Main thread menjalankan heartbeat `setInterval` 10 ms; jumlah tick dicatat.

## Yang Harus Dibuat

### `worker.js`

- Menerima pesan `{ type: "chunk", data }`.
- Menjumlahkan `qty * harga`.
- Mengirim hasil parsial.
- Menangani error dan mengirim pesan error, bukan crash diam-diam.

### `main.js`

- Fungsi `prosesDenganWorker(data)`.
- Fungsi `prosesDiMain(data)` sebagai pembanding.
- Pengukuran waktu dengan `performance.now()`.
- Pencatatan `antreanMaks`.
- `worker.terminate()` dipanggil di `finally`.

## Ekspektasi Output

```text
Data: 100000 baris
Total worker: 100000000
Total main: 100000000
Antrean maksimum: 4
Heartbeat aktif: true
Worker selesai: < 2000 ms
```

`< 2000 ms` adalah target; angka aktual boleh berbeda tergantung mesin. Yang dinilai adalah **target tercapai** dan kebenaran total.

## Kriteria Backpressure

| Kriteria | Target |
| --- | --- |
| Antrean maksimum | tidak lebih dari `4` |
| Data dikirim | semua 100 chunk |
| Total | sama dengan pembanding |
| Event loop | heartbeat tetap berjalan saat worker aktif |
| Worker | selalu dihentikan, termasuk saat error |
| Memori | tidak menyimpan semua chunk sekaligus di antrean |

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| 1.000 baris | total `1.000.000` |
| 100.000 baris | total `100.000.000` |
| Worker melempar error | error diteruskan ke main, program tidak menggantung |
| Antrean penuh | produsen menunggu, bukan menambah antrean |
| Worker dihentikan di tengah | proses selesai dengan error yang jelas |

## Ketentuan

- Wajib memakai `node:worker_threads`.
- Jangan memakai library worker pool eksternal.
- Jangan mengirim seluruh 100.000 baris dalam satu pesan.
- Jangan memakai `while` sibuk untuk menunggu; gunakan Promise/event.
- Jangan menelan error worker.
- Main thread tidak boleh memblokir event loop lebih dari beberapa milidetik.

## Checklist Sebelum Kumpul

- [ ] Worker menerima chunk, bukan seluruh data.
- [ ] Antrean maksimal 4.
- [ ] Total worker = total main.
- [ ] Heartbeat berjalan selama pemrosesan.
- [ ] `terminate()` dipanggil di semua jalur.
- [ ] Error worker terlihat di main.
- [ ] Output sesuai format dan target waktu tercapai.

## Bonus

1. Buat worker pool berisi 4 worker.
2. Gunakan `Transferable`/`SharedArrayBuffer` untuk data numerik besar.
3. Tambahkan pembatalan (`AbortSignal`) dan pengukuran memori per chunk.
