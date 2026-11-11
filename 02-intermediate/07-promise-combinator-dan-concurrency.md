# Task I07 — Promise Combinator & Concurrency

> **Level:** Intermediate · **Estimasi:** 90 menit · **Topik:** `Promise.allSettled`, concurrency pool, timeout, error isolation

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menjalankan banyak Promise dengan batas konkurensi.
2. Menjaga urutan hasil sesuai urutan input.
3. Mengisolasi kegagalan satu tugas agar tidak menggagalkan semuanya.

## Studi Kasus

Kopi Senja meminta harga ke lima supplier secara paralel. Terlalu banyak request sekaligus membuat koneksi penuh, tetapi berurutan terlalu lambat. Kasir membutuhkan **concurrency pool**: maksimal dua request aktif pada satu waktu, hasil tetap berurutan, dan satu supplier yang gagal tidak membatalkan supplier lain.

## Yang Harus Dibuat

Buat file **`task-i07.js`** dengan:

### `tidur(ms)`

Promise yang selesai setelah `ms` milidetik.

### `pool(tugas, batas)`

- `tugas` adalah array fungsi `() => Promise`.
- Jalankan maksimal `batas` tugas secara bersamaan.
- Kembalikan array hasil dengan bentuk `{ status: "fulfilled", value }` atau `{ status: "rejected", reason }`, **sesuai urutan input**.
- Jika satu tugas gagal, tugas lain tetap berjalan.
- Jika `tugas` kosong, kembalikan `[]`.
- Jika `batas < 1`, lempar `Error("Batas minimal 1")`.

### Data simulasi

```js
const supplier = [
  { nama: "supplier-a", delay: 30, gagal: false },
  { nama: "supplier-b", delay: 10, gagal: false },
  { nama: "supplier-c", delay: 20, gagal: false },
  { nama: "supplier-d", delay: 10, gagal: true },
  { nama: "supplier-e", delay: 5, gagal: false },
];
```

Buat fungsi tugas yang mencatat jumlah tugas aktif, memperbarui `maksAktif`, lalu resolve dengan nama supplier atau reject dengan `Error("<nama> gagal")`.

## Ekspektasi Output

```text
Maksimal aktif: 2
Selesai: supplier-a, supplier-b, supplier-c, supplier-e
Gagal: supplier-d (supplier-d gagal)
Sukses: 4, gagal: 1
```

## Ketentuan

- Wajib mengimplementasikan pool sendiri; tidak boleh memakai library.
- Gunakan `Promise.allSettled` untuk mengubah hasil akhir.
- Hasil harus mengikuti urutan input, bukan urutan selesai.
- Jumlah tugas aktif tidak boleh melebihi `batas`.
- Jangan memakai `Promise.all` untuk seluruh tugas.
- Setiap tugas harus dimulai paling banyak satu kali.

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| 5 tugas, batas 2 | maksimal aktif `2` |
| 5 tugas, batas 1 | berjalan berurutan |
| 5 tugas, batas 10 | semua berjalan, maksimal aktif `5` |
| Satu tugas reject | hasil lain tetap `fulfilled` |
| Array kosong | `[]` |
| Batas `0` | melempar error |

## Checklist Sebelum Kumpul

- [ ] Pool tidak pernah melebihi batas.
- [ ] Urutan hasil sama dengan urutan input.
- [ ] Kegagalan satu tugas tidak menghentikan tugas lain.
- [ ] Setiap tugas dijalankan tepat satu kali.
- [ ] `batas` tidak valid ditangani.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Tambahkan `denganTimeout(promise, ms)` memakai `Promise.race`.
2. Tambahkan opsi `hentikanSaatGagal` untuk berhenti memulai tugas baru setelah kegagalan.
3. Buat `pool` menerima `AbortSignal` untuk membatalkan tugas yang belum mulai.
