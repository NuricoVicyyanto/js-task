# Task E03 — Performance & Memory Profiling

> **Level:** Expert · **Estimasi:** 3 jam · **Topik:** benchmarking, Big-O, indexing, `performance.now`, memory usage, optimasi terukur

## Tujuan

Mengukur sebelum mengoptimalkan, menemukan bottleneck nyata, lalu membuktikan peningkatan performa dengan data—bukan opini.

## Studi Kasus

Kopi Senja memiliki 100.000 data menu historis. Pencarian menu dengan `find` memakan waktu lama saat kasir mengetik. Tim meminta index pencarian dan laporan `topN`, dengan bukti benchmark sebelum/sesudah.

## File yang Dibuat

```text
e03-performance/
├── benchmark.js
├── search.js
└── README.md
```

## Data

Buat 100.000 item deterministik:

```js
const data = Array.from({ length: 100000 }, (_, i) => ({
  id: i + 1,
  nama: `Menu-${String(i + 1).padStart(6, "0")}`,
  kategori: i % 2 === 0 ? "Minuman" : "Makanan",
  harga: 10000 + i,
  stok: i % 20,
}));
```

## Yang Harus Dibuat (Fungsi Wajib)

| Fungsi | Tugas |
| --- | --- |
| `buildIndex(data)` | membuat `Map` dari `nama` ke item |
| `searchNaive(data, nama)` | mencari dengan `.find()` |
| `searchIndexed(index, nama)` | mencari dengan `Map.get()` |
| `topN(data, n)` | `n` harga tertinggi tanpa mengubah data asli |
| `benchmark(fn, iterations)` | mengukur rata-rata waktu |

## Skenario Benchmark

- 1.000 query pencarian: 500 query yang ada, 500 query yang tidak ada.
- Bandingkan `searchNaive` dan `searchIndexed`.
- Ukur `topN(data, 5)`.
- Ukur memori dengan `process.memoryUsage().heapUsed` sebelum dan sesudah index.

## Ekspektasi Output

```text
Data: 100000
Naive: <ms> ms
Indexed: <ms> ms
Speedup: <x>x
Target (>=5x): true
Top 5: Menu-100000, Menu-099999, Menu-099998, Menu-099997, Menu-099996
Heap index: <MB> MB
```

Angka `<ms>` dan `<MB>` boleh berbeda. Yang wajib:

- `Target (>=5x): true`
- Hasil pencarian sama antara naive dan indexed.
- `Top 5` sesuai data (harga tertinggi; jika seri, urutan `id` stabil).
- Tidak ada memory leak saat benchmark diulang 3×.

## Ketentuan

- Ukur dengan `performance.now()`, bukan `Date.now()`.
- Lakukan warm-up minimal satu kali sebelum pengukuran.
- Jalankan setiap pengukuran minimal 3 kali dan ambil median/rata-rata.
- Jangan mengoptimalkan sebelum ada angka baseline.
- `buildIndex` tidak boleh mengubah array asli.
- `topN` tidak boleh mengubah urutan data asli.
- Jelaskan kompleksitas waktu di `README.md`.

## Analisis yang Harus Ditulis

Di `README.md` proyek, jawab:

1. Mengapa `find` O(n) dan `Map.get` rata-rata O(1)?
2. Berapa memori tambahan yang dipakai index?
3. Pada ukuran data berapa index mulai tidak sepadan dengan biaya memori?
4. Apa yang terjadi jika `nama` duplikat?

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| Query ada | item yang benar |
| Query tidak ada | `undefined`/`null` konsisten |
| Nama duplikat | index menyimpan strategi yang jelas (pertama/terakhir) |
| `topN(data, 0)` | `[]` |
| `topN(data, 5)` | 5 item, urutan benar |
| Data asli setelah `topN` | tidak berubah |

## Checklist Sebelum Kumpul

- [ ] Baseline diukur sebelum optimasi.
- [ ] Speedup minimal 5× tercapai.
- [ ] Hasil naive dan indexed identik.
- [ ] Memori index diukur.
- [ ] Kompleksitas dijelaskan.
- [ ] Data asli tidak termutasi.
- [ ] Output sesuai format.

## Bonus

1. Buat index per kategori dan bandingkan performanya.
2. Tambahkan LRU cache untuk 100 query terakhir.
3. Streaming data 1 juta baris dengan generator agar memori tetap rendah.
