# Task 13 — reduce & sort: Laporan Penjualan

> **Level:** Menengah · **Estimasi:** 60 menit · **Topik:** `.reduce()`, `.sort()`, comparator, menyalin array sebelum diurutkan

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menjumlahkan nilai dari array of objects menggunakan `.reduce()`.
2. Mengurutkan array dengan comparator numerik.
3. Menentukan nilai terbesar berdasarkan properti tertentu.
4. Menghindari mutasi array asli saat mengurutkan.

## Studi Kasus

Pemilik Kopi Senja ingin melihat laporan penjualan mingguan: total pendapatan, urutan menu termahal, menu paling banyak terjual, dan rata-rata harga menu. Data mentah sudah tersedia dalam bentuk array of objects.

## Data Awal

```js
const penjualan = [
  { nama: "Espresso", harga: 18000, terjual: 10 },
  { nama: "Latte", harga: 24000, terjual: 7 },
  { nama: "Kopi Susu", harga: 22000, terjual: 8 },
  { nama: "Croissant", harga: 25000, terjual: 5 },
];
```

## Yang Harus Dibuat

Buat file **`task-13.js`** yang menghasilkan:

1. `totalPendapatan` — jumlah dari `harga * terjual` semua menu, memakai `reduce`.
2. `urutTermahal` — array baru yang diurutkan dari harga tertinggi, tanpa mengubah `penjualan`.
3. `menuTerlaris` — objek menu dengan `terjual` paling banyak.
4. `rataRataHarga` — rata-rata `harga`, dibulatkan dengan `Math.round`.

## Ketentuan

- Total pendapatan wajib memakai `.reduce()`.
- Pengurutan wajib memakai comparator `(a, b) => b.harga - a.harga`.
- Sebelum `.sort()`, salin array dengan `.slice()` atau spread agar data asli tetap urut semula.
- Menu terlaris ditentukan dari `terjual`, bukan dari harga.
- Cetak nama menu pada urutan, bukan seluruh objek.

## Ekspektasi Output

```text
Total pendapatan : Rp649000
Urutan termahal  : Croissant, Latte, Kopi Susu, Espresso
Menu terlaris    : Espresso (10 porsi)
Rata-rata harga  : Rp22250
```

## Contoh Kasus Uji

| Perubahan data | Hasil yang diharapkan |
| --- | --- |
| `Espresso.terjual = 1` | Menu terlaris menjadi `Kopi Susu` |
| Tambah menu Rp30.000 | Menu tersebut muncul paling depan pada urutan termahal |
| Semua `terjual = 0` | Total pendapatan `Rp0` |
| Array kosong | Tangani agar tidak error; tampilkan `Rp0` |

## Checklist Sebelum Kumpul

- [ ] Total dihitung dengan `reduce`, bukan loop manual.
- [ ] Comparator mengembalikan angka, bukan boolean.
- [ ] Array `penjualan` tetap dalam urutan awal setelah laporan dibuat.
- [ ] Menu terlaris diambil dari properti `terjual`.
- [ ] Rata-rata dibulatkan dengan `Math.round`.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Urutkan menu berdasarkan jumlah terjual dari yang paling banyak.
2. Hitung total porsi terjual menggunakan `reduce`.
3. Jelaskan dalam komentar: mengapa `.sort()` tanpa salinan bisa mengubah data asli?
