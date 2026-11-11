# Task 15 — Nested Object & Array: Detail Pesanan

> **Level:** Menengah · **Estimasi:** 60 menit · **Topik:** objek bersarang, array di dalam objek, akses bertingkat, perhitungan subtotal

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Mengakses properti objek yang berada di dalam objek lain.
2. Mengakses array of objects di dalam objek.
3. Menghitung nilai dari data bersarang tanpa menyalin manual.

## Studi Kasus

Sistem Kopi Senja menerima pesanan dengan data pelanggan, alamat, dan daftar item. Semua informasi disimpan dalam satu objek pesanan. Kasir perlu mencetak ringkasan pesanan yang menghitung subtotal dari daftar item.

## Data Awal

```js
const pesanan = {
  id: "KS-001",
  pelanggan: {
    nama: "Nadia",
    telepon: "08123456789",
  },
  alamat: {
    jalan: "Jl. Merdeka 10",
    kota: "Bandung",
  },
  items: [
    { nama: "Espresso", harga: 18000, jumlah: 2 },
    { nama: "Latte", harga: 24000, jumlah: 1 },
  ],
};
```

Ongkir tetap **Rp10.000** untuk task ini.

## Yang Harus Dibuat

Buat file **`task-15.js`** yang:

1. Mengambil nama dan telepon pelanggan dari objek bersarang.
2. Menggabungkan jalan dan kota menjadi satu baris alamat.
3. Membuat ringkasan item dalam format `2x Espresso, 1x Latte`.
4. Menghitung subtotal dari `harga * jumlah` setiap item.
5. Menghitung total = subtotal + ongkir.
6. Mencetak ringkasan sesuai format.

## Ketentuan

- Jangan menyalin nilai pelanggan, alamat, atau item secara manual ke output.
- Subtotal dihitung dengan perulangan atau `reduce`, bukan angka jadi.
- Format item: `jumlah` + `x` + spasi + `nama`, dipisahkan `, `.
- Ongkir disimpan di variabel `const ongkir = 10000`.

## Ekspektasi Output

```text
ID Pesanan : KS-001
Pelanggan  : Nadia (08123456789)
Alamat     : Jl. Merdeka 10, Bandung
Item       : 2x Espresso, 1x Latte
Subtotal   : Rp60000
Ongkir     : Rp10000
Total      : Rp70000
```

## Contoh Kasus Uji

| Perubahan | Hasil yang diharapkan |
| --- | --- |
| Jumlah Espresso menjadi 3 | Subtotal `Rp78000`, total `Rp88000` |
| Tambah item Croissant 1 × 25000 | Item bertambah, subtotal naik |
| `items` kosong | Item string kosong, subtotal `Rp0`, total `Rp10000` |
| Kota diubah menjadi `"Jakarta"` | Baris alamat ikut berubah |

## Checklist Sebelum Kumpul

- [ ] Data pelanggan diambil dari objek bersarang, bukan ditulis ulang.
- [ ] Alamat menggabungkan jalan dan kota.
- [ ] Ringkasan item mengikuti format `2x Espresso`.
- [ ] Subtotal dihitung dari semua item.
- [ ] Total = subtotal + ongkir.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Tambahkan properti `catatan` di dalam `pesanan` dan cetak jika ada.
2. Hitung total porsi (jumlah semua `jumlah`) dan tampilkan sebagai `Total porsi`.
3. Gunakan nested destructuring untuk mengambil `nama`, `telepon`, dan `kota` dalam satu baris.
