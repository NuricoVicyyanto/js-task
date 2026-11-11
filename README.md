# JavaScript Task Library — Beginner, Intermediate, Expert

Kumpulan **60 task JavaScript** yang disusun bertingkat dalam tiga folder level. Setiap task adalah studi kasus mandiri dengan cerita, instruksi, ekspektasi output, kasus uji, dan checklist penilaian.

Materi dirancang untuk kelas profesional: pengajar bisa langsung mengajar, dan siswa bisa langsung praktik tanpa starter code yang rumit.

---

## Pilih Level

| Level | Folder | Jumlah | Fokus | Estimasi |
| --- | --- | --- | --- | --- |
| **01 · Beginner** | [01-beginner/](./01-beginner/README.md) | 30 task | Fondasi JavaScript, DOM, async dasar | ±32 jam |
| **02 · Intermediate** | [02-intermediate/](./02-intermediate/README.md) | 15 task | Modul, class, error, testing, async, CLI, state | ±23 jam |
| **03 · Expert** | [03-expert/](./03-expert/README.md) | 15 task | Arsitektur, performa, keamanan, API, database, operasional | ±70 jam |

**Total:** 60 task, ±125 jam belajar.

### 01 — Beginner — untuk siapa?

Belum pernah atau baru mulai belajar JavaScript. Berakhir dengan aplikasi kasir browser sederhana.

→ [Masuk ke Level 01 — Beginner](./01-beginner/README.md)

### 02 — Intermediate — untuk siapa?

Sudah bisa membuat fungsi, mengolah array/objek, DOM, dan `fetch` dasar. Fokus pada kode yang bisa dirawat, diuji, dan dipecah menjadi modul.

→ [Masuk ke Level 02 — Intermediate](./02-intermediate/README.md)

### 03 — Expert — untuk siapa?

Sudah nyaman dengan ES Modules, testing, async, dan arsitektur dasar. Fokus pada sistem produksi: keamanan, database, observabilitas, dan rilis.

→ [Masuk ke Level 03 — Expert](./03-expert/README.md)

---

## Struktur Repo

```text
js-task/
├── README.md                  ← indeks utama
├── 01-beginner/
│   ├── README.md              ← peta 30 task + rencana kelas
│   └── 01-...md ... 30-...md
├── 02-intermediate/
│   ├── README.md              ← peta 15 task + rencana kelas
│   └── 01-...md ... 15-...md
├── 03-expert/
│   ├── README.md              ← peta 15 task + rencana kelas
│   └── 01-...md ... 15-...md
└── docs/
    ├── panduan-pengajar.md    ← alur kelas, kesalahan umum, etika
    ├── rubrik-penilaian.md    ← rubrik semua level
    └── glosarium.md           ← istilah JavaScript
```

Setiap file task memiliki bagian konsisten:

- Tujuan pembelajaran
- Studi kasus
- Yang harus dibuat
- Ketentuan
- Ekspektasi output
- Contoh kasus uji
- Checklist sebelum kumpul
- Bonus

---

## Cara Menggunakan Materi

1. Tentukan level sesuai prasyarat di README level.
2. Baca README level untuk melihat urutan task dan rencana sesi.
3. Buka task, baca dari **Studi Kasus** sampai **Ekspektasi Output**.
4. Buat file kerja sesuai nama yang diminta.
5. Jalankan, bandingkan dengan ekspektasi output, lalu centang checklist.
6. Kerjakan bonus hanya setelah bagian wajib selesai.
7. Jangan lompat level; konsep level berikutnya bergantung pada level sebelumnya.

## Prasyarat Ringkas

| Level | Prasyarat |
| --- | --- |
| Beginner | Bisa mengoperasikan komputer dan terminal dasar |
| Intermediate | Menguasai variabel, fungsi, array, objek, DOM, `fetch` dasar |
| Expert | Menguasai ES Modules, class, error, testing, async, arsitektur dasar |

Tool minimum:

- Node.js 18+ untuk beginner/intermediate.
- Node.js **22+** untuk expert (`node:sqlite`, test runner modern).
- Browser modern untuk task DOM.
- npm untuk beberapa task expert (Vite, lint, CI).
- Docker untuk capstone expert.

---

## Penilaian

Setiap task maksimal **100 poin**. Rubrik lengkap: [docs/rubrik-penilaian.md](docs/rubrik-penilaian.md).

| Level | Komponen Khas |
| --- | --- |
| Beginner | output, konsep, kasus batas, kerapian |
| Intermediate | output, pemisahan tanggung jawab, error, testing |
| Expert | arsitektur, keamanan, testing, operasional, dokumentasi |

Nilai akhir level dihitung dari rata-rata task, dengan capstone dihitung **2×**.

---

## Untuk Pengajar

- [Panduan Pengajar](docs/panduan-pengajar.md) — alur sesi, strategi per level, kesalahan umum, kebijakan AI.
- [Rubrik Penilaian](docs/rubrik-penilaian.md) — komponen nilai, form, konversi predikat.
- [Glosarium](docs/glosarium.md) — istilah dasar hingga lanjutan.

Materi ini sengaja **tidak menyertakan jawaban siswa**. Pengajar menyiapkan solusi sendiri dan membahasnya di kelas.

---

## Aturan Umum

1. Satu task, satu file/folder kerja dengan nama yang diminta.
2. Utamakan output yang benar sebelum memperindah kode.
3. Jangan memakai library/framework kecuali task menyebutkannya.
4. Jangan menyalin jawaban; diskusi boleh, menulis ulang sendiri wajib.
5. Cantumkan bantuan AI di komentar jika dipakai untuk belajar.
6. Kumpulkan file kerja beserta bonus sesuai instruksi pengajar.

---

## FAQ

**Apakah harus menyelesaikan semua 60 task?**
Tidak selalu. Untuk kelas singkat, pilih satu level. Untuk program intensif, gunakan Beginner → Intermediate, lalu Expert sebagai spesialisasi.

**Berapa lama per task?**
Estimasi ada di setiap file dan README level. Jika lebih dari 2× estimasi, berhenti dan baca ulang konsep atau minta bantuan.

**Apakah boleh memakai `var`?**
Tidak. Gunakan `const` atau `let`.

**Apakah boleh memakai framework?**
Tidak, kecuali task expert secara eksplisit meminta build tooling atau CI.

**Di mana jawaban task?**
Tidak disertakan. Pengajar menyiapkan solusi dan membahasnya di kelas.

**Apa bedanya Intermediate dan Expert?**
Intermediate fokus pada **kode yang bisa dirawat**. Expert fokus pada **sistem yang bisa dioperasikan**: keamanan, performa, database, observabilitas, dan rilis.
