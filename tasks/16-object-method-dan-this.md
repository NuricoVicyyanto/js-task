# Task 16 — Object Method & `this`: Keranjang Belanja

> **Level:** Menengah · **Estimasi:** 60 menit · **Topik:** method objek, `this`, mutasi terkontrol, method chaining sederhana

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menambahkan fungsi sebagai method di dalam objek.
2. Mengakses properti objek lain melalui `this`.
3. Menjaga data tetap konsisten melalui method, bukan akses langsung.

## Studi Kasus

Kasir Kopi Senja membutuhkan keranjang belanja yang bisa menambah item, menghapus item, dan menghitung total. Agar kasir tidak mengubah array `items` secara sembarangan, semua operasi harus dilakukan melalui method keranjang.

## Yang Harus Dibuat

Buat file **`task-16.js`** dengan objek:

```js
const keranjang = {
  items: [],
  tambah(nama, harga) {
    // TODO
  },
  hapus(nama) {
    // TODO
  },
  total() {
    // TODO
  },
};
```

Method yang wajib dibuat:

| Method | Tugas |
| --- | --- |
| `tambah(nama, harga)` | menambahkan `{ nama, harga }` ke `this.items` |
| `hapus(nama)` | menghapus semua item dengan nama tersebut |
| `total()` | mengembalikan jumlah `harga` semua item |

Lalu simulasi:

1. Tambah Espresso Rp18.000.
2. Tambah Latte Rp24.000.
3. Cetak jumlah item dan total.
4. Hapus Latte.
5. Cetak jumlah item dan total lagi.

## Ketentuan

- Gunakan method dengan sintaks `namaMethod() { ... }`, bukan arrow function, agar `this` menunjuk objek keranjang.
- `tambah` memakai `this.items.push`.
- `hapus` memakai `this.items.filter` dan menimpa `this.items` dengan hasilnya.
- `total` memakai `reduce`.
- Jangan mengakses `items` dari luar objek setelah data dimasukkan.

## Ekspektasi Output

```text
Jumlah item: 2
Total: Rp42000
Setelah hapus Latte:
Jumlah item: 1
Total: Rp18000
```

## Contoh Kasus Uji

| Operasi | Hasil |
| --- | --- |
| `tambah("Croissant", 25000)` | jumlah item bertambah 1 |
| `hapus("Teh")` | data tidak berubah |
| `hapus("Latte")` dua kali | tetap tidak error, item tetap 1 |
| `total()` saat kosong | `0` |

## Checklist Sebelum Kumpul

- [ ] Tiga method ada dan namanya sesuai.
- [ ] `this.items` dipakai di dalam method.
- [ ] `hapus` menghapus berdasarkan nama.
- [ ] `total` mengembalikan angka, bukan string.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Tambahkan method `kosongkan()` untuk menghapus semua item.
2. Tambahkan method `cari(nama)` yang mengembalikan objek item atau `undefined`.
3. Jelaskan dalam komentar: mengapa arrow function tidak cocok untuk method yang memakai `this`?
