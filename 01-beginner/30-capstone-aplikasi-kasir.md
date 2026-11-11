# Task 30 — Capstone: Aplikasi Kasir Kopi Senja

> **Level:** Lanjutan · **Estimasi:** 4–6 jam · **Topik:** gabungan DOM, event, array of objects, validasi, localStorage, struk

## Tujuan

Menggabungkan seluruh materi Task 01–29 menjadi satu aplikasi kasir yang bisa dipakai di browser. Task ini adalah **proyek akhir**, bukan latihan satu topik. Kamu bebas menentukan tampilan, tetapi semua perilaku di bawah wajib berjalan.

## Studi Kasus

Kopi Senja membutuhkan aplikasi kasir sederhana untuk satu perangkat. Kasir harus bisa:

- melihat daftar menu,
- menambahkan menu ke keranjang,
- mengubah jumlah,
- menghapus item,
- memakai kode voucher,
- melihat pajak dan total,
- menyelesaikan pembayaran dan mencetak struk,
- mempertahankan keranjang saat halaman di-refresh.

Aplikasi tidak membutuhkan login, database, atau pembayaran online.

## Deliverable

Buat folder proyek:

```text
task-30/
├── index.html
├── style.css
├── app.js
├── menu.json        (opsional, untuk nilai tambah)
└── README.md        (dokumentasi proyekmu)
```

`README.md` milikmu minimal berisi:

1. Cara menjalankan aplikasi.
2. Daftar fitur.
3. Kode voucher yang didukung.
4. Satu contoh perhitungan manual.
5. Kendala yang kamu temui dan cara menyelesaikannya.

## Data Menu

Gunakan minimal **6 menu** dengan kategori berbeda. Contoh:

| Menu | Kategori | Harga |
| --- | --- | --- |
| Espresso | Minuman | 18000 |
| Latte | Minuman | 24000 |
| Kopi Susu | Minuman | 22000 |
| Croissant | Makanan | 25000 |
| Roti Bakar | Makanan | 20000 |
| Matcha | Minuman | 26000 |

Data boleh ditulis di `app.js` atau dimuat dari `menu.json` menggunakan `fetch`.

## Yang Harus Dibuat (Fitur Wajib)

### 1. Daftar menu

- Semua menu tampil dalam bentuk kartu.
- Setiap kartu berisi nama, kategori, harga, dan tombol **Tambah**.
- Harga tampil dengan format `Rp18000` atau `Rp18.000` (pilih satu, konsisten).

### 2. Keranjang

- Menambahkan menu yang sama **dua kali** menambah jumlah (qty), bukan membuat baris duplikat.
- Setiap baris menampilkan nama, harga satuan, qty, subtotal baris, tombol `+`, `−`, dan `Hapus`.
- Qty minimal `1`. Tombol `−` pada qty `1` tidak boleh membuat qty `0`.
- Menghapus baris menghapus seluruh qty menu tersebut.
- Keranjang kosong menampilkan pesan `Keranjang masih kosong`.

### 3. Perhitungan

- `subtotal` = jumlah `harga × qty` semua item.
- Voucher:
  - `SENJA10` → diskon 10%, minimal belanja Rp50.000.
  - `SENJA20` → diskon 20%, minimal belanja Rp100.000.
  - Kode lain atau kosong → diskon Rp0.
- Diskon dihitung dari subtotal.
- Pajak **11%** dihitung dari `subtotal - diskon`.
- `total = subtotal - diskon + pajak`.
- Semua nilai dibulatkan ke rupiah terdekat.

### 4. Voucher

- Ada input kode voucher dan tombol **Terapkan**.
- Jika valid, tampilkan `Voucher SENJA10 diterapkan: diskon Rp6000`.
- Jika minimal belanja belum terpenuhi, tampilkan `Minimal belanja Rp50000 untuk voucher ini`.
- Jika kode tidak dikenal, tampilkan `Kode voucher tidak valid`.
- Diskon langsung dihitung ulang saat voucher berubah.

### 5. Pembayaran

- Tombol **Bayar** hanya aktif jika keranjang tidak kosong.
- Saat diklik, tampilkan struk (modal atau bagian halaman) dengan:
  - nama item dan qty,
  - subtotal,
  - diskon,
  - pajak,
  - total,
  - teks `Terima kasih!`.
- Setelah struk ditutup, keranjang dikosongkan dan `localStorage` dibersihkan.
- Tombol **Batal** menutup struk tanpa mengosongkan keranjang.

### 6. Penyimpanan

- Keranjang dan voucher disimpan di `localStorage` dengan key `kopi-senja-keranjang`.
- Saat halaman dimuat, data dipulihkan dan total dihitung ulang.
- Tombol **Kosongkan Keranjang** menghapus data dan mereset voucher.
- Data rusak di `localStorage` ditangani dengan `try/catch`.

### 7. Validasi & kualitas

