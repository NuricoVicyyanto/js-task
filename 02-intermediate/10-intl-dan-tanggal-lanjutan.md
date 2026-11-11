# Task I10 — Intl & Tanggal Lanjutan

> **Level:** Intermediate · **Estimasi:** 75 menit · **Topik:** `Intl.DateTimeFormat`, `Intl.NumberFormat`, IANA time zone, durasi

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menampilkan tanggal dan jam untuk zona waktu berbeda.
2. Memformat mata uang dengan locale yang tepat.
3. Menghitung dan memformat durasi.

## Studi Kasus

Kopi Senja punya pelanggan luar negeri dan mitra di New York. Struk digital harus menampilkan waktu Jakarta dan New York dari satu timestamp yang sama. Harga juga perlu ditampilkan dalam IDR dan USD untuk laporan mitra.

Gunakan timestamp tetap:

```js
const waktu = new Date("2026-11-11T07:30:00Z");
```

## Yang Harus Dibuat

Buat file **`task-i10.js`** dengan fungsi:

| Fungsi | Tugas |
| --- | --- |
| `formatTanggal(date, timeZone)` | tanggal panjang bahasa Indonesia, misalnya `11 November 2026` |
| `formatJam(date, timeZone)` | jam dua digit, misalnya `14.30` |
| `formatUang(amount, locale, currency)` | format mata uang, spasi non-breaking diganti spasi biasa |
| `durasiMenit(mulai, selesai)` | selisih dalam menit |
| `formatDurasi(menit)` | `"2 jam 30 menit"` |

### Aturan format

- `formatTanggal` memakai `Intl.DateTimeFormat("id-ID", { dateStyle: "long", timeZone })`.
- `formatJam` memakai `Intl.DateTimeFormat("id-ID", { hour: "2-digit", minute: "2-digit", hour12: false, timeZone })`.
- `formatUang` memakai `Intl.NumberFormat(locale, { style: "currency", currency, maximumFractionDigits: currency === "IDR" ? 0 : 2 })`.
- Ganti karakter `\u00a0` (non-breaking space) dengan spasi biasa agar output stabil.
- `formatDurasi` menangani jam dan menit; jika menit `0`, hanya tampilkan jam.

## Skenario Program

```js
console.log("Jakarta:", formatTanggal(waktu, "Asia/Jakarta") + ", " + formatJam(waktu, "Asia/Jakarta"));
console.log("New York:", formatTanggal(waktu, "America/New_York") + ", " + formatJam(waktu, "America/New_York"));
console.log("IDR:", formatUang(60000, "id-ID", "IDR"));
console.log("USD:", formatUang(4, "en-US", "USD"));
console.log("Durasi:", formatDurasi(durasiMenit(new Date("2026-11-11T08:00:00Z"), new Date("2026-11-11T10:30:00Z"))));
```

## Ekspektasi Output

```text
Jakarta: 11 November 2026, 14.30
New York: 11 November 2026, 02.30
IDR: Rp 60.000
USD: $4.00
Durasi: 2 jam 30 menit
```

## Ketentuan

- Wajib memakai `Intl`, bukan perhitungan offset manual.
- Zona waktu harus berupa nama IANA, bukan `"WIB"` atau `"GMT+7"`.
- `formatUang` tidak boleh menulis simbol `Rp`/`$` secara manual.
- `durationMenit` harus mengembalikan angka bulat.
- `formatDurasi(60)` → `"1 jam"`, `formatDurasi(45)` → `"45 menit"`.

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| Jakarta dari `07:30Z` | `14.30` |
| New York dari `07:30Z` | `02.30` |
| New York saat DST (`2026-07-01T12:00:00Z`) | offset mengikuti DST |
| `formatUang(0, "id-ID", "IDR")` | `Rp 0` |
| `formatDurasi(90)` | `1 jam 30 menit` |
| `formatDurasi(0)` | `0 menit` |

## Checklist Sebelum Kumpul

- [ ] Zona waktu IANA dipakai.
- [ ] Tanggal dan jam konsisten untuk dua zona.
- [ ] Karakter spasi khusus dinormalisasi.
- [ ] Format IDR tidak menampilkan desimal.
- [ ] Durasi menangani 0 menit dan kelipatan jam.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Tambahkan `formatRelatif(date)` memakai `Intl.RelativeTimeFormat`.
2. Buat `jadwalBuka(date, timeZone)` yang mengembalikan status buka/tutup berdasarkan zona toko.
3. Tampilkan nama zona waktu panjang memakai `timeZoneName: "long"`.
