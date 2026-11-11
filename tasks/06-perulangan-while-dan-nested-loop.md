# Task 06 — Perulangan while & Nested Loop: Hitung Mundur dan Pola

> **Level:** Dasar · **Estimasi:** 45 menit · **Topik:** `while`, nested `for`, pola bintang

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menggunakan `while` untuk perulangan yang berhenti berdasarkan kondisi.
2. Menulis perulangan bersarang (nested loop).
3. Menghasilkan pola baris dan kolom.

## Studi Kasus

Dapur Kopi Senja memakai hitung mundur untuk menandai waktu penyajian pesanan. Setelah hitung mundur selesai, muncul pesan bahwa pesanan siap. Selain itu, barista magang diminta membuat pola bintang untuk latihan mencetak baris dan kolom — keterampilan yang nanti dipakai untuk membuat tabel dan grid di browser.

## Bagian A — Hitung Mundur

Buat hitung mundur dari **10 sampai 1** menggunakan `while`, lalu cetak `Pesanan siap!`.

## Bagian B — Pola Bintang

Buat pola segitiga siku-siku dengan **5 baris** menggunakan **nested loop**:

- Baris 1 berisi 1 bintang.
- Baris 2 berisi 2 bintang.
- Dan seterusnya sampai baris 5.

## Yang Harus Dibuat

Buat file **`task-06.js`** dengan dua bagian yang dipisahkan satu baris kosong:

1. Cetak judul `HITUNG MUNDUR PESANAN`.
2. Cetak angka 10 sampai 1, masing-masing di baris baru.
3. Cetak `Pesanan siap!`.
4. Cetak satu baris kosong.
5. Cetak judul `POLA BINTANG`.
6. Cetak pola bintang 5 baris.

## Ketentuan

- Bagian hitung mundur wajib memakai `while`.
- Bagian pola wajib memakai **dua** perulangan `for` (satu di dalam yang lain).
- Jangan menggunakan `.repeat()` atau string bintang yang ditulis manual per baris.
- Variabel penghitung harus berubah di dalam loop agar tidak terjadi infinite loop.

## Ekspektasi Output

Jalankan `node task-06.js`. Output harus **persis** seperti ini:

```text
HITUNG MUNDUR PESANAN
10
9
8
7
6
5
4
3
2
1
Pesanan siap!

POLA BINTANG
*
**
***
****
*****
```

## Contoh Kasus Uji

| Perubahan | Hasil yang diharapkan |
| --- | --- |
| Hitung mundur mulai 3 | `3`, `2`, `1`, lalu `Pesanan siap!` |
| Pola 3 baris | `*`, `**`, `***` |
| Pola 1 baris | `*` |
| Hitung mundur mulai 0 | Langsung `Pesanan siap!` tanpa angka |

## Checklist Sebelum Kumpul

- [ ] `while` berhenti dengan benar dan tidak infinite loop.
- [ ] Angka 10 sampai 1 tampil turun.
- [ ] Pola memiliki tepat 5 baris.
- [ ] Setiap baris pola bertambah satu bintang.
- [ ] Tidak ada spasi tambahan di akhir baris bintang.

## Bonus

1. Buat pola piramida rata tengah dengan 5 baris.
2. Buat hitung mundur yang mencetak `Kopi Senja` setiap angka kelipatan 3, menggantikan angkanya.
3. Jelaskan dalam komentar: apa fungsi loop dalam (inner loop) pada pola bintang?
