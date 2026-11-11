# Task 01 — Variabel & Tipe Data: Kartu Profil Barista

> **Level:** Dasar · **Estimasi:** 30 menit · **Topik:** `const`, `let`, `string`, `number`, `boolean`, template literal, `typeof`

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Membuat variabel dengan `const` dan `let`.
2. Menyimpan teks, angka, dan nilai benar/salah ke tipe data yang tepat.
3. Menampilkan variabel menggunakan template literal (backtick).

## Studi Kasus

Kopi Senja baru merekrut barista bernama **Sakti**. HRD meminta kartu profil digital sederhana yang bisa ditampilkan di terminal. Data yang harus tampil adalah nama, umur, shift kerja, dan status aktif.

Karena belum ada database, semua data ditulis langsung di dalam kode. Tugasmu membuat file program yang menyimpan data tersebut ke variabel, lalu mencetaknya dengan format yang sudah ditentukan.

## Yang Harus Dibuat

Buat file baru bernama **`task-01.js`**. Isi file tersebut dengan:

1. Variabel `nama` berisi `"Sakti"`.
2. Variabel `umur` berisi `20`.
3. Variabel `shift` berisi `"pagi"`.
4. Variabel `isAktif` berisi `true`.
5. Cetak kartu profil persis seperti format di bawah.
6. Cetak tipe data `umur` dan `isAktif` menggunakan `typeof`.

## Ketentuan

- Gunakan `const` untuk semua data karena nilainya tidak berubah.
- Gunakan template literal untuk mencetak, bukan penggabungan `+`.
- Jangan menulis angka atau teks profil langsung di dalam `console.log`; ambil dari variabel.
- Nama variabel harus sama dengan yang diminta.

## Ekspektasi Output

Jalankan `node task-01.js`. Output harus **persis** seperti ini:

```text
=== KARTU PROFIL BARISTA ===
Nama    : Sakti
Umur    : 20 tahun
Shift   : pagi
Aktif   : true
Tipe umur  : number
Tipe aktif : boolean
```

## Contoh Kasus Uji

Ubah nilai variabel, lalu pastikan hasilnya ikut berubah.

| Data | Hasil yang diharapkan |
| --- | --- |
| `nama = "Nadia"` | Baris `Nama    : Nadia` |
| `umur = 22` | Baris `Umur    : 22 tahun` |
| `isAktif = false` | Baris `Aktif   : false` |
| `typeof shift` | `string` |

## Checklist Sebelum Kumpul

- [ ] File bernama `task-01.js`.
- [ ] Semua data disimpan di variabel, bukan ditulis langsung di output.
- [ ] `const` dipakai untuk semua variabel.
- [ ] Output sama persis dengan contoh, termasuk huruf besar/kecil.
- [ ] `typeof` menunjukkan `number` dan `boolean` dengan benar.

## Bonus

1. Tambahkan variabel `jamKerja` berisi `8`, lalu cetak `Jam kerja : 8 jam`.
2. Buat variabel `gajiPerJam` dan hitung `gajiHarian = jamKerja * gajiPerJam`. Cetak hasilnya.
3. Jelaskan dalam komentar singkat: mengapa `umur` sebaiknya `number`, bukan `"20"`?
