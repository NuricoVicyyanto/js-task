# Task E12 — CI/CD & Code Quality

> **Level:** Expert · **Estimasi:** 3–4 jam · **Topik:** GitHub Actions, lint, format, test gate, coverage, artifact, semantic versioning

## Tujuan

Membuat pipeline yang menolak kode rusak sebelum masuk ke branch utama, serta menghasilkan artifact yang bisa dirilis.

## Studi Kasus

Tim Kopi Senja sering menerima pull request yang lulus di laptop pengembang tetapi gagal di production. Mereka meminta pipeline CI yang menjalankan lint, test, coverage, dan build pada setiap push/PR, serta artifact yang bisa diunduh.

## Yang Harus Dibuat (Struktur)

```text
e12-ci/
├── .github/
│   └── workflows/
│       └── ci.yml
├── src/
│   └── pricing.js
├── test/
│   └── pricing.test.js
├── eslint.config.js
├── .prettierrc
├── package.json
└── package-lock.json
```

## Script Wajib di `package.json`

```json
{
  "scripts": {
    "lint": "eslint .",
    "format:check": "prettier --check .",
    "test": "node --test",
    "test:coverage": "node --test --experimental-test-coverage",
    "build": "node scripts/build.js"
  }
}
```

## Pipeline `ci.yml`

Trigger:

- `push` ke `main`.
- `pull_request` ke `main`.
- `workflow_dispatch`.

Job `quality`:

1. Checkout.
2. Setup Node dengan matrix `[22, 24]`.
3. Cache dependency npm.
4. `npm ci`.
5. `npm run lint`.
6. `npm run format:check`.
7. `npm run test:coverage`.
8. `npm run build`.

Job `artifact` (hanya setelah `quality` sukses, Node 24):

1. Download hasil build.
2. Upload artifact `app-dist` dengan retensi 7 hari.

Aturan workflow:

- `permissions: contents: read`.
- `concurrency` membatalkan run lama pada branch yang sama.
- `timeout-minutes: 10`.
- Jangan mencetak secret.
- Gunakan `npm ci`, bukan `npm install`.
- Coverage di bawah 85% harus menggagalkan pipeline.
- Build harus deterministik (tidak ada timestamp acak di output).

## Build

`scripts/build.js` menyalin `src/` ke `dist/` dan menulis `dist/build-info.json`:

```json
{
  "name": "kopi-senja-ci",
  "version": "1.2.0",
  "node": "24"
}
```

Jangan menyertakan waktu build agar artifact deterministik.

## Ekspektasi Output Pipeline

```text
lint: pass
format: pass
test: pass (24)
coverage: 87%
build: dist/
artifact: app-dist (7 days)
```

Jika lint gagal, test gagal, atau coverage < 85%, job harus **merah** dan artifact tidak diunggah.

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| Kode dengan `var` | lint gagal |
| Format tidak sesuai Prettier | `format:check` gagal |
| Satu test gagal | pipeline gagal, artifact tidak dibuat |
| Coverage 84% | pipeline gagal |
| Node 22 dan 24 | keduanya diuji |
| Push baru saat run lama berjalan | run lama dibatalkan |
| Build dijalankan 2× | isi artifact identik |

## Ketentuan

- Jangan memakai `continue-on-error` untuk lint/test.
- Jangan menyimpan token di workflow.
- Jangan memakai `actions/checkout@master`; gunakan versi tag/SHA.
- Jangan mengunggah `node_modules` sebagai artifact.
- Jangan membuat build bergantung pada jam sistem.
- Jangan menonaktifkan aturan lint hanya agar pipeline hijau.

## Checklist Sebelum Kumpul

- [ ] Workflow berjalan pada push dan PR.
- [ ] Matrix Node 22/24.
- [ ] `npm ci` dan cache dipakai.
- [ ] Lint, format, test, coverage, build berjalan berurutan.
- [ ] Coverage gate 85% diterapkan.
- [ ] Artifact hanya dibuat setelah job quality sukses.
- [ ] Permission minimal dan concurrency aktif.
- [ ] Output sesuai contoh.

## Bonus

1. Tambahkan `npm audit --omit=dev` dengan kebijakan yang jelas.
2. Buat workflow rilis otomatis saat tag `v*` dibuat.
3. Tambahkan build Docker multi-stage dan scan image.
