# Task I14 — Node.js File I/O & CLI

> **Level:** Intermediate · **Estimasi:** 100 menit · **Topik:** `node:fs/promises`, `node:path`, `node:util parseArgs`, CSV, exit code

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Membaca dan menulis file secara asynchronous.
2. Mem-parsing argument CLI dengan `parseArgs`.
3. Menghasilkan laporan CSV yang valid.

## Studi Kasus

Stok Kopi Senja disimpan di `data/menu.json`. Setiap malam, kasir perlu membuat laporan nilai stok dalam format CSV untuk dikirim ke pemilik. Proses harus bisa dijalankan dari terminal dengan menentukan file input dan output.

## File yang Dibuat

```text
i14-cli/
├── inventory.js
└── data/
    └── menu.json
```

### `data/menu.json`

```json
[
  { "nama": "Espresso", "kategori": "Minuman", "harga": 18000, "stok": 10 },
  { "nama": "Latte", "kategori": "Minuman", "harga": 24000, "stok": 8 },
  { "nama": "Kopi Susu", "kategori": "Minuman", "harga": 22000, "stok": 12 },
  { "nama": "Croissant", "kategori": "Makanan", "harga": 25000, "stok": 6 },
  { "nama": "Roti Bakar", "kategori": "Makanan", "harga": 20000, "stok": 9 }
]
```

## Perintah

```bash
node inventory.js --file data/menu.json --format csv --out laporan.csv
```

| Opsi | Wajib | Default | Keterangan |
| --- | --- | --- | --- |
| `--file` | ya | — | path file JSON input |
| `--format` | tidak | `csv` | `csv` atau `json` |
| `--out` | tidak | `laporan.csv` | path file output |

## Yang Harus Dibuat

File **`inventory.js`** harus:

1. Mem-parsing argument memakai `parseArgs` dari `node:util`.
2. Membaca file JSON dengan `readFile` dari `node:fs/promises`.
3. Memvalidasi bahwa isinya array dan setiap item memiliki `nama`, `harga`, `stok`.
4. Menghitung `nilai = harga * stok` untuk setiap item.
5. Menulis CSV dengan header:

```csv
nama,kategori,harga,stok,nilai
```

6. Menulis file output memakai `writeFile`.
7. Mencetak ringkasan ke stdout:

```text
Membaca 5 item...
Laporan ditulis: laporan.csv
Total nilai stok: Rp966000
```

8. Jika file tidak ada atau JSON rusak, cetak error ke stderr dan `process.exitCode = 1`.

## Aturan CSV

- Field yang mengandung koma, kutip, atau baris baru harus dibungkus tanda kutip ganda.
- Tanda kutip di dalam field di-escape menjadi `""`.
- Baris diakhiri `\n`.
- Urutan kolom harus sama dengan header.

## Ekspektasi File CSV

```csv
nama,kategori,harga,stok,nilai
Espresso,Minuman,18000,10,180000
Latte,Minuman,24000,8,192000
Kopi Susu,Minuman,22000,12,264000
Croissant,Makanan,25000,6,150000
Roti Bakar,Makanan,20000,9,180000
```

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| File valid | CSV dan ringkasan benar |
| `--format json` | file JSON rapi, bukan CSV |
| File tidak ditemukan | pesan error, exit code `1` |
| JSON rusak | pesan error, tidak membuat file output |
| Item tanpa `stok` | validasi gagal |
| Nama berisi koma | di-escape dengan benar |

## Ketentuan

- Gunakan `fs/promises`, bukan `readFileSync`/`writeFileSync`.
- Gunakan `node:path` untuk menggabungkan path.
- Jangan menulis path absolut di kode.
- Argumen wajib divalidasi; `--file` tidak boleh kosong.
- Jangan memakai library CSV eksternal.
- Jangan menelan error tanpa pesan.

## Checklist Sebelum Kumpul

- [ ] `parseArgs` dipakai.
- [ ] File dibaca dan ditulis secara async.
- [ ] Validasi data berjalan.
- [ ] CSV memiliki header dan escape yang benar.
- [ ] Exit code `1` untuk kegagalan.
- [ ] Output stdout sama persis dengan contoh.

## Bonus

1. Tambahkan `--help` yang menampilkan cara pakai.
2. Tambahkan opsi `--sort nama|nilai` untuk mengurutkan laporan.
3. Tulis file secara atomik: tulis ke file sementara, lalu `rename`.
