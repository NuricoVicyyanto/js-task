# Task 12 — Array of Objects: map & filter

> **Level:** Menengah · **Estimasi:** 60 menit · **Topik:** array of objects, `.map()`, `.filter()`, chaining, immutability

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menyimpan banyak data terstruktur dalam array of objects.
2. Mengambil satu properti dari semua objek dengan `.map()`.
3. Menyaring data berdasarkan kondisi dengan `.filter()`.
4. Menggabungkan `filter` dan `map` tanpa mengubah data asli.

## Studi Kasus

Kopi Senja punya empat menu. Manajer ingin melihat beberapa laporan cepat:

- semua nama menu,
- menu kategori minuman,
- menu yang sedang tersedia,
- menu dengan harga di bawah Rp25.000.

Semua laporan harus dihitung dari **satu sumber data**, bukan ditulis manual.

## Data Awal

Gunakan data berikut:

```js
const menu = [
  { nama: "Espresso", kategori: "Minuman", harga: 18000, tersedia: true },
  { nama: "Latte", kategori: "Minuman", harga: 24000, tersedia: true },
  { nama: "Kopi Susu", kategori: "Minuman", harga: 22000, tersedia: false },
  { nama: "Croissant", kategori: "Makanan", harga: 25000, tersedia: true },
];
```

## Yang Harus Dibuat

Buat file **`task-12.js`** yang menghasilkan empat laporan:

1. `semuaNama` — semua nama menu menggunakan `map`.
2. `menuMinuman` — menu dengan `kategori === "Minuman"` menggunakan `filter`.
3. `menuTersedia` — menu dengan `tersedia === true`.
4. `menuMurah` — menu dengan `harga < 25000`.

Setiap laporan dicetak sebagai nama menu yang dipisahkan `, `.

## Ketentuan

- Gunakan `.map()` untuk mengambil nama.
- Gunakan `.filter()` untuk menyaring data.
- Jangan mengubah array `menu` asli.
- Untuk laporan yang membutuhkan nama, gunakan `filter(...).map(...)`.
- Jangan menulis daftar nama hasil secara manual.

## Ekspektasi Output

```text
Semua nama    : Espresso, Latte, Kopi Susu, Croissant
Menu minuman  : Espresso, Latte, Kopi Susu
Menu tersedia : Espresso, Latte, Croissant
Di bawah 25000: Espresso, Latte, Kopi Susu
Jumlah data   : 4
```

## Contoh Kasus Uji

| Perubahan data | Hasil yang diharapkan |
| --- | --- |
| `Latte.tersedia = false` | `Menu tersedia` tidak memuat Latte |
| Tambah menu `"Matcha"` kategori Minuman | Muncul di `Semua nama` dan `Menu minuman` |
| Harga Croissant menjadi `24000` | Croissant masuk `Di bawah 25000` |
| Semua `tersedia = false` | Laporan tersedia kosong (string kosong) |

## Checklist Sebelum Kumpul

- [ ] Data awal berisi 4 objek.
- [ ] `.map()` menghasilkan array nama, bukan array objek.
- [ ] `.filter()` memakai kondisi yang tepat.
- [ ] `harga < 25000` tidak memasukkan harga yang sama dengan 25000.
- [ ] Array asli tetap 4 item setelah semua laporan dibuat.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Buat laporan `Menu tersedia di bawah Rp25.000` dengan menggabungkan dua kondisi di dalam `filter`.
2. Buat `daftarLabel` berisi string seperti `"Espresso (Rp18000)"` menggunakan `map`.
3. Jelaskan dalam komentar: apa perbedaan `.map()` dan `.filter()` dari sisi jumlah elemen hasil?
