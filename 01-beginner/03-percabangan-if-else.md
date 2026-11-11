# Task 03 — Percabangan if/else: Diskon & Ongkir

> **Level:** Dasar · **Estimasi:** 45 menit · **Topik:** `if`, `else if`, `else`, operator perbandingan, operator logika

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menulis percabangan bertingkat dengan `if / else if / else`.
2. Menggunakan operator perbandingan `>=`, `<`, dan `<=`.
3. Menentukan nilai variabel berdasarkan kondisi yang berbeda.

## Studi Kasus

Kopi Senja sedang mengadakan promo. Besaran diskon bergantung pada subtotal belanja, sedangkan ongkir bergantung pada subtotal dan jarak pengiriman. Kasir perlu program yang otomatis menentukan diskon, ongkir, dan total akhir agar tidak salah hitung.

## Aturan Bisnis

### Diskon

| Subtotal | Diskon |
| --- | --- |
| Kurang dari Rp50.000 | 0% |
| Rp50.000 – Rp99.999 | 10% |
| Rp100.000 atau lebih | 20% |

### Ongkir

| Kondisi | Ongkir |
| --- | --- |
| Subtotal Rp75.000 atau lebih | Gratis (Rp0) |
| Subtotal di bawah Rp75.000 dan jarak ≤ 3 km | Rp10.000 |
| Subtotal di bawah Rp75.000 dan jarak > 3 km | Rp15.000 |

**Rumus:** `total = subtotal - diskon + ongkir`

## Yang Harus Dibuat

Buat file **`task-03.js`** dengan data awal:

```js
const subtotal = 60000;
const jarakKm = 5;
```

Program harus:

1. Menentukan `diskon` memakai `if / else if / else`.
2. Menentukan `ongkir` memakai `if / else`.
3. Menghitung `total`.
4. Mencetak hasil sesuai format.

## Ketentuan

- Diskon berupa **nominal rupiah**, bukan persen. Contoh: 10% dari 60.000 = 6.000.
- Periksa syarat **gratis ongkir terlebih dahulu** sebelum memeriksa jarak.
- Gunakan `let` untuk `diskon`, `ongkir`, dan `total` karena nilainya ditentukan kemudian.
- Jangan menggunakan `switch` pada task ini.

## Ekspektasi Output

Jalankan `node task-03.js`. Output harus **persis** seperti ini:

```text
Subtotal : Rp60000
Diskon   : Rp6000
Ongkir   : Rp15000
Total    : Rp69000
```

## Contoh Kasus Uji

| Subtotal | Jarak | Diskon | Ongkir | Total |
| --- | --- | --- | --- | --- |
| 120000 | 2 km | Rp24000 | Rp0 | Rp96000 |
| 50000 | 3 km | Rp5000 | Rp10000 | Rp55000 |
| 30000 | 5 km | Rp0 | Rp15000 | Rp45000 |
| 75000 | 10 km | Rp7500 | Rp0 | Rp67500 |
| 49999 | 1 km | Rp0 | Rp10000 | Rp59999 |

## Checklist Sebelum Kumpul

- [ ] Batas diskon 50.000 dan 100.000 diuji dengan benar.
- [ ] Diskon 20% hanya berlaku mulai Rp100.000.
- [ ] Gratis ongkir berlaku mulai Rp75.000, berapa pun jaraknya.
- [ ] Total dihitung setelah diskon dan ongkir.
- [ ] Output menggunakan label dan spasi yang sama dengan contoh.

## Bonus

1. Tampilkan juga persentase diskon, misalnya `Diskon   : Rp6000 (10%)`.
2. Tambahkan aturan: jika jarak lebih dari 10 km, tampilkan `Ongkir   : Tidak tersedia` dan total tidak dihitung.
3. Refaktor perhitungan diskon menjadi fungsi `hitungDiskon(subtotal)` (boleh menunggu sampai Task 07).
