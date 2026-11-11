# Rubrik Penilaian — 30 Task JavaScript Beginner

Rubrik ini dipakai untuk menilai seluruh task secara konsisten. Setiap task bernilai maksimal **100 poin**, dan **Task 30 (capstone) dihitung 2×** dalam nilai akhir.

---

## 1. Komponen Umum (Task 01–29)

| Komponen | Bobot | Yang Dinilai |
| --- | --- | --- |
| Kesesuaian output/perilaku | 50 | Output, nilai kembalian, atau perilaku UI sesuai ekspektasi task |
| Ketepatan konsep | 20 | Konsep yang diminta benar-benar dipakai (misalnya `reduce`, event, `fetch`) |
| Kasus batas & validasi | 15 | Input kosong, nol, negatif, data tidak ada, error, dan kondisi tepi |
| Kerapian kode | 10 | Nama jelas, indentasi konsisten, fungsi tidak terlalu panjang, tidak ada kode mati |
| Dokumentasi/refleksi | 5 | Komentar singkat, penjelasan bonus, atau refleksi sesuai instruksi |

### Deskriptor

| Nilai | Predikat | Deskripsi |
| --- | --- | --- |
| 90–100 | Sangat baik | Semua perilaku wajib benar, kasus batas ditangani, kode mudah dibaca |
| 75–89 | Baik | Perilaku utama benar, satu atau dua kasus batas terlewat |
| 60–74 | Cukup | Sebagian besar benar, tetapi ada kesalahan konsep atau output tidak persis |
| 45–59 | Kurang | Hanya sebagian kecil berjalan; perlu bimbingan terarah |
| 0–44 | Perlu bimbingan | Tidak berjalan, tidak dikumpulkan, atau tidak sesuai instruksi |

### Cara Menghitung Cepat

1. Mulai dari 100.
2. Kurangi 10–20 untuk setiap perilaku wajib yang gagal.
3. Kurangi 5 untuk setiap kasus batas yang tidak ditangani.
4. Kurangi 5–10 jika kode sulit dibaca atau konsep yang diminta tidak dipakai.
5. Tambahkan maksimal 10 untuk bonus (tidak melebihi 100).

---

## 2. Rubrik Khusus DOM (Task 24–27)

| Komponen | Bobot | Indikator |
| --- | --- | --- |
| Fungsionalitas | 45 | Render data, tambah item, hapus, total, simpan/muat berjalan |
| Interaksi & event | 20 | Event handler tepat, `preventDefault`, tidak ada reload tidak diinginkan |
| Ketahanan data | 15 | Total dihitung ulang, data kosong, data rusak, qty minimal |
| Kualitas DOM | 10 | `textContent`, `createElement`, `dataset`, tidak ada `innerHTML` untuk data pengguna |
| UI & aksesibilitas | 10 | Label input, tombol jelas, layout terbaca, empty state |

### Pengurangan khusus DOM

- `innerHTML` untuk data pengguna: **−15**.
- Halaman reload saat submit: **−10**.
- Total hanya ditambah, tidak dihitung ulang: **−10**.
- Data hilang setelah refresh pada Task 27: **−20**.
- Error console saat alur normal: **−5 per error**.

---

## 3. Rubrik Khusus Async (Task 28–29)

| Komponen | Bobot | Indikator |
| --- | --- | --- |
| Alur asynchronous | 40 | Callback/Promise/`await` berjalan sesuai urutan |
| Penanganan kegagalan | 25 | `response.ok`, `throw`, `try/catch`, pesan error ramah |
| Render data | 20 | Data dari JSON dirender tanpa hardcode |
| Kebersihan state | 15 | Loading hilang, tidak ada render ganda, tidak ada data setengah jadi |

### Pengurangan khusus async

- Memakai `fetch` tanpa memeriksa `response.ok`: **−10**.
- Data menu masih hardcode padahal diminta dari `menu.json`: **−20**.
- Loading tidak pernah hilang: **−10**.
- Error tidak ditangani sehingga halaman blank: **−15**.

---

## 4. Rubrik Capstone (Task 30)

Task 30 memakai rubrik tersendiri dan dihitung **2×**.

| Komponen | Bobot | Indikator |
| --- | --- | --- |
| Fungsionalitas inti | 40 | Tambah, qty, hapus, subtotal, diskon, pajak, total benar |
| Pembayaran & struk | 20 | Struk akurat, reset setelah bayar, batal tidak mereset |
| Penyimpanan | 15 | `localStorage`, pemulihan, data rusak ditangani |
| Validasi & kasus batas | 10 | Qty minimal, voucher, keranjang kosong, tombol nonaktif |
| Kualitas kode | 10 | Fungsi terpisah, penamaan jelas, tidak ada duplikasi besar |
| UI & dokumentasi | 5 | Layout rapi, README proyek lengkap |

### Rincian Fungsionalitas Inti (40 poin)

