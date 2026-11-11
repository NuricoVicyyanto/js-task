# Task 27 — localStorage: Simpan Keranjang

> **Level:** Lanjutan · **Estimasi:** 75 menit · **Topik:** `localStorage`, `JSON.stringify`, `JSON.parse`, persistensi data

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menyimpan data ke `localStorage`.
2. Membaca kembali data yang tersimpan saat halaman dimuat.
3. Menghapus data dari `localStorage`.
4. Menangani data rusak dengan `try/catch`.

## Studi Kasus

Keranjang di Task 26 hilang setiap kali halaman di-refresh. Kasir Kopi Senja ingin keranjang tetap tersimpan meskipun browser ditutup. Gunakan `localStorage` agar data bertahan di perangkat yang sama.

## File yang Dibuat

```text
task-27.html
task-27.js
```

Gunakan struktur HTML dari Task 26, lalu tambahkan tombol:

```html
<button id="tombol-kosongkan" type="button">Kosongkan Keranjang</button>
```

## Yang Harus Dibuat

File **`task-27.js`** harus:

1. Menyimpan keranjang sebagai array of objects: `[{ nama, harga }, ...]`.
2. Menyimpan array tersebut ke `localStorage` dengan key **`keranjang-kopi-senja`** setiap kali item ditambah atau dihapus.
3. Saat halaman dimuat, membaca data dari `localStorage` dan merender ulang item.
4. Menampilkan total yang sesuai setelah data dimuat.
5. Tombol `Kosongkan Keranjang` menghapus semua item dan memanggil `localStorage.removeItem`.
6. Jika data di `localStorage` rusak (bukan JSON valid), tangkap error, mulai dengan keranjang kosong, dan tampilkan pesan di console.

## Ketentuan

- Gunakan `JSON.stringify()` saat menyimpan.
- Gunakan `JSON.parse()` saat membaca.
- Jangan menyimpan objek DOM atau fungsi ke `localStorage`.
- Bungkus `JSON.parse` dengan `try/catch`.
- Gunakan key yang sama persis: `"keranjang-kopi-senja"`.
- Data harus tetap tampil setelah halaman di-refresh.

## Ekspektasi Perilaku

| Langkah | Hasil |
| --- | --- |
| Tambah Espresso Rp18000 | Item muncul, total `Rp18000`, data tersimpan |
| Tambah Latte Rp24000 | Total `Rp42000`, data tersimpan |
| Refresh halaman | Kedua item dan total `Rp42000` tetap tampil |
| Hapus Espresso | Total `Rp24000`, data tersimpan |
| Refresh lagi | Hanya Latte yang tampil |
| Klik Kosongkan | Daftar kosong, total `Rp0`, key terhapus |
| Refresh setelah kosong | Tetap kosong |

## Cara Memeriksa

1. Buka halaman, tambahkan dua item.
2. Refresh. Item harus tetap ada.
3. Buka DevTools → Application → Local Storage.
4. Cari key `keranjang-kopi-senja`; isinya harus JSON array.
5. Klik Kosongkan, lalu pastikan key tersebut hilang.
6. Untuk menguji data rusak, ubah value menjadi `bukan-json`, lalu refresh. Halaman tidak boleh crash.

## Checklist Sebelum Kumpul

- [ ] Data disimpan setiap kali keranjang berubah.
- [ ] Data dimuat saat halaman pertama kali dibuka.
- [ ] Total dihitung dari data yang dimuat.
- [ ] Tombol kosongkan menghapus data dari `localStorage`.
- [ ] JSON rusak ditangani dengan `try/catch`.
- [ ] Key sesuai: `keranjang-kopi-senja`.
- [ ] Tidak ada error di console saat alur normal.

## Bonus

1. Simpan juga waktu terakhir keranjang diubah dan tampilkan di halaman.
2. Tambahkan tombol `Ekspor` yang menyalin JSON keranjang ke clipboard.
3. Beri versi data, misalnya `{ versi: 1, items: [...] }`, agar mudah dimigrasikan di masa depan.
