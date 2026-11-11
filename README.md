# JavaScript Beginner — 30 Task Studi Kasus "Kopi Senja"

Kumpulan **30 task JavaScript untuk pemula**, disusun bertahap dari variabel sampai aplikasi kasir sederhana. Setiap task adalah studi kasus mandiri dengan cerita, instruksi, ekspektasi output, kasus uji, dan checklist penilaian.

Materi ini dirancang untuk kelas profesional: pengajar bisa langsung mengajar, dan siswa bisa langsung praktik tanpa starter code yang rumit.

---

## Untuk Siapa Materi Ini?

- Siswa yang **belum pernah** atau baru mulai belajar JavaScript.
- Kelas bootcamp, kursus, ekstrakurikuler, atau belajar mandiri.
- Pengajar yang membutuhkan modul latihan siap pakai dengan output yang jelas.

## Prasyarat

| Kebutuhan | Keterangan |
| --- | --- |
| Node.js | Versi 18 atau lebih baru, untuk task 01–23 dan 28–29 |
| Browser modern | Chrome, Edge, atau Firefox, untuk task 24–30 |
| Editor kode | VS Code atau editor lain |
| Pengetahuan dasar | Bisa membuat file, membuka terminal, dan menjalankan perintah |

Tidak ada dependency atau `npm install`. Semua task memakai JavaScript bawaan.

---

## Cara Menggunakan Materi

1. **Baca README root ini** untuk melihat urutan task.
2. Buka file task yang sesuai, misalnya `tasks/01-variabel-dan-tipe-data.md`.
3. Baca bagian **Studi Kasus** sampai **Ekspektasi Output**.
4. Buat file kerja sesuai instruksi, misalnya `task-01.js`.
5. Kerjakan, jalankan, lalu bandingkan hasilnya dengan **Ekspektasi Output**.
6. Centang **Checklist Sebelum Kumpul**. Jika ada yang belum, perbaiki dulu.
7. Kerjakan **Bonus** hanya setelah bagian wajib selesai.

> **Aturan penting:** jangan lanjut ke task berikutnya jika output task sekarang belum sesuai. Setiap task memakai konsep dari task sebelumnya.

## Struktur Folder

```text
js-task/
├── README.md                     ← kamu di sini
├── docs/
│   ├── panduan-pengajar.md       ← alur kelas, tips mengajar
│   ├── rubrik-penilaian.md       ← cara menilai 30 task
│   └── glosarium.md              ← istilah JavaScript
└── tasks/
    ├── 01-variabel-dan-tipe-data.md
    ├── 02-operator-dan-template-literal.md
    ├── ...
    └── 30-capstone-aplikasi-kasir.md
```

Setiap task berisi bagian yang konsisten:

- Tujuan pembelajaran
- Studi kasus
- Yang harus dibuat
- Ketentuan
- Ekspektasi output
- Contoh kasus uji
- Checklist sebelum kumpul
- Bonus

---

## Peta 30 Task

### Bagian 1 — Fondasi (Task 01–08)

Fokus: variabel, operator, percabangan, perulangan, dan fungsi dasar.

| No | Task | Topik Inti | Estimasi |
| --- | --- | --- | --- |
| 01 | [Variabel & Tipe Data](tasks/01-variabel-dan-tipe-data.md) | `const`, `let`, string, number, boolean, template literal | 30 menit |
| 02 | [Operator & Template Literal](tasks/02-operator-dan-template-literal.md) | aritmatika, urutan operasi, struk | 40 menit |
| 03 | [Percabangan if/else](tasks/03-percabangan-if-else.md) | `if`, `else if`, diskon, ongkir | 45 menit |
| 04 | [Switch & Voucher](tasks/04-switch-dan-voucher.md) | `switch`, `case`, `break`, validasi | 40 menit |
| 05 | [Perulangan for](tasks/05-perulangan-for.md) | `for`, indeks, array sederhana | 40 menit |
| 06 | [While & Nested Loop](tasks/06-perulangan-while-dan-nested-loop.md) | `while`, nested loop, pola | 45 menit |
| 07 | [Fungsi & Return](tasks/07-fungsi-dan-return.md) | parameter, `return`, komposisi fungsi | 50 menit |
| 08 | [Parameter Default & Scope](tasks/08-parameter-default-dan-scope.md) | default parameter, scope lokal/global | 45 menit |

### Bagian 2 — Array & Objek (Task 09–15)

Fokus: menyimpan banyak data dan mengolahnya.

