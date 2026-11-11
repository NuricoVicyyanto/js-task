# Task 02 — Operator & Template Literal: Struk Manual

> **Level:** Dasar · **Estimasi:** 40 menit · **Topik:** operator aritmatika, urutan operasi, template literal

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menghitung subtotal, pajak, dan total menggunakan operator aritmatika.
2. Menggunakan tanda kurung untuk mengatur urutan perhitungan.
3. Menampilkan hasil perhitungan ke dalam teks dengan template literal.

## Studi Kasus

Seorang pelanggan memesan tiga jenis menu di Kopi Senja. Kasir masih mencatat pesanan secara manual dan sering salah menghitung pajak. Kamu diminta membuat program sederhana yang menghitung struk pelanggan tersebut.

Pesanan pelanggan:

| Menu | Harga | Jumlah |
| --- | --- | --- |
| Espresso | Rp18.000 | 2 |
| Latte | Rp24.000 | 1 |
| Croissant | Rp30.000 | 2 |

Pajak yang dikenakan adalah **10% dari subtotal**.

## Yang Harus Dibuat

Buat file **`task-02.js`** yang:

1. Menyimpan harga dan jumlah setiap menu ke variabel.
2. Menghitung total per menu (`harga * jumlah`).
3. Menghitung `subtotal` dari ketiga total menu.
4. Menghitung `pajak` sebesar 10% dari subtotal.
5. Menghitung `total = subtotal + pajak`.
6. Mencetak struk sesuai format di bawah.

## Ketentuan

- Gunakan operator `*`, `+`, `/`, dan `%` jika diperlukan.
- Hitung pajak dari **subtotal**, bukan dari masing-masing item.
- Jangan menulis hasil akhir secara manual; semua angka harus berasal dari perhitungan.
- Gunakan template literal untuk setiap baris output.

## Ekspektasi Output

Jalankan `node task-02.js`. Output harus **persis** seperti ini:

```text
=== STRUK KOPI SENJA ===
Espresso x2 = Rp36000
Latte x1 = Rp24000
Croissant x2 = Rp30000
----------------------
Subtotal = Rp90000
Pajak 10% = Rp9000
Total = Rp99000
```

## Contoh Kasus Uji

| Perubahan data | Subtotal | Pajak 10% | Total |
| --- | --- | --- | --- |
| Espresso x1, Latte x1, Croissant x1 | Rp72000 | Rp7200 | Rp79200 |
| Espresso x3, Latte x2, Croissant x0 | Rp102000 | Rp10200 | Rp112200 |
| Semua jumlah `0` | Rp0 | Rp0 | Rp0 |

## Checklist Sebelum Kumpul

- [ ] Total setiap menu dihitung dengan `harga * jumlah`.
- [ ] Subtotal adalah penjumlahan ketiga total menu.
- [ ] Pajak dihitung dari subtotal, bukan dari total akhir.
- [ ] Output memiliki garis pemisah sebanyak 22 karakter `-`.
- [ ] Tidak ada angka hasil yang ditulis manual di dalam teks.

## Bonus

1. Tambahkan biaya layanan **5% dari subtotal** dan tampilkan sebagai baris `Biaya layanan`.
2. Bulatkan total ke bawah menggunakan `Math.floor` jika hasilnya mengandung desimal.
3. Jelaskan dalam komentar: apa perbedaan `subtotal * 10 / 100` dengan `subtotal * (10 / 100)`?
