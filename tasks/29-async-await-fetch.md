# Task 29 — async/await & fetch: Muat Menu dari API

> **Level:** Lanjutan · **Estimasi:** 90 menit · **Topik:** `async`, `await`, `fetch`, `response.ok`, `response.json()`, `try/catch`

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Mengambil data dari server menggunakan `fetch`.
2. Menunggu hasil request dengan `async/await`.
3. Memeriksa status response dan menangani kegagalan.
4. Merender data dari server ke halaman.

## Studi Kasus

Menu Kopi Senja sekarang disimpan di file terpisah `menu.json` agar bisa diperbarui tanpa mengubah kode JavaScript. Halaman kasir harus mengambil data tersebut saat dibuka, menampilkan pesan loading, lalu merender menu. Jika pengambilan data gagal, halaman harus menampilkan pesan error, bukan layar kosong.

## File yang Dibuat

```text
task-29.html
task-29.js
menu.json
```

### `menu.json`

```json
[
  { "nama": "Espresso", "harga": 18000 },
  { "nama": "Latte", "harga": 24000 },
  { "nama": "Kopi Susu", "harga": 22000 },
  { "nama": "Croissant", "harga": 25000 }
]
```

### Struktur HTML wajib

```html
<h1>Menu Kopi Senja</h1>
<p id="loading">Memuat menu...</p>
<p id="status" hidden></p>
<p id="pesan-error" hidden></p>
<div id="daftar-menu"></div>
<script src="task-29.js"></script>
```

## Cara Menjalankan

`fetch` tidak bisa membaca file lokal jika halaman dibuka dengan `file://`. Jalankan server statis dari folder tugas:

```bash
npx serve .
```

Atau, jika Python tersedia:

```bash
python -m http.server 8000
```

Lalu buka alamat yang muncul (misalnya `http://localhost:3000` atau `http://localhost:8000`).

## Yang Harus Dibuat

File **`task-29.js`** harus:

1. Fungsi `muatMenu()` bertipe `async`:
   - memanggil `fetch("menu.json")`,
   - memeriksa `response.ok`; jika `false`, lempar `Error("Gagal memuat menu")`,
   - mengembalikan hasil `response.json()`.
2. Fungsi `tampilkanMenu(menu)`:
   - menghapus isi `#daftar-menu` terlebih dahulu,
   - membuat kartu untuk setiap menu dengan nama dan `Rp` + harga,
   - memakai `createElement` dan `textContent`.
3. Fungsi `muatMenuAman()`:
   - memanggil `muatMenu()` di dalam `try`,
   - menyembunyikan `#pesan-error`, menampilkan `#status` berisi `Berhasil memuat N menu.` jika sukses,
   - menampilkan `#pesan-error` berisi `Gagal memuat menu. Coba lagi.` dan mengosongkan `#status` jika gagal,
   - memakai `finally` untuk menyembunyikan `#loading`.
4. Panggil `muatMenuAman()` saat halaman dimuat.

## Ketentuan

- Gunakan `async/await`, bukan `.then()`.
- Wajib memeriksa `response.ok`; `fetch` tidak otomatis melempar error untuk status 404.
- Jangan menulis data menu di JavaScript; data harus berasal dari `menu.json`.
- Gunakan `textContent`, bukan `innerHTML`.
- Pesan error tidak boleh menampilkan objek error mentah ke pengguna.

## Ekspektasi Perilaku

### Saat berhasil

Teks status berubah menjadi `Berhasil memuat 4 menu.` dan halaman menampilkan:

```text
Menu Kopi Senja

Berhasil memuat 4 menu.

┌──────────────────────────┐
│ Espresso                 │
│ Rp18000                  │
└──────────────────────────┘
┌──────────────────────────┐
│ Latte                    │
│ Rp24000                  │
└──────────────────────────┘
┌──────────────────────────┐
│ Kopi Susu                │
│ Rp22000                  │
└──────────────────────────┘
┌──────────────────────────┐
│ Croissant                │
│ Rp25000                  │
└──────────────────────────┘
```

### Saat gagal

Ubah sementara nama file menjadi `menu-salah.json`, lalu refresh. Halaman harus menampilkan:

```text
Menu Kopi Senja

Gagal memuat menu. Coba lagi.
```

Tidak boleh ada kartu setengah jadi dan tidak boleh ada error merah di console.

## Contoh Kasus Uji

| Skenario | Hasil |
| --- | --- |
| `menu.json` berisi 4 item | 4 kartu tampil, status sukses |
| `menu.json` berisi array kosong | Status sukses, tidak ada kartu, tampilkan `Menu sedang kosong` (bonus) |
| Nama file salah / 404 | Pesan error tampil, loading hilang |
| Server dimatikan | Pesan error tampil, loading hilang |
| `menu.json` bukan JSON valid | Masuk `catch`, pesan error tampil |

## Checklist Sebelum Kumpul

- [ ] Halaman dijalankan melalui server lokal, bukan `file://`.
- [ ] `fetch("menu.json")` dipakai.
- [ ] `response.ok` diperiksa.
- [ ] `async/await` dipakai.
- [ ] `try/catch/finally` bekerja.
- [ ] Data dirender dari JSON, bukan hardcode.
- [ ] Tidak ada `innerHTML`.
- [ ] Pesan loading hilang setelah selesai, baik sukses maupun gagal.

## Bonus

1. Tampilkan pesan `Menu sedang kosong` jika array kosong.
2. Tambahkan tombol `Muat Ulang` yang memanggil `muatMenuAman()` lagi.
3. Tambahkan input pencarian yang menyaring menu yang sudah dimuat tanpa request ulang.
