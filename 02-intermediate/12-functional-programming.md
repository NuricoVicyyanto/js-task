# Task I12 — Functional Programming: Curry, Pipe, Immutable

> **Level:** Intermediate · **Estimasi:** 90 menit · **Topik:** pure function, curry, pipe, immutable update, komposisi

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menyusun fungsi kecil yang murni dan dapat dikomposisi.
2. Membuat `curry` dan `pipe` tanpa library.
3. Memperbarui data tanpa memutasi objek/array asli.

## Studi Kasus

Perhitungan harga Kopi Senja tersebar di banyak tempat: pajak di satu fungsi, diskon di fungsi lain, pembulatan di tempat ketiga. Tim ingin menyusunnya sebagai **pipeline** yang mudah dibaca dan diuji. Selain itu, perubahan harga menu harus menghasilkan data baru agar riwayat transaksi tidak berubah.

## Yang Harus Dibuat

Buat file **`task-i12.js`** dengan:

### 1. `curry(fn)`

- Mendukung pemanggilan bertahap: `curry((a, b, c) => a + b + c)(1)(2)(3)` → `6`.
- Mendukung beberapa argument sekaligus: `curry(fn)(1, 2)(3)` → `6`.
- Jika jumlah argument sudah cukup, panggil `fn`.

### 2. `pipe(...fns)`

- Menjalankan fungsi dari kiri ke kanan.
- `pipe(f, g)(x)` sama dengan `g(f(x))`.
- `pipe()` tanpa fungsi mengembalikan fungsi identitas.

### 3. `updateMenu(menu, id, changes)`

- Mengembalikan array baru dengan item `id` yang diperbarui.
- Tidak mengubah array asli atau objek asli.
- Jika `id` tidak ditemukan, kembalikan salinan array tanpa perubahan.

### 4. `tambahItem(menu, item)`

- Mengembalikan array baru berisi item baru di akhir.
- Tidak mengubah array asli.

### 5. Pipeline harga

- `tambahPajak(persen)` → fungsi `harga => Math.round(harga * (1 + persen / 100))`
- `diskon(persen)` → fungsi `harga => Math.round(harga * (1 - persen / 100))`
- `bulatkan` → `Math.round`
- Susun pipeline: pajak 11% → diskon 10% → bulatkan.

## Skenario Program

```js
const menu = [
  { id: 1, nama: "Espresso", harga: 18000 },
  { id: 2, nama: "Latte", harga: 24000 },
];

console.log("Pipe total: Rp" + pipe(tambahPajak(11), diskon(10), bulatkan)(60000));
console.log("Curry:", curry((a, b, c) => a + b + c)(1)(2)(3));

const menuBaru = updateMenu(menu, 1, { harga: 20000 });
console.log("Menu lama: Rp" + menu[0].harga);
console.log("Menu baru: Rp" + menuBaru[0].harga);

const denganItem = tambahItem(menu, { id: 3, nama: "Matcha", harga: 26000 });
console.log("Jumlah lama:", menu.length);
console.log("Jumlah baru:", denganItem.length);
```

## Ekspektasi Output

```text
Pipe total: Rp59940
Curry: 6
Menu lama: Rp18000
Menu baru: Rp20000
Jumlah lama: 2
Jumlah baru: 3
```

## Ketentuan

- Semua fungsi pipeline harus **pure**: tidak memutasi input dan tidak memakai state global.
- `pipe` harus meneruskan nilai dari fungsi sebelumnya.
- `updateMenu` wajib memakai `map` dan spread.
- `tambahItem` wajib memakai spread.
- `curry` tidak boleh memakai `eval` atau `arguments` jika bisa dihindari.
- Jangan menulis `menu[0].harga = ...` atau `menu.push(...)`.

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| `pipe()` dengan `5` | `5` |
| `pipe((x) => x + 1, (x) => x * 2)(3)` | `8` |
| `curry(fn)(1, 2)(3)` | `6` |
| `curry(fn)(1)(2)(3)` | `6` |
| Update id yang tidak ada | salinan array, isi sama |
| Array asli setelah update | tidak berubah |

## Checklist Sebelum Kumpul

- [ ] `curry` mendukung satu per satu dan beberapa argument.
- [ ] `pipe` berjalan kiri ke kanan.
- [ ] `updateMenu` tidak mengubah data asli.
- [ ] `tambahItem` tidak mengubah array asli.
- [ ] Pipeline menghasilkan `59940`.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Buat `compose(...fns)` yang berjalan kanan ke kiri.
2. Tambahkan placeholder `_` pada `curry` untuk melewati argument.
3. Buat `pipeAsync(...fns)` yang mendukung fungsi async.
