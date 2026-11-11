# Task 11 — Objek Dasar: Detail Menu

> **Level:** Dasar · **Estimasi:** 45 menit · **Topik:** object literal, properti, dot notation, bracket notation, update properti

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Membuat objek dengan beberapa properti.
2. Mengakses properti dengan dot notation dan bracket notation.
3. Mengubah dan menambah properti objek.

## Studi Kasus

Setiap menu di Kopi Senja memiliki beberapa informasi yang saling berkaitan: nama, kategori, harga, dan status ketersediaan. Jika disimpan sebagai variabel terpisah, data mudah tercampur. Objek memungkinkan semua informasi satu menu disimpan dalam satu wadah.

Kali ini kamu mengelola satu menu saja, yaitu **Latte**.

## Yang Harus Dibuat

Buat file **`task-11.js`** dengan objek awal:

```js
const menu = {
  nama: "Latte",
  kategori: "Minuman",
  harga: 24000,
  tersedia: true,
};
```

Program harus:

1. Mencetak nama dengan dot notation.
2. Mencetak kategori dengan bracket notation `menu["kategori"]`.
3. Mencetak harga awal.
4. Mencetak status ketersediaan.
5. Mengubah harga menjadi `26000`.
6. Menambahkan properti `stok` berisi `20`.
7. Mencetak harga baru, stok, dan jumlah properti (`Object.keys(menu).length`).

## Ketentuan

- Gunakan object literal `{ ... }`, bukan `new Object()`.
- Minimal satu akses wajib memakai bracket notation.
- Perubahan harga harus mengubah objek, bukan membuat objek baru.
- Jangan menghapus properti apa pun.

## Ekspektasi Output

Jalankan `node task-11.js`. Output harus **persis** seperti ini:

```text
Nama             : Latte
Kategori         : Minuman
Harga awal       : Rp24000
Tersedia         : true
Harga baru       : Rp26000
Stok             : 20
Jumlah properti  : 5
```

## Contoh Kasus Uji

| Perubahan | Hasil yang diharapkan |
| --- | --- |
| `menu.harga = 30000` | Harga baru `Rp30000` |
| `menu.stok = 0` | Stok `0`, jumlah properti tetap `5` |
| `menu["nama"]` | `"Latte"` |
| Properti yang tidak ada | `undefined` |

## Checklist Sebelum Kumpul

- [ ] Objek memiliki 4 properti awal.
- [ ] Dot notation dan bracket notation sama-sama dipakai.
- [ ] Harga berubah menjadi `26000` sebelum dicetak.
- [ ] Properti `stok` ditambahkan setelah objek dibuat.
- [ ] Jumlah properti menjadi `5`.

## Bonus

1. Tambahkan properti `varian` berisi array `["panas", "dingin"]`, lalu cetak `Varian: panas, dingin`.
2. Hapus properti `tersedia` dengan `delete`, lalu cetak `Object.keys(menu)`.
3. Jelaskan dalam komentar: kapan sebaiknya memakai bracket notation?
