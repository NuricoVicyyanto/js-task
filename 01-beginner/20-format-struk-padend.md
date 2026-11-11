# Task 20 — Format Struk: `padEnd` & `padStart`

> **Level:** Menengah · **Estimasi:** 60 menit · **Topik:** `padEnd()`, `padStart()`, perataan teks, lebar kolom

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menentukan lebar kolom teks menggunakan `padEnd()` dan `padStart()`.
2. Membuat struk dengan harga rata kanan.
3. Menyusun output yang rapi tanpa menambah spasi manual per baris.

## Studi Kasus

Struk Kopi Senja saat ini berantakan karena harga tidak sejajar. Kasir ingin struk dengan lebar **30 karakter**: nama item rata kiri, harga rata kanan. Panjang nama item maksimal 20 karakter agar tidak mendorong harga keluar baris.

## Data Awal

```js
const items = [
  { nama: "Espresso", jumlah: 2, harga: 18000 },
  { nama: "Latte", jumlah: 1, harga: 24000 },
];

const total = 60000;
```

## Yang Harus Dibuat

Buat file **`task-20.js`** yang mencetak struk persis seperti format di bawah.

Aturan teknis:

1. Garis atas dan bawah memakai `"="` sebanyak 30 karakter.
2. Judul `STRUK KOPI SENJA` memiliki 7 spasi di depan.
3. Setiap baris item: label `${nama} x${jumlah}` di-`padEnd(22)`, lalu harga `Rp${harga * jumlah}` di-`padStart(8)`.
4. Garis pemisah memakai `"-"` sebanyak 30 karakter.
5. Baris `TOTAL` memakai aturan kolom yang sama dengan item.
6. Total ditulis sebagai `Rp60000` (tanpa titik).

## Ketentuan

- Wajib memakai `padEnd()` dan `padStart()`.
- Jangan menulis spasi manual untuk meratakan kolom.
- Jangan menggunakan `.repeat()`; buat garis dengan perulangan atau string literal.
- Lebar total setiap baris item adalah 30 karakter.

## Ekspektasi Output

```text
==============================
       STRUK KOPI SENJA
==============================
Espresso x2            Rp36000
Latte x1               Rp24000
------------------------------
TOTAL                  Rp60000
==============================
```

## Contoh Kasus Uji

| Item | Baris yang diharapkan |
| --- | --- |
| Espresso x2 | `Espresso x2            Rp36000` |
| Latte x1 | `Latte x1               Rp24000` |
| Croissant x1, 25000 | `Croissant x1           Rp25000` |
| Total 100000 | `TOTAL                  Rp100000` |

## Checklist Sebelum Kumpul

- [ ] Garis atas dan bawah tepat 30 karakter.
- [ ] Judul memiliki 7 spasi di depan.
- [ ] Label item memakai `padEnd(22)`.
- [ ] Harga memakai `padStart(8)`.
- [ ] Harga setiap item dihitung dari `harga * jumlah`.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Tambahkan baris `Tanggal` dan `Kasir` di bawah judul dengan perataan yang sama.
2. Buat lebar struk menjadi variabel `const lebar = 30`, lalu gunakan variabel itu untuk semua perhitungan.
3. Tangani nama item yang lebih dari 20 karakter dengan memotongnya memakai `slice()`.
