# Task 28 — Callback & Promise: Simulasi Dapur

> **Level:** Lanjutan · **Estimasi:** 75 menit · **Topik:** callback, `setTimeout`, Promise, `.then()`, `Promise.all()`

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menjalankan kode setelah proses selesai menggunakan callback.
2. Membuat dan menggunakan Promise.
3. Menunggu beberapa proses sekaligus dengan `Promise.all()`.

## Studi Kasus

Dapur Kopi Senja membutuhkan waktu untuk membuat pesanan. Kasir tidak boleh menunggu secara blocking; ia harus bisa menerima pesanan lain sementara pesanan sebelumnya diproses. Simulasikan proses ini menggunakan `setTimeout`, callback, dan Promise.

## Yang Harus Dibuat

Buat file **`task-28.js`** yang menjalankan tiga bagian secara berurutan: callback, Promise, lalu `Promise.all`. Setiap bagian dijelaskan di bawah.

## Bagian A — Callback

Buat fungsi:

```js
function ambilPesanan(nama, callback) {
  console.log("Menerima pesanan...");
  setTimeout(() => {
    callback(`Pesanan siap: ${nama}`);
  }, 1000);
}
```

Panggil dengan `"Espresso"`, lalu cetak hasil dari callback menggunakan `console.log`.

## Bagian B — Promise

Buat fungsi:

```js
function ambilPesananPromise(nama) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(nama);
    }, 1000);
  });
}
```

Cetak `Memproses pesanan Latte...`, panggil fungsi untuk `"Latte"` menggunakan `.then()`, lalu cetak `Pesanan siap: <nama>`.

## Bagian C — Promise.all

Cetak `Memproses 2 pesanan sekaligus...`, panggil `ambilPesananPromise` untuk `"Croissant"` dan `"Matcha"` secara bersamaan, lalu tunggu keduanya selesai dengan `Promise.all()`. Cetak hasilnya dalam satu baris dipisahkan `, `.

## Ketentuan

- Gunakan `setTimeout` dengan delay **1000 ms**.
- Bagian A wajib memakai callback.
- Bagian B wajib memakai `.then()`, bukan `await` (async/await ada di Task 29).
- Bagian C wajib memakai `Promise.all()`.
- Urutan proses harus berantai: mulai Bagian B **di dalam callback Bagian A**, dan mulai Bagian C **di dalam `.then()` Bagian B**. Jangan memanggil ketiganya sekaligus.
- Jangan mengubah delay agar urutan output mudah diamati.
- Semua output harus muncul dalam urutan yang ditentukan.

## Ekspektasi Output

```text
Menerima pesanan...
Pesanan siap: Espresso
Memproses pesanan Latte...
Pesanan siap: Latte
Memproses 2 pesanan sekaligus...
Semua pesanan siap: Croissant, Matcha
```

> Perhatikan: output muncul bertahap, bukan sekaligus. `Pesanan siap: Espresso` baru muncul setelah ±1 detik.

## Contoh Kasus Uji

| Skenario | Hasil |
| --- | --- |
| `ambilPesanan("Espresso", cb)` | `Pesanan siap: Espresso` setelah 1 detik |
| `ambilPesananPromise("Latte")` | Promise resolve dengan nama pesanan |
| `Promise.all` dua pesanan | Array dua string, urutan sesuai input |
| Nama kosong | Boleh tetap diproses; validasi belum diwajibkan |

## Checklist Sebelum Kumpul

- [ ] Callback dipanggil di dalam `setTimeout`.
- [ ] Promise memakai `resolve`.
- [ ] Bagian B memakai `.then()`.
- [ ] Bagian C memakai `Promise.all()`.
- [ ] Output muncul bertahap, bukan langsung semua.
- [ ] Urutan output sama dengan contoh.

## Bonus

1. Tambahkan `reject` jika nama pesanan kosong, lalu tangani dengan `.catch()`.
2. Buat `Promise.race()` untuk melihat pesanan mana yang selesai lebih dulu dengan delay berbeda.
3. Ubah Bagian C agar setiap pesanan memiliki delay berbeda, tetapi hasil tetap menunggu semua selesai.
