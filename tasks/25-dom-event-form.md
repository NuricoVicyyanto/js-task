# Task 25 — DOM Event: Form Tambah Menu

> **Level:** Lanjutan · **Estimasi:** 75 menit · **Topik:** `addEventListener`, `submit`, `preventDefault`, `value`, `reset`, validasi form

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menangani event `submit` pada form.
2. Mencegah perilaku bawaan browser dengan `preventDefault()`.
3. Mengambil nilai input dan menampilkannya ke halaman.
4. Mengosongkan form setelah data ditambahkan.

## Studi Kasus

Pemilik Kopi Senja ingin menambah menu baru tanpa mengedit kode. Ia membutuhkan form sederhana: isi nama menu dan harga, klik **Tambah**, lalu menu baru langsung muncul di daftar.

## File yang Dibuat

```text
task-25.html
task-25.js
```

### Struktur HTML wajib

```html
<h1>Kelola Menu Kopi Senja</h1>

<form id="form-menu">
  <input id="input-nama" type="text" placeholder="Nama menu" />
  <input id="input-harga" type="number" placeholder="Harga" />
  <button type="submit">Tambah</button>
</form>

<p id="pesan-error"></p>
<div id="daftar-menu"></div>
```

Jangan mengubah `id` elemen.

## Yang Harus Dibuat

File **`task-25.js`** harus:

1. Mengambil form, kedua input, dan `#daftar-menu`.
2. Menambahkan listener pada event `submit`.
3. Memanggil `event.preventDefault()` agar halaman tidak reload.
4. Membaca `nama` dan `harga` dari input.
5. Memvalidasi: nama tidak boleh kosong dan harga harus lebih dari `0`.
6. Jika tidak valid, tampilkan pesan di `#pesan-error` dan **jangan** tambah menu.
7. Jika valid, buat kartu menu baru dan tambahkan ke `#daftar-menu`.
8. Kosongkan form dan kembalikan fokus ke input nama.
9. Hapus pesan error setelah berhasil.

## Ketentuan

- Harga dari input bertipe **string**; ubah ke angka dengan `Number()` sebelum dihitung.
- Gunakan `textContent`, bukan `innerHTML`.
- Gunakan `form.reset()` untuk mengosongkan form.
- Gunakan `inputNama.focus()` setelah berhasil.
- Jangan menyimpan data ke `localStorage` pada task ini.

## Ekspektasi Perilaku

| Langkah | Hasil yang diharapkan |
| --- | --- |
| Halaman dibuka | Daftar kosong, tidak ada error |
| Nama kosong + harga `18000`, klik Tambah | Pesan `Nama menu wajib diisi`, daftar tetap kosong |
| Nama `"Matcha"` + harga `0` | Pesan `Harga harus lebih dari 0`, daftar tetap kosong |
| Nama `"Matcha"` + harga `26000` | Kartu `Matcha — Rp26000` muncul |
| Setelah berhasil | Input kosong, fokus di input nama, pesan error hilang |
| Klik Tambah lagi dengan data baru | Menu kedua muncul, menu pertama tetap ada |

### Tampilan setelah dua menu ditambahkan

```text
Kelola Menu Kopi Senja

[Nama menu........] [Harga....] [Tambah]

┌──────────────────────────┐
│ Matcha                   │
│ Rp26000                  │
└──────────────────────────┘
┌──────────────────────────┐
│ Croissant                │
│ Rp25000                  │
└──────────────────────────┘
```

## Cara Memeriksa

1. Buka `task-25.html` di browser.
2. Coba semua langkah pada tabel di atas.
3. Pastikan halaman **tidak reload** saat tombol Tambah diklik.
4. Buka DevTools → Console, pastikan tidak ada error.

## Checklist Sebelum Kumpul

- [ ] `preventDefault()` dipanggil di handler submit.
- [ ] Nama kosong ditolak.
- [ ] Harga `0` atau negatif ditolak.
- [ ] Harga dikonversi menjadi angka.
- [ ] Menu baru muncul tanpa reload.
- [ ] Form kembali kosong dan fokus berpindah ke input nama.
- [ ] Tidak ada `innerHTML`.

## Bonus

1. Tampilkan pesan error di dekat input yang bermasalah, bukan di satu tempat.
2. Nonaktifkan tombol Tambah selama form kosong.
3. Tambahkan tombol `Batal` yang mengosongkan form dan pesan error.
