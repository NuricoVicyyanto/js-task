# Task 10 — Method Array: Antrean Pesanan

> **Level:** Dasar · **Estimasi:** 50 menit · **Topik:** `push`, `unshift`, `shift`, `pop`, `includes`, `indexOf`, `.join()`

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menambah item di akhir dan di awal array.
2. Menghapus item dari awal dan akhir array.
3. Memeriksa keberadaan dan posisi item di dalam array.

## Studi Kasus

Kopi Senja memakai antrean pesanan sederhana. Pesanan baru biasanya masuk dari belakang, tetapi pesanan prioritas bisa dimasukkan ke depan. Setelah pesanan selesai dibuat, pesanan paling depan dihapus dari antrean.

Simulasikan alur berikut:

1. Antrean awal: `Espresso`, `Latte`.
2. Tambah `Croissant` di belakang.
3. Tambah `Kopi Susu` di depan (pesanan prioritas).
4. Layani pesanan paling depan.
5. Periksa apakah `Latte` masih ada.
6. Cari posisi `Latte`.

## Yang Harus Dibuat

Buat file **`task-10.js`** yang melakukan langkah-langkah di atas menggunakan method array, lalu mencetak hasil setiap tahap.

## Ketentuan

- Gunakan `push` untuk menambah di belakang.
- Gunakan `unshift` untuk menambah di depan.
- Gunakan `shift` untuk mengambil pesanan paling depan.
- Gunakan `includes` untuk memeriksa keberadaan.
- Gunakan `indexOf` untuk mencari posisi.
- Simpan hasil `shift` ke variabel `pesananDilayani`, lalu cetak.
- Tampilkan isi array dengan `.join(", ")`.

## Ekspektasi Output

Jalankan `node task-10.js`. Output harus **persis** seperti ini:

```text
Antrean awal     : Espresso, Latte
Setelah push     : Espresso, Latte, Croissant
Setelah unshift  : Kopi Susu, Espresso, Latte, Croissant
Pesanan dilayani : Kopi Susu
Antrean sekarang : Espresso, Latte, Croissant
Latte ada?       : true
Posisi Latte     : 1
```

## Contoh Kasus Uji

| Operasi | Hasil |
| --- | --- |
| `["A", "B"].push("C")` | `["A", "B", "C"]` |
| `["A", "B"].unshift("C")` | `["C", "A", "B"]` |
| `["A", "B"].shift()` | mengembalikan `"A"`, array menjadi `["B"]` |
| `["A", "B"].pop()` | mengembalikan `"B"`, array menjadi `["A"]` |
| `["A", "B"].includes("B")` | `true` |
| `["A", "B"].indexOf("C")` | `-1` |

## Checklist Sebelum Kumpul

- [ ] `push` dan `unshift` digunakan pada posisi yang benar.
- [ ] `shift` menyimpan nilai yang dihapus, bukan hanya memanggilnya.
- [ ] Posisi `Latte` adalah `1`, bukan `2`.
- [ ] Item yang tidak ada menghasilkan `-1` pada `indexOf`.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Tambahkan simulasi pembatalan pesanan terakhir menggunakan `pop`, lalu cetak antrean.
2. Buat salinan antrean dengan `slice()` sebelum mengubahnya, agar antrean asli tetap aman.
3. Jelaskan dalam komentar: apa perbedaan `shift()` dan `pop()`?
