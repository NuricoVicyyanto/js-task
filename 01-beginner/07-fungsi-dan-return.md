# Task 07 — Fungsi & Return: Kalkulator Harga

> **Level:** Dasar · **Estimasi:** 50 menit · **Topik:** deklarasi fungsi, parameter, `return`, pemanggilan fungsi

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Membuat fungsi dengan parameter.
2. Mengembalikan nilai menggunakan `return`.
3. Memanggil fungsi dari fungsi lain.

## Studi Kasus

Kasir Kopi Senja masih menghitung total belanja secara manual. Agar perhitungan konsisten, kamu diminta membuat tiga fungsi kecil yang bisa dipakai berulang kali:

- menghitung subtotal,
- menghitung pajak,
- menghitung total akhir.

Pajak restoran di kota ini adalah **11% dari subtotal**.

## Yang Harus Dibuat

Buat file **`task-07.js`** dengan tiga fungsi:

| Fungsi | Parameter | Tugas |
| --- | --- | --- |
| `hitungSubtotal(harga, jumlah)` | harga satuan, jumlah beli | mengembalikan `harga * jumlah` |
| `hitungPajak(subtotal)` | subtotal | mengembalikan 11% dari subtotal |
| `hitungTotal(harga, jumlah)` | harga satuan, jumlah beli | memanggil dua fungsi di atas dan mengembalikan total |

Lalu panggil `hitungTotal(25000, 3)` dan cetak hasilnya.

## Ketentuan

- Ketiga fungsi wajib mengembalikan nilai dengan `return`.
- `hitungTotal` **wajib memanggil** `hitungSubtotal` dan `hitungPajak`; jangan menghitung ulang dari nol.
- Fungsi bantu tidak boleh mencetak apa pun. Hanya kode utama yang boleh `console.log`.
- Rumus pajak: `subtotal * 11 / 100`.
- Jangan membulatkan hasil kecuali diminta.

## Ekspektasi Output

Jalankan `node task-07.js`. Output harus **persis** seperti ini:

```text
Subtotal: Rp75000
Pajak 11%: Rp8250
Total: Rp83250
```

## Contoh Kasus Uji

| Pemanggilan | Subtotal | Pajak | Total |
| --- | --- | --- | --- |
| `hitungTotal(18000, 2)` | 36000 | 3960 | 39960 |
| `hitungTotal(24000, 1)` | 24000 | 2640 | 26640 |
| `hitungTotal(15000, 0)` | 0 | 0 | 0 |
| `hitungTotal(0, 5)` | 0 | 0 | 0 |

## Checklist Sebelum Kumpul

- [ ] Tiga fungsi ada dan namanya sesuai.
- [ ] Setiap fungsi memakai `return`, bukan hanya `console.log`.
- [ ] `hitungTotal` memanggil dua fungsi bantu.
- [ ] Output sama persis dengan contoh.
- [ ] Mengubah harga atau jumlah otomatis mengubah output.

## Bonus

1. Tambahkan fungsi `hitungKembalian(total, uangDibayar)` yang mengembalikan uang kembalian.
2. Tambahkan validasi: jika `jumlah` negatif, fungsi mengembalikan `0`.
3. Jelaskan dalam komentar: apa perbedaan `return` dengan `console.log` di dalam fungsi?
