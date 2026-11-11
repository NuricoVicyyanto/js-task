# Task I15 — Mini Project: CLI Inventory Manager

> **Level:** Intermediate · **Estimasi:** 3–4 jam · **Topik:** CLI, repository, service, validasi, persistensi JSON, arsitektur sederhana

## Tujuan

Menggabungkan modul, file I/O, array of objects, validasi, dan testing menjadi satu aplikasi CLI untuk mengelola stok Kopi Senja. Ini adalah **proyek akhir level intermediate**.

## Studi Kasus

Pemilik Kopi Senja mencatat stok di buku dan sering telat mengetahui menu yang hampir habis. Ia membutuhkan satu perintah terminal untuk melihat, menambah, menghapus, dan memeriksa stok rendah, dengan data yang tetap tersimpan setelah program ditutup.

## Deliverable

```text
i15-inventory-cli/
├── cli.js
├── lib/
│   ├── repository.js
│   ├── service.js
│   └── format.js
├── data/
│   └── menu.json
└── README.md
```

`README.md` milikmu menjelaskan cara menjalankan, daftar perintah, dan contoh output.

## Data Awal

Gunakan 5 menu dari Task I14. Setiap item memiliki `id`, `nama`, `kategori`, `harga`, dan `stok`.

```json
[
  { "id": 1, "nama": "Espresso", "kategori": "Minuman", "harga": 18000, "stok": 10 },
  { "id": 2, "nama": "Latte", "kategori": "Minuman", "harga": 24000, "stok": 8 },
  { "id": 3, "nama": "Kopi Susu", "kategori": "Minuman", "harga": 22000, "stok": 12 },
  { "id": 4, "nama": "Croissant", "kategori": "Makanan", "harga": 25000, "stok": 6 },
  { "id": 5, "nama": "Roti Bakar", "kategori": "Makanan", "harga": 20000, "stok": 9 }
]
```

## Perintah Wajib

### `list`

```bash
node cli.js list
```

Output:

```text
1. Espresso | Minuman | Rp18000 | stok 10
2. Latte | Minuman | Rp24000 | stok 8
3. Kopi Susu | Minuman | Rp22000 | stok 12
4. Croissant | Makanan | Rp25000 | stok 6
5. Roti Bakar | Makanan | Rp20000 | stok 9
```

Dukung filter:

```bash
node cli.js list --kategori Minuman
```

### `add`

```bash
node cli.js add "Matcha" Minuman 26000 12
```

- `id` otomatis menjadi `6`.
- Output: `Ditambahkan: #6 Matcha`
- Data langsung tersimpan ke JSON.

### `remove`

```bash
node cli.js remove 2
```

- Output: `Dihapus: #2 Latte`
- Jika id tidak ada: `Menu #2 tidak ditemukan`, exit code `1`.

### `low-stock`

```bash
node cli.js low-stock --threshold 7
```

- Menampilkan item dengan `stok < threshold`.
- Output: `Stok rendah (<7): Croissant (6)`
- Jika tidak ada: `Tidak ada stok rendah.`

## Tanggung Jawab Layer

| Layer | File | Tugas |
| --- | --- | --- |
| Repository | `lib/repository.js` | baca/tulis JSON, atomic write, buat id berikutnya |
| Service | `lib/service.js` | validasi, aturan bisnis, filter, low-stock |
| Format | `lib/format.js` | format rupiah dan baris output |
| CLI | `cli.js` | parsing argumen, memanggil service, menangani error |

## Validasi

| Aturan | Pesan error |
| --- | --- |
| Nama kosong | `Nama menu wajib diisi` |
| Kategori bukan Minuman/Makanan | `Kategori harus Minuman atau Makanan` |
| Harga ≤ 0 | `Harga harus lebih dari 0` |
| Stok < 0 | `Stok tidak boleh negatif` |
| Threshold ≤ 0 | `Threshold harus lebih dari 0` |
| ID tidak ditemukan | `Menu #<id> tidak ditemukan` |

Error ditulis ke stderr dan `process.exitCode = 1`; data tidak boleh berubah jika validasi gagal.

## Ekspektasi & Skenario Penerimaan

| No | Perintah | Hasil |
| --- | --- | --- |
| 1 | `list` | 5 baris sesuai data |
| 2 | `list --kategori Makanan` | hanya Croissant dan Roti Bakar |
| 3 | `add "Matcha" Minuman 26000 12` | id `6`, data tersimpan |
| 4 | `add "" Minuman 10000 1` | error nama, data tetap 6 |
| 5 | `remove 2` | Latte hilang, data tersimpan |
| 6 | `remove 99` | error, exit code `1` |
| 7 | `low-stock --threshold 7` | Croissant (6) |
| 8 | `low-stock --threshold 10` | Croissant (6) dan Roti Bakar (9) |
| 9 | Jalankan `list` lagi | perubahan tetap ada |

## Ketentuan

- Jangan menaruh semua logika di `cli.js`.
- Repository tidak boleh memformat teks untuk pengguna.
- Service tidak boleh memanggil `process.exit`.
- CLI tidak boleh mengakses file JSON secara langsung.
- Gunakan `fs/promises` dan tulis file secara atomik (temp + `rename`).
- Gunakan `node:util parseArgs` untuk opsi.
- Jangan memakai dependency eksternal.
- ID baru = `Math.max(...id) + 1`, bukan `length + 1`.

## Checklist Sebelum Kumpul

- [ ] Empat perintah wajib berjalan.
- [ ] Filter kategori bekerja.
- [ ] ID unik dan tidak bentrok setelah penghapusan.
- [ ] Validasi menolak input salah tanpa mengubah data.
- [ ] Data tersimpan setelah setiap perubahan.
- [ ] Layer repository/service/cli terpisah.
- [ ] README proyek lengkap.

## Bonus

1. Tambahkan perintah `update <id> --harga 20000 --stok 5`.
2. Tambahkan `export --format csv`.
3. Tulis unit test untuk service memakai repository palsu.
