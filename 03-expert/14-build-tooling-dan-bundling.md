# Task E14 — Build Tooling & Bundling

> **Level:** Expert · **Estimasi:** 4 jam · **Topik:** Vite, environment variable, code splitting, source map, bundle budget, tree shaking

## Tujuan

Mengubah source frontend modular menjadi bundle produksi yang kecil, aman, dan bisa di-cache, serta membuktikan tidak ada secret yang bocor.

## Studi Kasus

Frontend kasir Kopi Senja masih memuat 15 file script terpisah. Halaman lambat, cache tidak efektif, dan URL API ditulis manual di kode. Tim meminta build produksi dengan asset hashing, environment variable, code splitting, dan budget ukuran.

## Yang Harus Dibuat (File)

```text
e14-build/
├── index.html
├── vite.config.js
├── package.json
├── .env.example
├── src/
│   ├── main.js
│   ├── api.js
│   ├── ui.js
│   ├── style.css
│   └── laporan.js
└── scripts/
    └── check-budget.js
```

## Fitur Build

### Environment

- `VITE_API_URL` dibaca dari `.env`.
- Jika tidak ada, gunakan `/api`.
- Hanya variabel berawalan `VITE_` yang boleh masuk ke client.
- `.env.example` berisi nama variabel, bukan nilai rahasia.

### Code splitting

- `laporan.js` dimuat dinamis saat tombol **Lihat Laporan** diklik:

```js
const { tampilkanLaporan } = await import("./laporan.js");
```

- Bundle awal tidak boleh memuat kode laporan.

### Build

`vite.config.js`:

- `build.outDir = "dist"`.
- `build.sourcemap = true`.
- `build.target = "es2020"`.
- Asset file name memakai hash.
- `base = "/"`.

### Budget

`scripts/check-budget.js`:

- Membaca semua file di `dist/assets`.
- Menghitung ukuran gzip memakai `node:zlib`.
- Gagal (`exit 1`) jika total JavaScript > **100 kB** gzip atau CSS > **20 kB** gzip.
- Mencetak ukuran per file dan status.

## Script `package.json`

```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build && node scripts/check-budget.js",
    "preview": "vite preview"
  }
}
```

## Ekspektasi Output

```text
dist/index.html
dist/assets/index-a1b2c3.js       42.1 kB (gzip 14.3 kB)
dist/assets/index-d4e5f6.css       3.2 kB (gzip 1.1 kB)
dist/assets/laporan-g7h8i9.js      8.4 kB (gzip 3.0 kB)
Build time: 1.8 s
Budget JS: 17.3 kB / 100 kB PASS
Budget CSS: 1.1 kB / 20 kB PASS
```

Ukuran aktual boleh berbeda; yang wajib adalah **budget PASS** dan file laporan terpisah.

## Pemeriksaan Wajib

1. Jalankan build dengan `VITE_API_URL=https://api.kopisenja.id`.
2. Cari URL tersebut di bundle → harus ada.
3. Cari `SECRET`, `PASSWORD`, atau token contoh di bundle → tidak boleh ada.
4. Pastikan `laporan-*.js` tidak dimuat di awal (cek Network tab).
5. Jalankan build dua kali → hash file sama jika source sama.
6. Buka source map dan pastikan mengarah ke source asli.

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| `VITE_API_URL` kosong | fallback `/api` |
| Env rahasia tanpa prefix `VITE_` | tidak masuk bundle |
| Tombol laporan diklik | chunk laporan baru dimuat |
| Total JS > budget | build gagal, exit code `1` |
| Build ulang tanpa perubahan | hash stabil |
| Console produksi | tidak ada error |

## Ketentuan

- Jangan menaruh secret di `VITE_*`; semua variabel tersebut publik.
- Jangan mematikan minify hanya agar mudah dibaca.
- Jangan mengimpor seluruh library jika hanya butuh satu fungsi.
- Jangan menonaktifkan source map tanpa alasan.
- Jangan mengunggah `.env` asli ke repository.
- Jangan memakai `eval` atau `new Function` yang menghalangi optimasi.

## Checklist Sebelum Kumpul

- [ ] Build menghasilkan `dist/`.
- [ ] Asset memakai hash.
- [ ] `laporan.js` menjadi chunk terpisah.
- [ ] `VITE_API_URL` dipakai dan fallback bekerja.
- [ ] Tidak ada secret di bundle.
- [ ] Budget berjalan dan gagal saat melebihi batas.
- [ ] Output build sesuai format.

## Bonus

1. Buat analisis bundle (rollup-plugin-visualizer) dan jelaskan 3 dependensi terbesar.
2. Tambahkan `build.rollupOptions.output.manualChunks` untuk vendor.
3. Bandingkan strategi SPA, SSR, dan static prerender untuk halaman menu.
