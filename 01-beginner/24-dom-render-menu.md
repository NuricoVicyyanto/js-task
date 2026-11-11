# Task 24 — DOM: Tampilkan Menu

> **Level:** Lanjutan · **Estimasi:** 75 menit · **Topik:** `querySelector`, `createElement`, `textContent`, `append`, DOM rendering

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Memilih elemen HTML dengan `querySelector`.
2. Membuat elemen baru dengan `createElement`.
3. Mengisi teks dengan `textContent` dan memasukkannya ke halaman.

## Studi Kasus

Kopi Senja ingin menampilkan daftar menu di halaman web. Data menu sudah tersedia di JavaScript, tetapi belum muncul di layar. Tugasmu menghubungkan data dengan HTML: setiap menu menjadi satu kartu berisi nama dan harga.

## File yang Dibuat

Buat dua file di folder yang sama:

```text
task-24.html
task-24.js
```

### Struktur HTML minimal

```html
<!doctype html>
<html lang="id">
  <head>
    <meta charset="utf-8" />
    <title>Menu Kopi Senja</title>
  </head>
  <body>
    <main>
      <h1>Menu Kopi Senja</h1>
      <div id="daftar-menu"></div>
    </main>
    <script src="task-24.js"></script>
  </body>
</html>
```

Jangan mengubah `id="daftar-menu"`.

## Data Awal

```js
const menu = [
  { nama: "Espresso", kategori: "Minuman", harga: 18000 },
  { nama: "Latte", kategori: "Minuman", harga: 24000 },
  { nama: "Croissant", kategori: "Makanan", harga: 25000 },
];
```

## Yang Harus Dibuat

File **`task-24.js`** harus:

1. Mengambil elemen `#daftar-menu`.
2. Melakukan perulangan pada array `menu`.
3. Membuat satu elemen kartu untuk setiap menu, misalnya `<article>`.
4. Mengisi nama menu dengan `textContent`.
5. Mengisi kategori menu dengan `textContent`.
6. Mengisi harga dengan format `Rp18000`.
7. Menambahkan kartu ke `#daftar-menu`.

## Ketentuan

- Gunakan `document.querySelector()`.
- Gunakan `document.createElement()`.
- Gunakan `textContent`, **bukan** `innerHTML`, untuk mengisi data.
- Jangan memakai `document.write()`.
- Jangan menulis tiga kartu secara manual di HTML; kartu harus dibuat dari data.

## Ekspektasi Tampilan

Halaman menampilkan konten berikut di dalam `#daftar-menu`:

```text
Menu Kopi Senja

┌──────────────────────────┐
│ Espresso                 │
│ Minuman                  │
│ Rp18000                  │
└──────────────────────────┘
┌──────────────────────────┐
│ Latte                    │
│ Minuman                  │
│ Rp24000                  │
└──────────────────────────┘
┌──────────────────────────┐
│ Croissant                │
│ Makanan                  │
│ Rp25000                  │
└──────────────────────────┘
```

Di DevTools (klik kanan → Inspect), struktur `#daftar-menu` harus berisi **3 elemen kartu**. Setiap kartu berisi teks nama, kategori, dan harga.

## Cara Memeriksa

1. Buka `task-24.html` langsung di browser.
2. Buka DevTools → Console. Tidak boleh ada error merah.
3. Buka tab Elements, cari `#daftar-menu`.
4. Pastikan ada 3 kartu dan tidak ada teks `undefined`.

## Checklist Sebelum Kumpul

- [ ] Halaman menampilkan 3 kartu menu.
- [ ] Nama, kategori, dan harga berasal dari array.
- [ ] Harga memakai format `Rp` + angka.
- [ ] Tidak ada `innerHTML` atau `document.write`.
- [ ] Console browser bersih dari error.
- [ ] Jika satu menu ditambahkan ke array, kartu baru ikut muncul.

## Bonus

1. Tambahkan badge kategori dengan `class="badge"`.
2. Beri warna berbeda untuk kategori Minuman dan Makanan menggunakan CSS.
3. Tampilkan pesan `Menu sedang kosong` jika array `menu` kosong.
