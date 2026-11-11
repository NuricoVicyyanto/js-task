# Task 09 — Array Dasar: Daftar Menu

> **Level:** Dasar · **Estimasi:** 40 menit · **Topik:** array literal, indeks, `.length`, update elemen, `.join()`

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Membuat array berisi beberapa nilai.
2. Mengakses elemen pertama, terakhir, dan elemen tertentu.
3. Mengubah isi array berdasarkan indeks.

## Studi Kasus

Kopi Senja menyimpan daftar menu di satu tempat agar mudah diubah. Kasir ingin melihat menu pertama, menu terakhir, jumlah menu, dan seluruh daftar menu. Ia juga ingin mengganti nama menu kedua karena ada perubahan nama produk.

## Yang Harus Dibuat

Buat file **`task-09.js`** dengan array awal:

```js
const menu = ["Espresso", "Latte", "Kopi Susu", "Croissant"];
```

Program harus:

1. Mencetak menu pertama.
2. Mencetak menu terakhir menggunakan `.length`.
3. Mencetak jumlah menu.
4. Mencetak menu kedua.
5. Mencetak seluruh menu dipisahkan `, ` menggunakan `.join(", ")`.
6. Mengganti menu kedua menjadi `"Cappuccino"`.
7. Mencetak daftar setelah perubahan.

## Ketentuan

- Gunakan indeks array, bukan menulis ulang nama menu.
- Untuk menu terakhir, gunakan `menu[menu.length - 1]`, bukan angka `3`.
- Gunakan `.join(", ")` untuk menampilkan daftar.
- Jangan mengubah urutan array selain mengganti elemen kedua.

## Ekspektasi Output

Jalankan `node task-09.js`. Output harus **persis** seperti ini:

```text
Menu pertama  : Espresso
Menu terakhir : Croissant
Jumlah menu   : 4
Menu kedua    : Latte
Daftar menu   : Espresso, Latte, Kopi Susu, Croissant
Setelah update: Espresso, Cappuccino, Kopi Susu, Croissant
```

## Contoh Kasus Uji

| Perubahan | Hasil yang diharapkan |
| --- | --- |
| Tambah `"Matcha"` di akhir | Menu terakhir menjadi `Matcha`, jumlah menjadi `5` |
| Hapus `"Latte"` | Menu kedua menjadi `Kopi Susu` |
| Array hanya 1 item | Menu pertama dan terakhir sama |
| Ganti menu terakhir | `.length - 1` tetap menunjuk elemen terakhir yang baru |

## Checklist Sebelum Kumpul

- [ ] Array awal berisi 4 menu sesuai urutan.
- [ ] Menu terakhir diambil dengan `.length - 1`.
- [ ] Jumlah menu memakai `.length`.
- [ ] Menu kedua diganti dengan `"Cappuccino"`.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Cetak menu dalam urutan terbalik tanpa mengubah array asli.
2. Tambahkan menu `"Matcha"` di akhir, lalu cetak jumlah menu yang baru.
3. Jelaskan dalam komentar: mengapa indeks array dimulai dari `0`, bukan `1`?