- Tidak ada `innerHTML` untuk data pengguna; gunakan `textContent`.
- Tidak ada error di console saat alur normal.
- Tombol yang tidak relevan dinonaktifkan (misalnya Bayar saat kosong).
- Layout tetap terbaca di lebar layar 360 px.

## Ekspektasi Output

Nilai transaksi dan struk harus mengikuti contoh perhitungan berikut.

### Contoh Perhitungan Wajib

Gunakan contoh ini untuk memastikan rumusmu benar.

**Keranjang:**

| Item | Harga | Qty | Subtotal |
| --- | --- | --- | --- |
| Espresso | 18000 | 2 | 36000 |
| Latte | 24000 | 1 | 24000 |

- Subtotal: **Rp60.000**
- Voucher: `SENJA10` → diskon 10% = **Rp6.000**
- Setelah diskon: **Rp54.000**
- Pajak 11% = 54000 × 11 / 100 = **Rp5.940**
- Total: **Rp59.940**

### Contoh struk

```text
================================
        STRUK KOPI SENJA
================================
Espresso x2          Rp36000
Latte x1             Rp24000
--------------------------------
Subtotal             Rp60000
Diskon (10%)         -Rp6000
Pajak 11%            Rp5940
--------------------------------
TOTAL                Rp59940
================================
Terima kasih!
```

## Skenario Penerimaan

Gunakan skenario ini saat menguji aplikasimu sendiri.

| No | Langkah | Hasil yang diharapkan |
| --- | --- | --- |
| 1 | Buka aplikasi | Menu tampil, keranjang kosong, total `Rp0`, tombol Bayar nonaktif |
| 2 | Tambah Espresso 2× | Satu baris, qty `2`, subtotal baris `Rp36000` |
| 3 | Tambah Latte 1× | Dua baris, subtotal `Rp60000` |
| 4 | Terapkan `SENJA10` | Diskon `Rp6000`, total `Rp59940` |
| 5 | Terapkan `SENJA20` | Pesan minimal belanja Rp100000 |
| 6 | Terapkan `SENJA99` | Pesan kode tidak valid |
| 7 | Refresh halaman | Keranjang dan voucher tetap, total benar |
| 8 | Klik `+` pada Latte | Qty `2`, subtotal `Rp84000`, total dihitung ulang |
| 9 | Klik `−` sampai qty `1` | Qty tidak bisa kurang dari `1` |
| 10 | Hapus Espresso | Hanya Latte tersisa, total dihitung ulang |
| 11 | Klik Bayar | Struk tampil dengan angka yang benar |
| 12 | Tutup struk | Keranjang kosong, total `Rp0`, data localStorage terhapus |
| 13 | Kosongkan keranjang | Semua item hilang, voucher reset |
| 14 | Ubah localStorage menjadi teks rusak, refresh | Aplikasi tidak crash, mulai dari keranjang kosong |

## Rubrik Penilaian

| Komponen | Bobot | Indikator |
| --- | --- | --- |
| Fungsionalitas inti | 40 | Tambah, qty, hapus, subtotal, diskon, pajak, total benar |
| Alur pembayaran & struk | 20 | Struk akurat, reset setelah bayar, batal tidak mereset |
| Penyimpanan | 15 | localStorage, pemulihan, penanganan data rusak |
| Validasi & kasus batas | 10 | Qty minimal, voucher, keranjang kosong, tombol nonaktif |
| Kualitas kode | 10 | Fungsi terpisah, penamaan jelas, tidak ada duplikasi besar |
| UI & dokumentasi | 5 | Layout rapi, README lengkap dan jujur |

Nilai maksimal **100**. Bonus maksimal **+10**.

## Checklist Sebelum Kumpul

- [ ] Minimal 6 menu dengan 2 kategori.
- [ ] Menambah menu yang sama menaikkan qty, bukan menduplikasi baris.
- [ ] Qty tidak bisa di bawah 1.
- [ ] Hapus baris dan kosongkan keranjang bekerja.
- [ ] Voucher `SENJA10` dan `SENJA20` bekerja beserta minimal belanja.
- [ ] Pajak dihitung setelah diskon.
- [ ] Tombol Bayar nonaktif saat keranjang kosong.
- [ ] Struk menampilkan item, subtotal, diskon, pajak, total.
- [ ] Setelah bayar, keranjang dan localStorage bersih.
- [ ] Refresh mempertahankan keranjang.
- [ ] Data localStorage rusak tidak membuat aplikasi crash.
- [ ] Tidak ada `innerHTML` untuk data pengguna.
- [ ] README proyek lengkap.

## Bonus

1. Tambahkan pencarian menu berdasarkan nama.
2. Tambahkan filter kategori (Semua / Minuman / Makanan).
3. Tambahkan tombol cetak struk menggunakan `window.print()`.
4. Simpan riwayat transaksi terakhir (maksimal 5) dan tampilkan di halaman terpisah.
5. Tambahkan format harga dengan pemisah ribuan menggunakan `toLocaleString("id-ID")`.
6. Buat tampilan responsif dua kolom: menu di kiri, keranjang di kanan.
