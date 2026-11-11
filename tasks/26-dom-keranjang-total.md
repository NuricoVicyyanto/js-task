# Task 26 — DOM: Keranjang, Total, dan Hapus Item

> **Level:** Lanjutan · **Estimasi:** 90 menit · **Topik:** event delegation, `dataset`, `remove()`, perhitungan total, empty state

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menampilkan daftar item yang bisa dihapus satu per satu.
2. Menyimpan data tambahan pada elemen dengan `data-*`.
3. Menghitung ulang total setiap kali data berubah.
4. Menampilkan empty state saat keranjang kosong.

## Studi Kasus

Kopi Senja membutuhkan keranjang pesanan sederhana. Kasir menambahkan item, melihat total belanja, dan menghapus item jika pelanggan berubah pikiran. Total harus selalu akurat dan tidak boleh dihitung manual.

## File yang Dibuat

```text
task-26.html
task-26.js
```

### Struktur HTML wajib

```html
<h1>Keranjang Kopi Senja</h1>

<form id="form-item">
  <input id="input-nama" type="text" placeholder="Nama item" />
  <input id="input-harga" type="number" placeholder="Harga" />
  <button type="submit">Tambah</button>
</form>

<p id="pesan-kosong">Keranjang masih kosong.</p>
<ul id="daftar-item"></ul>

<p>Total: <strong id="total-harga">Rp0</strong></p>
```

Jangan mengubah `id` elemen.

## Yang Harus Dibuat

File **`task-26.js`** harus:

1. Menangani submit form seperti Task 25 (validasi + tambah item).
2. Setiap item dirender sebagai `<li>` berisi:
   - nama item,
   - harga dalam format `Rp18000`,
   - tombol `Hapus`.
3. Setiap `<li>` menyimpan harga pada `data-harga`.
4. Saat tombol Hapus diklik, item tersebut dihapus dari DOM.
5. Total dihitung ulang dari semua `data-harga` yang masih ada.
6. `#pesan-kosong` hanya tampil saat tidak ada item.
7. Total menampilkan `Rp0` saat keranjang kosong.

## Ketentuan

- Gunakan `dataset.harga` untuk membaca harga item.
- Gunakan `Number()` saat mengubah `data-harga` menjadi angka.
- Gunakan `element.remove()` untuk menghapus item.
- Jangan menyimpan total di variabel yang hanya ditambah; hitung ulang dari DOM agar selalu konsisten.
- Gunakan `textContent`, bukan `innerHTML`.
- Form tetap harus mencegah reload.

## Ekspektasi Perilaku

| Langkah | Total | Empty state |
| --- | --- | --- |
| Halaman dibuka | `Rp0` | Tampil |
| Tambah Espresso Rp18000 | `Rp18000` | Hilang |
| Tambah Latte Rp24000 | `Rp42000` | Hilang |
| Hapus Espresso | `Rp24000` | Hilang |
| Hapus Latte | `Rp0` | Tampil |
| Hapus saat kosong | Tetap `Rp0` | Tetap tampil |

### Tampilan saat dua item ada

```text
Keranjang Kopi Senja

[Nama item........] [Harga....] [Tambah]

• Espresso — Rp18000        [Hapus]
• Latte — Rp24000           [Hapus]

Total: Rp42000
```

### Tampilan saat kosong

```text
Keranjang masih kosong.

Total: Rp0
```

## Cara Memeriksa

1. Buka `task-26.html`.
2. Ikuti tabel perilaku dari atas ke bawah.
3. Hapus item tengah, lalu pastikan total dan urutan tetap benar.
4. Refresh halaman: data boleh hilang (penyimpanan permanen ada di Task 27).

## Checklist Sebelum Kumpul

- [ ] Setiap item memiliki tombol Hapus.
- [ ] Harga tersimpan di `data-harga`.
- [ ] Total dihitung ulang dari item yang tersisa.
- [ ] Empty state muncul/hilang dengan benar.
- [ ] Tidak ada item ganda saat tombol diklik berkali-kali.
- [ ] Tidak ada `innerHTML`.

## Bonus

1. Tambahkan tombol `Kosongkan Keranjang` yang menghapus semua item sekaligus.
2. Tambahkan jumlah (qty) per item dan kalikan dengan harga.
3. Tampilkan jumlah item di samping total: `Total (2 item): Rp42000`.
