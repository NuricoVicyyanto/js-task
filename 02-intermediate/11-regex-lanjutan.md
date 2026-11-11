# Task I11 — Regex Lanjutan

> **Level:** Intermediate · **Estimasi:** 75 menit · **Topik:** named capture group, replace callback, anchor, parsing teks

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menggunakan named capture group untuk mem-parsing teks.
2. Menggunakan `replace` dengan callback.
3. Menulis regex yang aman untuk format yang ketat.

## Studi Kasus

Kopi Senja menerima struk dalam bentuk teks dari mesin kasir lama. Tim perlu mengubah teks tersebut menjadi data terstruktur, menyamarkan nomor telepon pelanggan, dan menandai kata kunci pada catatan pesanan.

## Yang Harus Dibuat

Buat file **`task-i11.js`** dengan fungsi:

### 1. `parseBarisStruk(baris)`

Format: `"<nama> x<qty> Rp<total>"`.

- Gunakan named group: `nama`, `qty`, `total`.
- Kembalikan `{ nama, qty: Number, total: Number }`.
- Jika format tidak cocok, kembalikan `null`.

Contoh: `"Espresso x2 Rp36000"` → `{ nama: "Espresso", qty: 2, total: 36000 }`.

### 2. `parseVoucher(kode)`

Format: `"<KODE>-<persen>-<tahun>"`, contoh `"SENJA-10-2026"`.

- Kembalikan `{ kode: "SENJA", persen: 10, tahun: 2026 }`.
- Jika tidak cocok, `null`.

### 3. `sensorTelepon(nomor)`

- Hanya untuk nomor 12 digit yang dimulai `08`.
- Ganti 4 digit di tengah dengan `****`.
- `"081234567890"` → `"0812****7890"`.
- Jika format tidak sesuai, kembalikan `"Nomor tidak valid"`.

### 4. `highlightKata(teks, kata)`

- Ganti semua kemunculan `kata` (case-insensitive) menjadi `**<kata asli>**`.
- `"kopi susu, KOPI senja"` + `"kopi"` → `"**kopi** susu, **KOPI** senja"`.
- Jika `kata` kosong, kembalikan teks asli.

## Ekspektasi Output

```text
{ nama: 'Espresso', qty: 2, total: 36000 }
Kode: SENJA, Persen: 10, Tahun: 2026
Telepon: 0812****7890
Highlight: **kopi** susu, **KOPI** senja
Baris tidak valid: null
```

## Ketentuan

- Wajib memakai **named capture group** `(?<nama>...)`.
- `parseBarisStruk` tidak boleh memakai `split()` untuk memisahkan field.
- `highlightKata` wajib memakai `replace` dengan callback agar huruf asli dipertahankan.
- Regex harus memakai anchor `^` dan `$` untuk format baris.
- Escape input pengguna sebelum membangun regex dinamis.
- Jangan memakai `eval`.

## Kasus Uji

| Input | Hasil |
| --- | --- |
| `"Latte x1 Rp24000"` | objek dengan qty `1` |
| `"Latte 1 Rp24000"` | `null` |
| `"Latte x0 Rp0"` | qty `0`, total `0` |
| `"SENJA-20-2027"` | persen `20`, tahun `2027` |
| `"senja-20-2027"` | `null` |
| `"0812345678"` | `"Nomor tidak valid"` |
| `"0812-3456-7890"` | `"Nomor tidak valid"` |
| Kata berisi karakter regex `"."` | diperlakukan sebagai teks biasa |

## Checklist Sebelum Kumpul

- [ ] Named group dipakai minimal di dua fungsi.
- [ ] Anchor `^` dan `$` mencegah parsing sebagian.
- [ ] `replace` callback mempertahankan huruf asli.
- [ ] Input regex dinamis di-escape.
- [ ] Format tidak valid mengembalikan `null`, bukan error.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Buat `parseStruk(teks)` yang mem-parsing banyak baris menjadi array.
2. Validasi slug `^[a-z0-9]+(?:-[a-z0-9]+)*$`.
3. Buat parser jam `"14:30"` yang menolak `"25:99"` tanpa `Date`.
