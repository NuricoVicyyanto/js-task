# Task 23 — Regex Dasar: Validasi Kontak & Voucher

> **Level:** Menengah · **Estimasi:** 60 menit · **Topik:** regex literal, anchor `^ $`, `\d`, quantifier `{8,11}`, `.test()`

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Membuat pola regex sederhana dengan anchor dan quantifier.
2. Menguji string menggunakan `.test()`.
3. Menjelaskan mengapa urutan dan jangkar karakter penting dalam validasi.

## Studi Kasus

Kopi Senja menerima data pelanggan dari formulir. Sebelum data disimpan, kasir harus memastikan nomor telepon, email, dan kode voucher memiliki format yang benar. Validasi dilakukan dengan regex agar aturannya konsisten.

## Aturan Format

| Data | Aturan | Contoh valid | Contoh tidak valid |
| --- | --- | --- | --- |
| Telepon | diawali `08`, lalu 8–11 digit angka | `081234567890` | `0812-3456` |
| Email | ada teks, `@`, teks, titik, teks; tanpa spasi | `nadia@kopisenja.id` | `nadia@` |
| Voucher | `SENJA` + tepat 2 digit | `SENJA10` | `senja10` |

Gunakan pola:

```js
const polaTelepon = /^08\d{8,11}$/;
const polaEmail = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
const polaVoucher = /^SENJA\d{2}$/;
```

## Yang Harus Dibuat

Buat file **`task-23.js`** dengan:

1. Fungsi `periksa(label, nilai, pola)` yang mencetak `valid` atau `tidak valid` menggunakan `pola.test(nilai)`.
2. Uji minimal dua nilai untuk setiap pola: satu valid, satu tidak valid.
3. Cetak hasil dengan format di bawah.

## Ketentuan

- Gunakan regex literal (`/.../`), bukan `new RegExp("...")`.
- Gunakan `.test()`, bukan `.match()` atau `.replace()`.
- Jangan menambahkan `if` manual untuk memeriksa panjang atau karakter; semua aturan harus ada di regex.
- Voucher bersifat case-sensitive.

## Ekspektasi Output

```text
Telepon 081234567890 : valid
Telepon 0812-3456    : tidak valid
Email nadia@kopisenja.id : valid
Email nadia@         : tidak valid
Voucher SENJA10      : valid
Voucher senja10      : tidak valid
```

## Contoh Kasus Uji

| Nilai | Pola | Hasil |
| --- | --- | --- |
| `0812345678` | telepon | valid |
| `081234567` | telepon | tidak valid |
| `" 081234567890"` | telepon | tidak valid (ada spasi) |
| `nadia@kopisenja` | email | tidak valid (tanpa titik) |
| `nadia @kopisenja.id` | email | tidak valid (ada spasi) |
| `SENJA100` | voucher | tidak valid |
| `SENJA1` | voucher | tidak valid |

## Checklist Sebelum Kumpul

- [ ] Ketiga pola memakai anchor `^` dan `$`.
- [ ] Telepon hanya menerima angka setelah `08`.
- [ ] Email menolak spasi dan alamat tanpa titik.
- [ ] Voucher menolak huruf kecil.
- [ ] Validasi memakai `.test()`.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Buat pola telepon yang menerima format `+62` sebagai alternatif.
2. Buat pola voucher yang menerima `SENJA` diikuti 2–3 digit.
3. Gunakan `.replace()` untuk menghapus semua karakter selain angka dari nomor telepon sebelum validasi.
