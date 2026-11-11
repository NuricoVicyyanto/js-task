# Task I01 — ES Modules & Struktur Proyek

> **Level:** Intermediate · **Estimasi:** 60 menit · **Topik:** `import`/`export`, `package.json`, pemisahan tanggung jawab, dependency graph

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Memecah satu file monolitik menjadi beberapa modul.
2. Menggunakan named export dan default export dengan tepat.
3. Menjalankan proyek Node.js berbasis ES Modules.

## Studi Kasus

Aplikasi kasir Kopi Senja mulai sulit dirawat karena semua kode——data menu, format harga, dan perhitungan pesanan——berada dalam satu file. Manajer meminta kode dipisah berdasarkan tanggung jawab agar mudah diuji dan dikembangkan.

## Yang Harus Dibuat (Struktur)

```text
i01-es-modules/
├── package.json
└── src/
    ├── index.js
    ├── data/
    │   └── menu.js
    ├── utils/
    │   └── format.js
    └── services/
        └── order.js
```

`package.json` minimal:

```json
{
  "name": "kopi-senja-modules",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "start": "node src/index.js"
  }
}
```

## Tanggung Jawab Modul

| File | Isi | Bentuk Export |
| --- | --- | --- |
| `data/menu.js` | array `menu` berisi 3 menu | named export |
| `utils/format.js` | `formatRupiah(angka)` | named export |
| `services/order.js` | `hitungSubtotal(items)`, `buatPesanan(items)` | named + default |
| `index.js` | merangkai semuanya dan mencetak hasil | tidak perlu export |

### Data menu

```js
export const menu = [
  { nama: "Espresso", harga: 18000 },
  { nama: "Latte", harga: 24000 },
  { nama: "Croissant", harga: 25000 },
];
```

### Bentuk hasil `buatPesanan`

```js
{
  items: [
    { nama: "Espresso", harga: 18000, qty: 2 },
    { nama: "Latte", harga: 24000, qty: 1 }
  ],
  subtotal: 60000,
  totalItem: 3,
  rincian: "2x Espresso, 1x Latte"
}
```

## Ketentuan

- Gunakan **ES Modules**, bukan `require`/`module.exports`.
- Semua import harus menyertakan ekstensi `.js`.
- Tidak boleh ada data menu yang ditulis ulang di `index.js`.
- Tidak boleh ada variabel global yang dipakai lintas modul.
- `buatPesanan` wajib memanggil `hitungSubtotal`.
- `index.js` wajib memakai `formatRupiah` untuk mencetak subtotal.
- Tidak ada circular import.

## Ekspektasi Output

Jalankan `node src/index.js` dari folder proyek. Output harus **persis**:

```text
Subtotal: Rp60000
Total item: 3
Rincian: 2x Espresso, 1x Latte
```

## Kasus Uji

| Pemeriksaan | Hasil |
| --- | --- |
| `node src/index.js` | Output sesuai contoh |
| Menambah item di `data/menu.js` | Tidak merusak import lain |
| Memanggil `buatPesanan([])` | `subtotal: 0`, `totalItem: 0`, `rincian: ""` |
| Menghapus export yang dipakai | Error jelas saat start, bukan `undefined` diam-diam |

## Checklist Sebelum Kumpul

- [ ] `package.json` memiliki `"type": "module"`.
- [ ] Ada 3 folder: `data`, `utils`, `services`.
- [ ] `formatRupiah` hanya didefinisikan di satu tempat.
- [ ] `index.js` tidak berisi logika perhitungan.
- [ ] Default export digunakan minimal satu kali.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Tambahkan `src/index.js` di setiap folder sebagai barrel export.
2. Gunakan dynamic `import()` untuk memuat modul laporan hanya saat dibutuhkan.
3. Buat diagram dependency graph singkat di komentar `README` proyek.
