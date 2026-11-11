# Task I03 — Array Pipeline Lanjutan

> **Level:** Intermediate · **Estimasi:** 75 menit · **Topik:** `reduce`, `flatMap`, `some`, `every`, `find`, grouping, pipeline

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Mengubah array of objects menjadi struktur ringkasan.
2. Menggabungkan beberapa operasi array dalam satu pipeline.
3. Memilih method yang tepat untuk pertanyaan yang berbeda.

## Studi Kasus

Manajer Kopi Senja membutuhkan laporan cepat dari data menu dan pesanan:

- berapa menu per kategori,
- apakah semua menu punya harga,
- apakah ada menu yang habis,
- berapa total baris pesanan,
- menu termahal.

Semua jawaban harus dihitung dari data, bukan ditulis manual.

## Data Awal

```js
const menu = [
  { nama: "Espresso", kategori: "Minuman", harga: 18000, tersedia: true },
  { nama: "Latte", kategori: "Minuman", harga: 24000, tersedia: true },
  { nama: "Kopi Susu", kategori: "Minuman", harga: 22000, tersedia: false },
  { nama: "Croissant", kategori: "Makanan", harga: 25000, tersedia: true },
  { nama: "Roti Bakar", kategori: "Makanan", harga: 20000, tersedia: false },
];

const pesanan = [
  { id: "KS-001", items: [{ nama: "Espresso", qty: 2 }, { nama: "Latte", qty: 1 }] },
  { id: "KS-002", items: [{ nama: "Croissant", qty: 1 }, { nama: "Roti Bakar", qty: 2 }] },
];
```

## Yang Harus Dibuat

Buat file **`task-i03.js`** dengan fungsi:

| Fungsi | Tugas | Method wajib |
| --- | --- | --- |
| `kelompokkanKategori(menu)` | menghasilkan objek `{ Minuman: [...], Makanan: [...] }` | `reduce` |
| `semuaPunyaHarga(menu)` | `true` jika semua `harga > 0` | `every` |
| `adaYangHabis(menu)` | `true` jika ada `tersedia === false` | `some` |
| `rincianSemuaPesanan(pesanan)` | array semua item dari semua pesanan | `flatMap` |
| `menuTermahal(menu)` | objek menu dengan harga tertinggi | `reduce` |

## Ekspektasi Output

```text
Kategori: Minuman=3, Makanan=2
Semua punya harga: true
Ada yang habis: true
Total baris pesanan: 4
Termahal: Croissant
```

Gunakan `Object.entries` dan `.map()` untuk mencetak baris `Kategori`.

## Ketentuan

- Dilarang memakai `for`, `for...of`, atau `forEach` untuk lima fungsi utama.
- Jangan mengubah array `menu` atau `pesanan`.
- `menuTermahal` harus mengembalikan objek utuh, bukan hanya nama.
- `rincianSemuaPesanan` harus meratakan item, bukan mengembalikan array of arrays.
- `kelompokkanKategori` tidak boleh memakai key kategori yang ditulis manual.

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| Semua menu punya harga | `true` |
| Satu menu `harga: 0` | `false` |
| Semua menu tersedia | `adaYangHabis` → `false` |
| `pesanan` kosong | `rincianSemuaPesanan` → `[]` |
| Dua menu dengan harga tertinggi sama | Kembalikan salah satu secara konsisten |

## Checklist Sebelum Kumpul

- [ ] Lima fungsi memakai method yang diminta.
- [ ] Tidak ada loop manual pada fungsi utama.
- [ ] Data asli tidak berubah.
- [ ] `flatMap` menghasilkan array datar.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Buat `rekapNilaiKategori(menu)` yang menjumlahkan `harga` per kategori.
2. Buat `cariMenu(menu, kataKunci)` yang mencari nama secara case-insensitive.
3. Buat `topN(menu, n)` tanpa mengubah urutan array asli.
