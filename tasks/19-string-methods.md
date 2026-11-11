# Task 19 — String Methods: Pencarian Menu

> **Level:** Menengah · **Estimasi:** 50 menit · **Topik:** `trim()`, `toLowerCase()`, `toUpperCase()`, `includes()`, `slice()`

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Membersihkan input pengguna dengan `trim()`.
2. Menyeragamkan huruf dengan `toLowerCase()` dan `toUpperCase()`.
3. Mencari kata di dalam string menggunakan `includes()`.
4. Mengambil sebagian string dengan `slice()`.

## Studi Kasus

Pelanggan sering mengetik nama menu dengan huruf besar-kecil campur dan spasi berlebih, misalnya `"  LATTE "`. Pencarian kasir harus tetap menemukan `Latte`. Selain itu, setiap menu perlu kode singkat tiga huruf pertama untuk struk.

## Data Awal

```js
const menu = ["Espresso", "Latte", "Kopi Susu", "Croissant"];
const kataKunci = "  LATTE ";
```

## Yang Harus Dibuat

Buat file **`task-19.js`** yang:

1. Membersihkan `kataKunci` dengan `trim()` dan `toLowerCase()`.
2. Mencari menu yang mengandung kata kunci tersebut (tanpa membedakan huruf besar/kecil).
3. Menampilkan hasil pencarian. Jika lebih dari satu, pisahkan dengan `, `.
4. Mengambil kode menu dari hasil pertama: tiga huruf pertama, huruf besar.
5. Mencetak semua nama menu dalam huruf besar.

## Ketentuan

- Gunakan `trim()`, `toLowerCase()`, `includes()`, `slice()`, dan `toUpperCase()`.
- Jangan mengubah array `menu` asli.
- Pencarian harus **case-insensitive**.
- Jika kata kunci kosong setelah `trim()`, tampilkan `Hasil cari : (tidak ada)`.
- Jika tidak ada hasil, tampilkan `Hasil cari : (tidak ada)` dan `Kode menu : -`.

## Ekspektasi Output

```text
Kata kunci asli   : "  LATTE "
Kata kunci bersih : latte
Hasil cari        : Latte
Kode menu         : LAT
Semua nama        : ESPRESSO, LATTE, KOPI SUSU, CROISSANT
```

## Contoh Kasus Uji

| `kataKunci` | Hasil cari |
| --- | --- |
| `"  LATTE "` | `Latte` |
| `"kopi"` | `Kopi Susu` |
| `"SUSU"` | `Kopi Susu` |
| `"te"` | `Latte` |
| `"teh"` | `(tidak ada)` |
| `"   "` | `(tidak ada)` |

## Checklist Sebelum Kumpul

- [ ] Input dibersihkan sebelum dibandingkan.
- [ ] Pencarian tidak membedakan huruf besar/kecil.
- [ ] Hasil lebih dari satu digabung dengan `, `.
- [ ] Kode menu diambil dari hasil pertama, bukan ditulis manual.
- [ ] Kata kunci kosong ditangani tanpa error.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Cari menu yang **diawali** kata kunci menggunakan `startsWith()`.
2. Tampilkan posisi kata kunci di dalam nama menu menggunakan `indexOf()`.
3. Jelaskan dalam komentar: mengapa `includes()` lebih sederhana daripada membandingkan dengan `===`?