| No | Task | Topik Inti | Estimasi |
| --- | --- | --- | --- |
| 09 | [Array Dasar](tasks/09-array-dasar.md) | indeks, `.length`, update, `.join()` | 40 menit |
| 10 | [Method Array](tasks/10-method-array-mutasi.md) | `push`, `pop`, `shift`, `unshift`, `includes`, `indexOf` | 50 menit |
| 11 | [Objek Dasar](tasks/11-objek-dasar.md) | properti, dot/bracket notation, update | 45 menit |
| 12 | [Array of Objects: map & filter](tasks/12-array-of-objects-map-filter.md) | `.map()`, `.filter()`, chaining | 60 menit |
| 13 | [reduce & sort](tasks/13-reduce-dan-sort.md) | `.reduce()`, comparator, laporan | 60 menit |
| 14 | [Destructuring & Spread](tasks/14-destructuring-dan-spread.md) | destructuring, spread, immutability | 50 menit |
| 15 | [Nested Object & Array](tasks/15-nested-object-dan-array.md) | data bersarang, subtotal pesanan | 60 menit |

### Bagian 3 — Data & Logika Lanjutan (Task 16–23)

Fokus: method objek, JSON, struktur data, string, tanggal, error, dan regex.

| No | Task | Topik Inti | Estimasi |
| --- | --- | --- | --- |
| 16 | [Object Method & this](tasks/16-object-method-dan-this.md) | method objek, `this`, keranjang | 60 menit |
| 17 | [JSON](tasks/17-json-stringify-parse.md) | `JSON.stringify`, `JSON.parse` | 50 menit |
| 18 | [Set & Map](tasks/18-set-dan-map.md) | data unik, rekap key-value | 60 menit |
| 19 | [String Methods](tasks/19-string-methods.md) | `trim`, `toLowerCase`, `includes`, `slice` | 50 menit |
| 20 | [Format Struk](tasks/20-format-struk-padend.md) | `padEnd`, `padStart`, perataan | 60 menit |
| 21 | [Date & Waktu](tasks/21-date-dan-waktu.md) | `Date`, jam operasional, format tanggal | 60 menit |
| 22 | [Error Handling](tasks/22-error-handling.md) | `throw`, `try/catch`, validasi | 60 menit |
| 23 | [Regex Dasar](tasks/23-regex-dasar.md) | pola, anchor, `.test()` | 60 menit |

### Bagian 4 — DOM & Browser (Task 24–27)

Fokus: menampilkan data dan menangani interaksi di browser.

| No | Task | Topik Inti | Estimasi |
| --- | --- | --- | --- |
| 24 | [DOM: Render Menu](tasks/24-dom-render-menu.md) | `querySelector`, `createElement`, `textContent` | 75 menit |
| 25 | [DOM: Form Tambah Menu](tasks/25-dom-event-form.md) | event submit, `preventDefault`, validasi | 75 menit |
| 26 | [DOM: Keranjang & Total](tasks/26-dom-keranjang-total.md) | `dataset`, `remove()`, hitung total | 90 menit |
| 27 | [localStorage](tasks/27-localstorage.md) | simpan, muat, hapus, JSON rusak | 75 menit |

### Bagian 5 — Async & Proyek Akhir (Task 28–30)

Fokus: proses asynchronous dan menggabungkan semua materi.

| No | Task | Topik Inti | Estimasi |
| --- | --- | --- | --- |
| 28 | [Callback & Promise](tasks/28-callback-dan-promise.md) | callback, Promise, `Promise.all` | 75 menit |
| 29 | [async/await & fetch](tasks/29-async-await-fetch.md) | `fetch`, `await`, `try/catch`, render | 90 menit |
| 30 | [Capstone: Aplikasi Kasir](tasks/30-capstone-aplikasi-kasir.md) | gabungan DOM, data, localStorage, struk | 4–6 jam |

**Total estimasi:** sekitar 32 jam belajar, termasuk capstone.

---

## Rencana Kelas 16 Sesi

Setiap sesi 120 menit. Task yang lebih ringan digabung; task besar diberi waktu sendiri.

| Sesi | Materi | Fokus Sesi |
| --- | --- | --- |
| 1 | Task 01–02 | Variabel, tipe data, operator, output |
| 2 | Task 03–04 | Percabangan dan switch |
| 3 | Task 05–06 | Perulangan dan pola |
| 4 | Task 07–08 | Fungsi, parameter, scope |
| 5 | Task 09–10 | Array dan method dasar |
| 6 | Task 11–12 | Objek dan array of objects |
| 7 | Task 13 | reduce, sort, laporan |
| 8 | Task 14–15 | Destructuring, spread, data bersarang |
| 9 | Task 16–17 | Method objek dan JSON |
| 10 | Task 18–19 | Set, Map, string |
| 11 | Task 20–21 | Format struk dan tanggal |
| 12 | Task 22–23 | Error handling dan regex |
| 13 | Task 24–25 | Render DOM dan form |
| 14 | Task 26–27 | Keranjang dan localStorage |
| 15 | Task 28–29 | Callback, Promise, fetch |
| 16 | Task 30 | Presentasi dan review capstone |