| Fitur | Poin |
| --- | --- |
| Daftar menu tampil dari data | 5 |
| Tambah ke keranjang | 5 |
| Menu sama menambah qty, bukan duplikat | 5 |
| Tombol `+` / `−` dan batas qty minimal 1 | 5 |
| Hapus baris dan kosongkan keranjang | 5 |
| Subtotal benar | 5 |
| Voucher `SENJA10` / `SENJA20` beserta minimal belanja | 5 |
| Pajak 11% setelah diskon dan total benar | 5 |

### Rincian Pembayaran & Struk (20 poin)

| Fitur | Poin |
| --- | --- |
| Tombol Bayar aktif hanya saat ada item | 4 |
| Struk menampilkan item dan qty | 4 |
| Struk menampilkan subtotal, diskon, pajak, total | 6 |
| Setelah bayar, keranjang dan localStorage bersih | 4 |
| Tombol Batal tidak mengosongkan keranjang | 2 |

### Bonus Capstone

Maksimal **+10**, tidak boleh menutupi komponen wajib yang gagal.

| Bonus | Poin |
| --- | --- |
| Pencarian menu | +2 |
| Filter kategori | +2 |
| Cetak struk (`window.print`) | +2 |
| Riwayat transaksi | +2 |
| Format ribuan `toLocaleString` | +1 |
| Layout responsif dua kolom | +1 |

---

## 5. Nilai Akhir

Rumus:

```text
Nilai akhir = (jumlah nilai Task 01–29 + 2 × nilai Task 30) / 31
```

Contoh:

- Rata-rata Task 01–29 = 82
- Nilai Task 30 = 90
- Nilai akhir = `(29 × 82 + 2 × 90) / 31 = (2378 + 180) / 31 = 82,5`

### Konversi Predikat

| Rentang | Predikat | Keterangan |
| --- | --- | --- |
| 85–100 | A | Menguasai materi dengan sangat baik |
| 75–84 | B | Menguasai materi dengan baik |
| 65–74 | C | Cukup, perlu penguatan di beberapa topik |
| 55–64 | D | Perlu remedial |
| < 55 | E | Belum mencapai kompetensi minimum |

Sekolah atau lembaga dapat menyesuaikan rentang selama dikomunikasikan di awal kelas.

---

## 6. Form Penilaian

| No | Task | Output (50) | Konsep (20) | Batas (15) | Rapi (10) | Dok (5) | Total |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 01 | Variabel & tipe data | | | | | | |
| 02 | Operator & template literal | | | | | | |
| 03 | Percabangan if/else | | | | | | |
| 04 | Switch & voucher | | | | | | |
| 05 | Perulangan for | | | | | | |
| 06 | While & nested loop | | | | | | |
| 07 | Fungsi & return | | | | | | |
| 08 | Parameter default & scope | | | | | | |
| 09 | Array dasar | | | | | | |
| 10 | Method array | | | | | | |
| 11 | Objek dasar | | | | | | |
| 12 | map & filter | | | | | | |
| 13 | reduce & sort | | | | | | |
| 14 | Destructuring & spread | | | | | | |
| 15 | Nested object & array | | | | | | |
| 16 | Object method & this | | | | | | |
| 17 | JSON | | | | | | |
| 18 | Set & Map | | | | | | |
| 19 | String methods | | | | | | |
| 20 | Format struk | | | | | | |
| 21 | Date & waktu | | | | | | |
| 22 | Error handling | | | | | | |
| 23 | Regex dasar | | | | | | |
| 24 | DOM render menu | | | | | | |
| 25 | DOM form | | | | | | |
| 26 | DOM keranjang & total | | | | | | |
| 27 | localStorage | | | | | | |
| 28 | Callback & Promise | | | | | | |
| 29 | async/await & fetch | | | | | | |
| 30 | Capstone (×2) | | | | | | |

---

## 7. Panduan Umpan Balik

Saat memberikan nilai, sertakan:

1. **Satu hal yang sudah baik.**
2. **Satu hal utama yang perlu diperbaiki.**
3. **Satu langkah konkret untuk memperbaikinya.**

Contoh:

> “Struk dan perhitungan pajak sudah tepat. Namun qty masih bisa menjadi 0 saat tombol `−` ditekan. Tambahkan pengecekan `if (qty > 1)` sebelum mengurangi, lalu uji kasus qty 1.”

> “Fungsi `map` dan `filter` sudah dipakai dengan benar. Kasus array kosong belum ditangani sehingga `cariMenuTermahal` error. Tambahkan pengecekan `if (daftar.length === 0) return null`.”

---

## 8. Integritas Penilaian

- Nilai perilaku yang benar, bukan panjang kode.
- Jangan memberi nilai penuh jika siswa tidak bisa menjelaskan kodenya.
- Bonus tidak boleh menutupi fitur wajib yang belum berfungsi.
- Simpan bukti pekerjaan (file atau commit) untuk audit.
- Gunakan rubrik yang sama untuk semua siswa pada kelas yang sama.
