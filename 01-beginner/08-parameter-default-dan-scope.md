# Task 08 — Parameter Default & Scope: Format Harga

> **Level:** Dasar · **Estimasi:** 45 menit · **Topik:** parameter default, scope lokal, global, `undefined`

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Memberi nilai default pada parameter fungsi.
2. Memahami perbedaan variabel global dan lokal.
3. Menyusun fungsi kecil yang saling memanggil.

## Studi Kasus

Kopi Senja ingin menampilkan harga dalam beberapa format. Untuk pelanggan lokal, harga memakai awalan `Rp`. Untuk laporan ekspor, harga memakai awalan `$`. Selain itu, kasir butuh label menu yang bisa menampilkan harga setelah diskon, dengan diskon default `0` jika tidak ada promo.

## Yang Harus Dibuat

Buat file **`task-08.js`** dengan dua fungsi:

### 1. `formatRupiah(angka, prefix = "Rp")`

Mengembalikan string `prefix` diikuti angka **tanpa spasi dan tanpa titik**.

| Pemanggilan | Hasil |
| --- | --- |
| `formatRupiah(24000)` | `"Rp24000"` |
| `formatRupiah(24000, "$")` | `"$24000"` |
| `formatRupiah(0)` | `"Rp0"` |

### 2. `buatLabel(nama, harga, diskon = 0)`

Mengembalikan `${nama} - ${formatRupiah(harga - diskon)}`.

| Pemanggilan | Hasil |
| --- | --- |
| `buatLabel("Latte", 24000)` | `"Latte - Rp24000"` |
| `buatLabel("Latte", 24000, 2000)` | `"Latte - Rp22000"` |

## Ketentuan

- Parameter default harus ditulis di deklarasi fungsi, bukan di dalam `if`.
- `buatLabel` wajib memakai `formatRupiah`, bukan menggabungkan `"Rp"` sendiri.
- Gunakan `const` untuk nilai yang tidak berubah.
- Jangan mengubah nilai parameter di dalam fungsi.

## Ekspektasi Output

```text
Harga normal : Rp24000
Label diskon : Latte - Rp22000
Harga dolar  : $24000
```

## Eksperimen Scope

Tambahkan kode berikut di bagian bawah, lalu jalankan. Perhatikan error yang muncul.

```js
function contohScope() {
  const rahasia = "hanya di dalam fungsi";
  return rahasia;
}

console.log(contohScope());
// console.log(rahasia); // Buka komentar ini: ReferenceError
```

Tulis di komentar: mengapa `rahasia` tidak bisa diakses dari luar fungsi?

## Contoh Kasus Uji

| Pemanggilan | Hasil |
| --- | --- |
| `formatRupiah(15000, "USD ")` | `"USD 15000"` |
| `buatLabel("Espresso", 18000, 0)` | `"Espresso - Rp18000"` |
| `buatLabel("Espresso", 18000, 3000)` | `"Espresso - Rp15000"` |
| `formatRupiah(24000, undefined)` | `"Rp24000"` |
| `formatRupiah(24000, null)` | `"null24000"` |

## Checklist Sebelum Kumpul

- [ ] Parameter default ditulis dengan `=`.
- [ ] `formatRupiah` menghasilkan format tanpa spasi.
- [ ] `buatLabel` memanggil `formatRupiah`.
- [ ] Output sama persis dengan contoh.
- [ ] Menjelaskan perbedaan parameter `undefined` dan `null` pada komentar.

## Bonus

1. Tambahkan parameter ketiga `desimal = 0` pada `formatRupiah` untuk membulatkan angka.
2. Buat fungsi `buatLabelDiskon(nama, harga, persenDiskon = 0)` yang menghitung nominal diskon dari persen.
3. Jelaskan dalam komentar: mengapa variabel di dalam fungsi tidak bentrok dengan variabel global bernama sama?