Jika kelas hanya punya 8 sesi, gabungkan sesi 1–2, 3–4, dan seterusnya, lalu jadikan capstone tugas akhir mandiri.

---

## Aturan Pengerjaan

1. **Satu task, satu file kerja.** Gunakan nama file yang diminta pada task.
2. **Utamakan output yang benar** sebelum memperindah kode.
3. **Jangan menyalin jawaban teman.** Diskusi boleh, menulis ulang kode sendiri wajib.
4. **Boleh mencari dokumentasi** (MDN) dan bertanya, tetapi pahami setiap baris yang ditulis.
5. **Jangan lompat task.** Konsep task berikutnya bergantung pada task sebelumnya.
6. **Commit pekerjaan** secara berkala jika memakai Git (misalnya `task 01 selesai`).
7. **Kumpulkan file kerja + jawaban bonus** sesuai instruksi pengajar.

### Kebijakan Penggunaan AI

AI boleh dipakai sebagai **tutor**: menjelaskan konsep, menunjukkan error, atau memberi petunjuk. AI **tidak boleh** dipakai untuk menghasilkan seluruh jawaban tanpa dipahami.

Jika memakai AI, tulis di komentar file:

```js
// Dibantu AI untuk: menjelaskan perbedaan map dan filter
```

Pengajar berhak menanyakan ulang logika kode secara lisan.

---

## Penilaian

Setiap task dinilai maksimal **100 poin** dengan komponen umum:

| Komponen | Bobot |
| --- | --- |
| Kesesuaian output dan perilaku | 50 |
| Ketepatan konsep yang diuji | 20 |
| Kasus batas dan validasi | 15 |
| Kerapian kode | 10 |
| Dokumentasi/refleksi | 5 |

Nilai akhir adalah rata-rata 30 task, dengan **Task 30 (capstone) berbobot 2×**.

- Rubrik lengkap: [docs/rubrik-penilaian.md](docs/rubrik-penilaian.md)
- Panduan mengajar: [docs/panduan-pengajar.md](docs/panduan-pengajar.md)
- Glosarium: [docs/glosarium.md](docs/glosarium.md)

---

## Tips Belajar

- **Jalankan kode sering.** Jangan menulis 50 baris lalu baru menjalankan.
- **Baca pesan error dari bawah ke atas.** Baris yang disebut adalah lokasi masalah.
- **Gunakan `console.log` untuk melihat nilai.** Debugging adalah bagian dari belajar.
- **Ulangi task tanpa melihat catatan.** Jika bisa mengerjakan ulang dengan lancar, konsepnya sudah melekat.
- **Jangan takut salah.** Error adalah umpan balik, bukan kegagalan.

---

## Untuk Pengajar

Materi ini bisa dipakai apa adanya. Sebelum kelas:

1. Baca [docs/panduan-pengajar.md](docs/panduan-pengajar.md) untuk alur sesi dan kesalahan umum.
2. Siapkan solusi pribadi untuk setiap task; jangan membagikan jawaban ke siswa.
3. Uji setiap contoh output di environment kelas (Node dan browser).
4. Siapkan aturan penggunaan AI dan konsekuensi plagiarisme.

Setiap task sudah memiliki ekspektasi output yang eksplisit, sehingga pengajar dapat menilai secara objektif tanpa harus menebak maksud soal.

---

## FAQ

**Apakah harus menyelesaikan 30 task?**
Untuk kelas pemula, 30 task adalah jalur lengkap. Jika waktu terbatas, minimal selesaikan Level 1–2, lalu pilih task DOM dan capstone sebagai proyek.

**Berapa lama per task?**
Estimasi ada di setiap file. Jika lebih dari 2× estimasi, hentikan dan baca ulang konsepnya atau minta bantuan.

**Apakah boleh memakai `var`?**
Tidak untuk materi ini. Gunakan `const` atau `let`.

**Apakah boleh memakai library atau framework?**
Tidak. Semua task dirancang memakai JavaScript, HTML, dan CSS bawaan agar konsep dasarnya terlatih.

**Browser menampilkan error saat membuka file HTML?**
Untuk Task 29, jalankan server lokal (`npx serve .`). Task DOM lain bisa dibuka langsung, tetapi server lokal tetap disarankan.

**Di mana jawaban task?**
Materi ini sengaja tidak menyertakan jawaban siswa. Pengajar menyiapkan solusi sendiri dan membahasnya di kelas.
