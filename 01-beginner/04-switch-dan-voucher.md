# Task 04 — Switch & Validasi Voucher

> **Level:** Dasar · **Estimasi:** 40 menit · **Topik:** `switch`, `case`, `break`, `default`, validasi string

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Memilih satu dari beberapa kemungkinan menggunakan `switch`.
2. Menggunakan `break` agar eksekusi tidak jatuh ke `case` berikutnya.
3. Menangani nilai yang tidak dikenali dengan `default`.

## Studi Kasus

Kopi Senja menerima kode voucher dari pelanggan. Kasir harus memeriksa kode tersebut dan menentukan potongan yang didapat. Kode yang berlaku:

| Kode | Manfaat |
| --- | --- |
| `SENJA10` | Diskon 10% |
| `SENJA20` | Diskon 20% |
| `GRATISONGKIR` | Gratis ongkir |

Kode selain itu dianggap tidak valid. Untuk task ini, fokuslah pada penentuan manfaat voucher, belum pada perhitungan total belanja.

## Yang Harus Dibuat

Buat file **`task-04.js`** dengan data awal:

```js
const kodeVoucher = "SENJA20";
```

Program harus:

1. Memeriksa kode menggunakan `switch`.
2. Menentukan `status` (`"valid"` atau `"tidak valid"`).
3. Menentukan `potongan` (10, 20, atau 0 dalam persen).
4. Menentukan `keterangan` yang sesuai.
5. Mencetak hasil sesuai format.

## Ketentuan

- Gunakan `switch`, bukan `if / else if`.
- Setiap `case` wajib diakhiri `break`.
- Kode bersifat **case-sensitive**: `senja20` dianggap tidak valid.
- Untuk `GRATISONGKIR`, potongan tetap `0%`, tetapi keterangannya `Gratis ongkir`.

## Ekspektasi Output

Jalankan `node task-04.js`. Output harus **persis** seperti ini:

```text
Kode voucher : SENJA20
Status       : valid
Potongan     : 20%
Keterangan   : Diskon 20%
```

## Contoh Kasus Uji

| `kodeVoucher` | Status | Potongan | Keterangan |
| --- | --- | --- | --- |
| `"SENJA10"` | valid | 10% | Diskon 10% |
| `"SENJA20"` | valid | 20% | Diskon 20% |
| `"GRATISONGKIR"` | valid | 0% | Gratis ongkir |
| `"SENJA99"` | tidak valid | 0% | Kode tidak dikenali |
| `""` | tidak valid | 0% | Kode tidak dikenali |
| `"senja10"` | tidak valid | 0% | Kode tidak dikenali |

## Checklist Sebelum Kumpul

- [ ] Semua kode yang berlaku ditangani.
- [ ] `default` menangani kode tidak dikenal dan string kosong.
- [ ] Tidak ada `case` yang lupa `break`.
- [ ] Output berubah dengan benar saat kode diganti.
- [ ] Tidak ada perhitungan total belanja di task ini.

## Bonus

1. Ubah program agar menerima kode huruf kecil, misalnya `senja10`, dengan mengubah input menjadi huruf besar memakai `toUpperCase()`.
2. Tambahkan kode `SENJA50` dengan syarat minimal belanja Rp200.000. Tampilkan keterangan `Minimal belanja Rp200000` jika syarat belum terpenuhi.
3. Jelaskan dalam komentar: apa yang terjadi jika `break` dihapus dari `case "SENJA10"`?
