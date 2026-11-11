# Task 05 — Perulangan for: Cetak Menu

> **Level:** Dasar · **Estimasi:** 40 menit · **Topik:** `for`, indeks, `.length`, akumulasi string

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menulis perulangan `for` dengan indeks.
2. Mengakses elemen array menggunakan indeks.
3. Membangun teks berulang tanpa menulis baris satu per satu.

## Studi Kasus

Kopi Senja menambah menu baru setiap bulan. Kasir meminta daftar menu otomatis yang bisa dicetak ke terminal. Jika suatu hari menu bertambah, program harus tetap menampilkan semua menu tanpa perlu mengubah banyak baris kode.

Daftar menu saat ini:

```text
Espresso
Latte
Kopi Susu
Croissant
```

> Catatan: array dipakai sebagai daftar sederhana. Pembahasan mendalam tentang array ada di **Task 09**.

## Yang Harus Dibuat

Buat file **`task-05.js`** yang:

1. Menyimpan nama-nama menu dalam satu array.
2. Mencetak garis pembatas sepanjang **20 karakter** menggunakan perulangan.
3. Mencetak judul `MENU KOPI SENJA`.
4. Mencetak setiap menu dengan nomor urut mulai dari 1.
5. Mencetak garis penutup.

## Ketentuan

- Gunakan perulangan `for` klasik (`for (let i = 0; ...)`).
- Jangan menggunakan `.repeat()`, `.forEach()`, atau `.map()`.
- Nomor urut dihitung dari indeks array, bukan ditulis manual.
- Jika array kosong, program tetap mencetak judul dan garis tanpa error.

## Ekspektasi Output

Jalankan `node task-05.js`. Output harus **persis** seperti ini:

```text
====================
MENU KOPI SENJA
====================
1. Espresso
2. Latte
3. Kopi Susu
4. Croissant
====================
```

## Contoh Kasus Uji

| Isi array | Hasil yang diharapkan |
| --- | --- |
| 4 menu di atas | Nomor 1 sampai 4 tampil berurutan |
| Tambah `"Matcha"` di akhir | Baris `5. Matcha` muncul |
| Array kosong | Hanya garis dan judul, tanpa error |
| Menu dihapus dari tengah | Nomor tetap berurutan tanpa lompat |

## Checklist Sebelum Kumpul

- [ ] Garis tepat 20 karakter `=`.
- [ ] Garis dibuat dengan perulangan, bukan ditulis manual.
- [ ] Nomor menu dimulai dari 1, bukan 0.
- [ ] Semua menu tampil, termasuk menu terakhir.
- [ ] Tidak ada `.repeat()`, `.forEach()`, atau `.map()`.

## Bonus

1. Tambahkan harga di samping nama menu, misalnya `1. Espresso — Rp18000`, menggunakan array harga yang sejajar dengan array menu.
2. Cetak menu dalam urutan terbalik (menu terakhir muncul lebih dulu).
3. Jelaskan dalam komentar: mengapa kondisi `i < menu.length` lebih aman daripada `i <= 3`?
