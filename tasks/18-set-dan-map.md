# Task 18 — Set & Map: Kategori Unik dan Rekap Pendapatan

> **Level:** Menengah · **Estimasi:** 60 menit · **Topik:** `Set`, `Map`, iterasi `for...of`, data unik, rekap key-value

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Mengambil nilai unik menggunakan `Set`.
2. Menyimpan pasangan key-value menggunakan `Map`.
3. Mengakumulasi nilai per kategori dari array of objects.

## Studi Kasus

Manajer Kopi Senja ingin tahu kategori menu apa saja yang dimiliki, lalu melihat total pendapatan per kategori. Kategori tidak boleh duplikat, dan rekap harus dihitung otomatis dari data penjualan.

## Data Awal

```js
const menu = [
  { nama: "Espresso", kategori: "Minuman", harga: 18000, terjual: 10 },
  { nama: "Latte", kategori: "Minuman", harga: 24000, terjual: 7 },
  { nama: "Kopi Susu", kategori: "Minuman", harga: 22000, terjual: 8 },
  { nama: "Croissant", kategori: "Makanan", harga: 25000, terjual: 5 },
];
```

## Yang Harus Dibuat

Buat file **`task-18.js`** yang:

1. Mengambil semua kategori unik dengan `Set`.
2. Mengubah `Set` menjadi array agar bisa dicetak dengan `.join(", ")`.
3. Membuat `Map` bernama `rekapPendapatan`.
4. Menghitung pendapatan setiap menu (`harga * terjual`) dan menambahkannya ke kategori yang sesuai.
5. Mencetak kategori unik dan isi `Map`.
6. Mencetak jumlah kategori.

## Ketentuan

- Gunakan `new Set(menu.map(...))` untuk kategori unik.
- Gunakan `new Map()` untuk rekap.
- Saat kategori belum ada di `Map`, inisialisasi dengan `0` terlebih dahulu.
- Gunakan `rekap.get(kategori)` dan `rekap.set(kategori, nilaiBaru)`.
- Cetak isi `Map` menggunakan `for...of`, bukan mengakses key satu per satu secara manual.

## Ekspektasi Output

```text
Kategori unik : Minuman, Makanan
Rekap pendapatan:
- Minuman: Rp524000
- Makanan: Rp125000
Jumlah kategori: 2
```

## Contoh Kasus Uji

| Perubahan data | Hasil yang diharapkan |
| --- | --- |
| Tambah menu `"Matcha"` kategori Minuman | Tetap 2 kategori, pendapatan Minuman bertambah |
| Tambah menu `"Roti"` kategori Makanan | Tetap 2 kategori, pendapatan Makanan bertambah |
| Tambah kategori `"Snack"` | Kategori unik menjadi 3 |
| Semua `terjual = 0` | Semua rekap bernilai `Rp0` |

## Checklist Sebelum Kumpul

- [ ] `Set` menghasilkan kategori tanpa duplikat.
- [ ] `Map` menyimpan kategori sebagai key.
- [ ] Akumulasi memakai nilai sebelumnya, bukan menimpa.
- [ ] Iterasi `Map` menghasilkan key dan value yang benar.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Buat `Map` kedua berisi jumlah menu per kategori.
2. Gunakan `Set` untuk menampilkan nama menu unik (tanpa duplikat).
3. Jelaskan dalam komentar: apa perbedaan `Set` dan `Map`?
