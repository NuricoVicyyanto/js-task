# Task I04 — Object Utilities & Optional Chaining

> **Level:** Intermediate · **Estimasi:** 60 menit · **Topik:** optional chaining `?.`, nullish coalescing `??`, `Object.entries`, `Object.fromEntries`, normalisasi data

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Mengakses properti bersarang dengan aman memakai `?.`.
2. Memberi nilai default tanpa menimpa nilai `0` atau `""` memakai `??`.
3. Mengubah objek menjadi array pasangan dan sebaliknya.

## Studi Kasus

Kopi Senja menerima data pelanggan dari berbagai sumber. Sebagian data tidak lengkap: `telepon` bernilai `null`, `preferensi` tidak ada, dan sebagian pelanggan tidak mengisi alamat. Program tidak boleh error dan harus menampilkan nilai default yang masuk akal.

## Data Awal

```js
const pelanggan = {
  nama: "Nadia",
  telepon: null,
  alamat: { jalan: "Jl. Merdeka 10", kota: "Bandung" },
  preferensi: undefined,
};
```

## Yang Harus Dibuat

Buat file **`task-i04.js`** dengan fungsi:

| Fungsi | Tugas |
| --- | --- |
| `normalisasiPelanggan(data)` | mengembalikan `{ nama, telepon, kota, preferensi }` dengan default `"-"`, memakai `Object.fromEntries` |
| `formatAlamat(data)` | `"Jl. Merdeka 10, Bandung"` atau `"Alamat belum diisi"` |
| `hitungProperti(data)` | jumlah properti top-level dengan `Object.keys` |
| `propertiTerisi(data)` | array key yang nilainya bukan `null`/`undefined` |

## Ekspektasi Output

```text
Nama: Nadia
Telepon: -
Kota: Bandung
Preferensi: -
Jumlah properti: 4
Alamat: Jl. Merdeka 10, Bandung
Properti terisi: nama, alamat
```

## Ketentuan

- Gunakan `?.` untuk akses bersarang.
- Gunakan `??`, bukan `||`, untuk nilai default.
- `normalisasiPelanggan` tidak boleh mengubah objek asli.
- `propertiTerisi` memakai `Object.entries` dan `filter`.
- Jangan menulis `if (data.alamat && data.alamat.kota)` berulang-ulang.

## Kasus Uji

| Data | Hasil |
| --- | --- |
| `alamat` tidak ada | `kota: "-"`, alamat `"Alamat belum diisi"` |
| `telepon: 0` | tetap `0`, bukan `"-"` |
| `nama: ""` | tetap `""`, bukan default (gunakan `??`) |
| `preferensi: "dingin"` | `"dingin"` |
| Objek kosong | semua default, jumlah properti `0` |

## Checklist Sebelum Kumpul

- [ ] Tidak ada error saat `alamat` atau `pelanggan` tidak ada.
- [ ] `??` dipakai, bukan `||`.
- [ ] Objek asli tidak berubah.
- [ ] `Object.entries` dan `Object.fromEntries` sama-sama dipakai minimal sekali.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Buat `gabungDefault(data, default)` yang menggabungkan objek secara dangkal.
2. Buat `deepMerge(a, b)` untuk objek bersarang tanpa mengubah input.
3. Bekukan hasil normalisasi dengan `Object.freeze`, lalu buktikan perubahan ditolak.
