# Task 21 — Date & Waktu: Jam Operasional

> **Level:** Menengah · **Estimasi:** 60 menit · **Topik:** `new Date()`, `getDay()`, `getDate()`, `getMonth()`, `getHours()`, `padStart()`

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Membuat objek tanggal dan mengambil komponennya.
2. Mengubah angka hari/bulan menjadi nama yang mudah dibaca.
3. Menentukan status buka/tutup berdasarkan hari dan jam.

## Studi Kasus

Kopi Senja buka setiap hari **kecuali Minggu**, pukul **08.00–21.00**. Kasir ingin program yang menampilkan hari, tanggal, jam, status buka/tutup, dan sisa jam buka pada waktu tertentu.

Gunakan tanggal tetap berikut agar hasilnya dapat diprediksi:

```js
const sekarang = new Date("2026-11-11T14:30:00");
```

Tanggal tersebut adalah **Rabu, 11 November 2026, pukul 14.30**.

## Yang Harus Dibuat

Buat file **`task-21.js`** yang:

1. Menampilkan nama hari dalam bahasa Indonesia.
2. Menampilkan tanggal dalam format `11 November 2026`.
3. Menampilkan jam dalam format `14:30` (dua digit).
4. Menampilkan jam buka `08:00` dan jam tutup `21:00`.
5. Menentukan status: `Buka` jika bukan Minggu dan jam 08.00–20.59; selain itu `Tutup`.
6. Menghitung sisa jam buka (`21 - jam sekarang`) jika sedang buka; jika tutup, tampilkan `0 jam`.

## Ketentuan

- Gunakan method `getDay()`, `getDate()`, `getMonth()`, `getFullYear()`, `getHours()`, dan `getMinutes()`.
- Gunakan array nama hari dan nama bulan; jangan menulis nama hari/bulan langsung di output.
- Gunakan `padStart(2, "0")` untuk menit dan jam.
- Jangan memakai `toLocaleDateString()` agar hasilnya sama di semua environment.
- Hari Minggu adalah indeks `0`.

## Ekspektasi Output

```text
Hari         : Rabu
Tanggal      : 11 November 2026
Jam          : 14:30
Jam buka     : 08:00
Jam tutup    : 21:00
Status       : Buka
Sisa jam buka: 7 jam
```

## Contoh Kasus Uji

| Tanggal | Status | Sisa jam buka |
| --- | --- | --- |
| `2026-11-11T14:30:00` (Rabu) | Buka | 7 jam |
| `2026-11-11T07:00:00` (Rabu) | Tutup | 0 jam |
| `2026-11-11T21:00:00` (Rabu) | Tutup | 0 jam |
| `2026-11-15T12:00:00` (Minggu) | Tutup | 0 jam |
| `2026-11-09T08:00:00` (Senin) | Buka | 13 jam |

## Checklist Sebelum Kumpul

- [ ] Nama hari dan bulan berasal dari array.
- [ ] Tanggal memakai format `11 November 2026`.
- [ ] Jam memakai dua digit (`08:00`, bukan `8:0`).
- [ ] Hari Minggu selalu tutup.
- [ ] Jam 21.00 sudah dianggap tutup.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Tampilkan pesan `Buka dalam 2 jam` jika sekarang sebelum jam buka.
2. Hitung sisa waktu dalam format `7 jam 30 menit`.
3. Buat fungsi `statusOperasional(tanggal)` agar tanggal lain bisa diuji dengan mudah.
