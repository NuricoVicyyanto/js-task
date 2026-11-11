# Level 02 — Intermediate — 15 Task JavaScript Lanjutan

Folder ini berisi **15 task** untuk siswa yang sudah menguasai dasar JavaScript: variabel, kondisi, perulangan, fungsi, array, objek, DOM, dan `fetch` dasar. Fokus level ini adalah **menulis kode yang bisa dirawat**: modul, class, error, testing, async, dan arsitektur kecil.

## Prasyarat

Siswa sudah mampu:

- Menulis fungsi dengan parameter dan `return`.
- Menggunakan `map`, `filter`, `reduce`, dan `sort`.
- Mengakses DOM dan menangani event.
- Menggunakan `localStorage`, `fetch`, dan `async/await` dasar.
- Menjalankan Node.js dan browser dari terminal.

Jika belum, selesaikan [Level 01 — Beginner](../01-beginner/README.md) terlebih dahulu.

## Hasil Belajar

Setelah 15 task, siswa mampu:

1. Memecah aplikasi menjadi modul dan layer.
2. Menggunakan closure, higher-order function, class, dan functional pipeline.
3. Menangani error dan retry secara terstruktur.
4. Mengelola konkurensi dan API client.
5. Menulis unit test dengan `node:test`.
6. Membuat CLI dengan file I/O yang aman.
7. Membangun state management DOM yang konsisten.

## Peta 15 Task

| No | Task | Topik Inti | Estimasi |
| --- | --- | --- | --- |
| 01 | [ES Modules & Struktur Proyek](./01-es-modules-struktur-proyek.md) | `import`/`export`, `package.json`, dependency graph | 60 menit |
| 02 | [Closure & Higher-Order Function](./02-closure-dan-higher-order-function.md) | closure, factory, memoization | 75 menit |
| 03 | [Array Pipeline Lanjutan](./03-array-pipeline-lanjutan.md) | `reduce`, `flatMap`, `some`, `every` | 75 menit |
| 04 | [Object Utilities & Optional Chaining](./04-object-utilities-dan-optional-chaining.md) | `?.`, `??`, `Object.entries` | 60 menit |
| 05 | [Class & Inheritance](./05-class-dan-inheritance.md) | `extends`, `super`, getter, static | 75 menit |
| 06 | [Custom Error & Retry](./06-custom-error-dan-retry.md) | error class, `cause`, retry | 75 menit |
| 07 | [Promise Combinator & Concurrency](./07-promise-combinator-dan-concurrency.md) | `allSettled`, concurrency pool | 90 menit |
| 08 | [Fetch API Client](./08-fetch-api-client.md) | `URL`, timeout, error HTTP | 90 menit |
| 09 | [Unit Testing `node:test`](./09-unit-testing-node-test.md) | test, assertion, boundary | 90 menit |
| 10 | [Intl & Tanggal Lanjutan](./10-intl-dan-tanggal-lanjutan.md) | `Intl`, time zone, currency | 75 menit |
| 11 | [Regex Lanjutan](./11-regex-lanjutan.md) | named groups, replace callback | 75 menit |
| 12 | [Functional Programming](./12-functional-programming.md) | curry, pipe, immutable | 90 menit |
| 13 | [DOM State Management](./13-dom-state-management.md) | single state, render, delegation | 120 menit |
| 14 | [Node.js File I/O & CLI](./14-node-file-io-dan-cli.md) | `fs/promises`, `parseArgs`, CSV | 100 menit |
| 15 | [Mini Project CLI Inventory](./15-mini-project-cli-inventory.md) | repository, service, CLI, persistensi | 3–4 jam |

**Total estimasi:** ±23 jam.

## Rencana Kelas 10 Sesi

| Sesi | Materi | Fokus |
| --- | --- | --- |
| 1 | I01–I02 | Modul dan closure |
| 2 | I03–I04 | Pipeline array dan object utilities |
| 3 | I05–I06 | Class dan error |
| 4 | I07 | Concurrency |
| 5 | I08 | API client |
| 6 | I09 | Testing |
| 7 | I10–I11 | Intl dan regex |
| 8 | I12 | Functional programming |
| 9 | I13–I14 | State DOM dan CLI file I/O |
| 10 | I15 | Presentasi mini project |

## Aturan

- Setiap task harus bisa dijalankan dari terminal atau browser tanpa error.
- Gunakan ES Modules (`"type": "module"`) untuk task Node.
- Jangan memakai framework; library hanya diperbolehkan jika task menyebutkannya.
- Utamakan kode yang bisa diuji: fungsi kecil, input/output jelas.
- Sertakan penanganan error; jangan biarkan program crash tanpa pesan.

## Penilaian

Gunakan [rubrik penilaian](../docs/rubrik-penilaian.md). Komponen tambahan untuk level intermediate:

| Komponen | Bobot |
| --- | --- |
| Perilaku dan output | 45 |
| Pemisahan tanggung jawab | 20 |
| Penanganan error & kasus batas | 15 |
| Keterbacaan dan konsistensi | 10 |
| Testing/dokumentasi | 10 |

## Lanjut ke Level Expert

Setelah menguasai modul, testing, async, dan arsitektur dasar, lanjut ke [Level 03 — Expert](../03-expert/README.md).
