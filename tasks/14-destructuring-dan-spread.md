# Task 14 — Destructuring & Spread: Update Pesanan

> **Level:** Menengah · **Estimasi:** 50 menit · **Topik:** object destructuring, array destructuring, spread operator, immutability

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Mengambil properti objek dengan destructuring.
2. Menyalin objek dan array menggunakan spread.
3. Memperbarui data tanpa mengubah data asli.

## Studi Kasus

Pesanan pelanggan berubah status dari `"baru"` menjadi `"diproses"`, dan pelanggan menambah satu item. Kopi Senja ingin menyimpan **riwayat versi lama** pesanan untuk audit. Artinya, objek pesanan lama tidak boleh diubah; perubahan harus menghasilkan objek baru.

## Data Awal

```js
const pesanan = {
  id: "KS-001",
  pelanggan: "Nadia",
  total: 60000,
  status: "baru",
  items: ["Espresso", "Latte"],
};
```

## Yang Harus Dibuat

Buat file **`task-14.js`** yang:

1. Mengambil `pelanggan` dan `total` dengan destructuring.
2. Membuat `pesananDiproses`, yaitu salinan `pesanan` dengan `status: "diproses"`.
3. Membuat `itemsBaru`, yaitu salinan `items` ditambah `"Croissant"`.
4. Mencetak data lama dan data baru untuk membuktikan data lama tidak berubah.

## Ketentuan

- Gunakan destructuring untuk mengambil `pelanggan` dan `total`.
- Gunakan spread `{ ...pesanan, status: "diproses" }` untuk objek.
- Gunakan spread `[...pesanan.items, "Croissant"]` untuk array.
- Jangan memakai `pesanan.status = ...` atau `pesanan.items.push(...)`.
- Jangan mengubah objek `pesanan` maupun array `pesanan.items`.

## Ekspektasi Output

```text
Pelanggan lama : Nadia
Total lama     : Rp60000
Status baru    : diproses
Item baru      : Espresso, Latte, Croissant
Pesanan lama   : baru
Item lama      : Espresso, Latte
```

## Contoh Kasus Uji

| Pemeriksaan | Hasil yang diharapkan |
| --- | --- |
| `pesanan.status` setelah update | tetap `"baru"` |
| `pesanan.items.length` | tetap `2` |
| `pesananDiproses.status` | `"diproses"` |
| `itemsBaru.length` | `3` |
| `pesananDiproses === pesanan` | `false` |

## Checklist Sebelum Kumpul

- [ ] Destructuring dipakai untuk `pelanggan` dan `total`.
- [ ] Objek baru dibuat dengan spread.
- [ ] Array baru dibuat dengan spread.
- [ ] Data lama tetap utuh setelah update.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Gunakan destructuring dengan nama baru: `const { pelanggan: namaPelanggan } = pesanan`.
2. Ambil sisa properti dengan rest: `const { items, ...infoPesanan } = pesanan`.
3. Tambahkan item tanpa membuat array baru, lalu jelaskan mengapa cara itu melanggar aturan immutability.
