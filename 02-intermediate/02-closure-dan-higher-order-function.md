# Task I02 — Closure & Higher-Order Function

> **Level:** Intermediate · **Estimasi:** 75 menit · **Topik:** closure, function factory, callback, memoization, state privat

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Membuat fungsi yang mengembalikan fungsi lain.
2. Menyimpan state privat menggunakan closure.
3. Membuat cache sederhana dengan `memoize`.

## Studi Kasus

Kopi Senja memiliki aturan diskon yang sering berubah. Alih-alih menulis `if` berulang, kasir ingin membuat **aturan diskon sebagai fungsi** yang bisa disimpan dan dipakai ulang. Selain itu, perhitungan laporan menu cukup berat, sehingga hasil yang sama tidak perlu dihitung dua kali.

## Yang Harus Dibuat

Buat file **`task-i02.js`** dengan tiga fungsi.

### 1. `buatAturanDiskon({ minBelanja, persen })`

Mengembalikan fungsi `(subtotal) => nominalDiskon`.

- Jika `subtotal < minBelanja`, kembalikan `0`.
- Jika memenuhi, kembalikan `Math.round(subtotal * persen / 100)`.
- Nilai `minBelanja` dan `persen` disimpan di closure, bukan global.

### 2. `buatPenghitung()`

Mengembalikan fungsi tanpa parameter. Setiap pemanggilan mengembalikan angka `1`, `2`, `3`, dan seterusnya. Tidak ada variabel penghitung global.

### 3. `memoize(fn)`

Mengembalikan versi `fn` yang menyimpan hasil berdasarkan argument. Pemanggilan dengan argument sama tidak boleh mengeksekusi `fn` lagi.

## Ekspektasi Output

Gunakan skenario berikut:

```js
const diskon10 = buatAturanDiskon({ minBelanja: 50000, persen: 10 });
const diskon20 = buatAturanDiskon({ minBelanja: 100000, persen: 20 });

console.log("Diskon 10%:", "Rp" + diskon10(60000));
console.log("Diskon 20%:", "Rp" + diskon20(60000));

const hitung = buatPenghitung();
console.log("Penghitung:", hitung() + ", " + hitung() + ", " + hitung());

let panggilan = 0;
const lambat = (n) => {
  panggilan += 1;
  return n * 2;
};
const cepat = memoize(lambat);
console.log(cepat(21), cepat(21));
console.log("Panggilan:", panggilan);
```

Output harus **persis**:

```text
Diskon 10%: Rp6000
Diskon 20%: Rp0
Penghitung: 1, 2, 3
42 42
Panggilan: 1
```

## Ketentuan

- `buatAturanDiskon` dan `buatPenghitung` wajib memakai closure.
- `memoize` harus mendukung lebih dari satu argument.
- Cache tidak boleh bocor ke luar fungsi.
- Jangan memakai variabel global untuk menyimpan state.
- Jangan mengubah `fn` asli yang dikirim ke `memoize`.

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| `diskon10(49999)` | `0` |
| `diskon10(50000)` | `5000` |
| `diskon20(100000)` | `20000` |
| Dua penghitung berbeda | Masing-masing mulai dari `1` |
| `cepat(5)` lalu `cepat(5)` | `fn` hanya dipanggil sekali |
| `cepat(5)` lalu `cepat(6)` | `fn` dipanggil lagi |

## Checklist Sebelum Kumpul

- [ ] Tidak ada state diskon di variabel global.
- [ ] Batas minimal belanja diuji tepat di angka batas.
- [ ] Dua instance penghitung tidak saling memengaruhi.
- [ ] `memoize` menyimpan hasil per kombinasi argument.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Tambahkan TTL pada cache `memoize`, misalnya hasil kedaluwarsa setelah 5 detik.
2. Buat `once(fn)` yang hanya boleh dieksekusi satu kali.
3. Buat `buatAturanDiskonBertingkat([...aturan])` yang memilih aturan terbaik untuk satu subtotal.
