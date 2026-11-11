# Task I13 — DOM State Management

> **Level:** Intermediate · **Estimasi:** 120 menit · **Topik:** single source of truth, immutable state, render function, event delegation

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menyimpan seluruh data UI dalam satu objek state.
2. Mengubah state tanpa memutasi state lama.
3. Merender ulang UI dari state, bukan menambal DOM secara acak.

## Studi Kasus

Keranjang Kopi Senja di versi sebelumnya menghitung total dengan mengubah teks DOM langsung. Akibatnya, tampilan dan data sering tidak sinkron. Refaktor UI menjadi pola **state → render**, dengan satu sumber kebenaran untuk menu, keranjang, dan voucher.

## Yang Harus Dibuat (File)

```text
i13-state/
├── index.html
├── style.css
└── app.js
```

HTML minimal memiliki:

```html
<main id="app">
  <section id="menu"></section>
  <section id="keranjang"></section>
  <p id="ringkasan"></p>
</main>
```

## Bentuk State

```js
const state = {
  menu: [
    { id: 1, nama: "Espresso", harga: 18000 },
    { id: 2, nama: "Latte", harga: 24000 },
    { id: 3, nama: "Croissant", harga: 25000 },
  ],
  cart: [],
  voucher: "",
};
```

Setiap item cart: `{ id, nama, harga, qty }`.

## Fungsi yang Harus Dibuat

| Fungsi | Tugas |
| --- | --- |
| `tambahItem(state, id)` | menambah item; jika sudah ada, `qty + 1` |
| `ubahQty(state, id, delta)` | mengubah qty; qty minimal `1` |
| `hapusItem(state, id)` | menghapus baris dari cart |
| `setVoucher(state, kode)` | menyimpan kode voucher |
| `hitungRingkasan(state)` | mengembalikan `{ subtotal, diskon, pajak, total }` |
| `render(state)` | menggambar ulang menu, cart, dan ringkasan |

Aturan harga:

- Diskon `SENJA10` = 10% jika subtotal ≥ 50000, selain itu 0.
- Pajak 11% dari `subtotal - diskon`.
- Semua nilai dibulatkan dengan `Math.round`.

## Interaksi

Gunakan **event delegation** pada `#app`:

- Klik `[data-action="tambah"]` → `tambahItem`.
- Klik `[data-action="kurang"]` / `[data-action="tambah-qty"]` → `ubahQty`.
- Klik `[data-action="hapus"]` → `hapusItem`.
- Setelah aksi, panggil `render(state)`.
- Tidak boleh ada `addEventListener` per tombol item.
- Tidak boleh mengubah `textContent` di luar `render`.

## Ekspektasi Tampilan

Setelah menambah Espresso 2×, Latte 1×, dan voucher `SENJA10`:

```text
MENU
Espresso — Rp18000 [Tambah]
Latte — Rp24000 [Tambah]
Croissant — Rp25000 [Tambah]

KERANJANG
Espresso x2  Rp36000  [−] [+]
Latte x1     Rp24000  [−] [+]

Subtotal  Rp60000
Diskon    Rp6000
Pajak     Rp5940
Total     Rp59940
```

## Kasus Uji

| Aksi | Hasil |
| --- | --- |
| Tambah menu yang sama 2× | satu baris, qty `2` |
| Klik `−` saat qty `1` | tetap `1` |
| Hapus Latte | baris hilang, total dihitung ulang |
| Voucher `SENJA20` saat subtotal 60000 | diskon `0`, pesan minimal belanja |
| Voucher tidak dikenal | diskon `0`, pesan tidak valid |
| Keranjang kosong | pesan `Keranjang masih kosong` |

## Ketentuan

- Semua perubahan state menghasilkan objek state baru; jangan `state.cart.push(...)`.
- `render` boleh membaca state, tetapi tidak boleh mengubah state.
- `hitungRingkasan` tidak boleh membaca DOM.
- Jangan memakai `innerHTML` untuk data pengguna.
- Jangan menyimpan state di atribut DOM sebagai sumber utama.
- Qty tidak boleh `0` atau negatif.

## Checklist Sebelum Kumpul

- [ ] Hanya ada satu objek `state` sebagai sumber data.
- [ ] Semua aksi mengembalikan state baru.
- [ ] Render dipanggil setelah setiap aksi.
- [ ] Event delegation dipakai.
- [ ] Perhitungan total terpusat di `hitungRingkasan`.
- [ ] Qty minimal 1.
- [ ] Tampilan sesuai contoh.

## Bonus

1. Tambahkan riwayat undo/redo dengan array snapshot state.
2. Simpan state ke `localStorage` dan pulihkan saat halaman dibuka.
3. Pisahkan `renderMenu`, `renderCart`, dan `renderRingkasan` ke modul masing-masing.
