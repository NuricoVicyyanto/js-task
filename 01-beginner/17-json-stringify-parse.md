# Task 17 — JSON: Simpan & Baca Data Pesanan

> **Level:** Menengah · **Estimasi:** 50 menit · **Topik:** `JSON.stringify()`, `JSON.parse()`, data terstruktur, salinan data

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Mengubah objek JavaScript menjadi string JSON.
2. Mengubah string JSON kembali menjadi objek.
3. Mengakses data hasil parse dan memahami bahwa hasilnya adalah salinan baru.

## Studi Kasus

Kopi Senja ingin mengirim detail pesanan ke layanan lain. Layanan tersebut hanya menerima data berbentuk teks JSON, bukan objek JavaScript. Kasir juga perlu membaca kembali JSON yang diterima untuk menampilkan ringkasan pesanan.

## Data Awal

```js
const pesanan = {
  id: "KS-001",
  pelanggan: "Nadia",
  items: [
    { nama: "Espresso", harga: 18000, jumlah: 2 },
    { nama: "Latte", harga: 24000, jumlah: 1 },
  ],
  total: 60000,
  status: "baru",
};
```

## Yang Harus Dibuat

Buat file **`task-17.js`** yang:

1. Mengubah `pesanan` menjadi string JSON dan menyimpannya di `jsonPesanan`.
2. Mencetak string JSON tersebut.
3. Mengubah `jsonPesanan` kembali menjadi objek dan menyimpannya di `pesananHasilParse`.
4. Mencetak tipe data hasil parse.
5. Mencetak pelanggan, total, dan jumlah item dari hasil parse.
6. Mengubah `pelanggan` pada hasil parse menjadi `"Budi"`, lalu membuktikan `pesanan` asli tetap `"Nadia"`.

## Ketentuan

- Gunakan `JSON.stringify()` dan `JSON.parse()`, bukan menulis string JSON manual.
- String JSON harus memakai tanda kutip ganda untuk key dan nilai teks.
- Jangan mengubah objek `pesanan` asli.
- Jumlah item dihitung dari `items.length`.

## Ekspektasi Output

```text
JSON pesanan:
{"id":"KS-001","pelanggan":"Nadia","items":[{"nama":"Espresso","harga":18000,"jumlah":2},{"nama":"Latte","harga":24000,"jumlah":1}],"total":60000,"status":"baru"}
Tipe data setelah parse: object
Pelanggan: Nadia
Total: Rp60000
Jumlah item: 2
Pelanggan asli tetap: Nadia
```

## Contoh Kasus Uji

| Pemeriksaan | Hasil yang diharapkan |
| --- | --- |
| `typeof jsonPesanan` | `string` |
| `typeof pesananHasilParse` | `object` |
| `pesananHasilParse.items.length` | `2` |
| `pesananHasilParse === pesanan` | `false` |
| `JSON.parse("bukan json")` | melempar `SyntaxError` |

## Checklist Sebelum Kumpul

- [ ] JSON dibuat dengan `JSON.stringify`.
- [ ] JSON dibaca dengan `JSON.parse`.
- [ ] Hasil parse bisa diakses seperti objek biasa.
- [ ] Objek asli tidak berubah setelah hasil parse diubah.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Cetak JSON yang lebih mudah dibaca dengan `JSON.stringify(pesanan, null, 2)`.
2. Tambahkan properti `catatan: undefined`, lalu jelaskan mengapa properti itu hilang dari JSON.
3. Bungkus `JSON.parse` dengan `try/catch` dan tampilkan pesan jika JSON tidak valid.
