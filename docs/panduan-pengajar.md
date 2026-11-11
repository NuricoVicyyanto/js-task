# Panduan Pengajar — Kelas JavaScript Beginner sampai Expert "Kopi Senja"

Dokumen ini membantu pengajar menyampaikan 60 task bertingkat, menilai dengan konsisten, dan menangani kesalahan umum siswa.

---

## 1. Ringkasan Kelas

| Level | Folder | Jumlah | Estimasi | Fokus |
| --- | --- | --- | --- | --- |
| 01 · Beginner | `01-beginner/` | 30 | ±32 jam | Fondasi, DOM, async dasar |
| 02 · Intermediate | `02-intermediate/` | 15 | ±23 jam | Modul, class, testing, CLI, state |
| 03 · Expert | `03-expert/` | 15 | ±70 jam | Arsitektur, keamanan, API, database, operasional |

| Item | Keterangan |
| --- | --- |
| Nama program | JavaScript Task Library — Studi Kasus Kopi Senja |
| Format | Sesi 120 menit; jumlah sesi menyesuaikan level |
| Prasyarat | Level Beginner: terminal dasar; Intermediate: fondasi JS; Expert: ES Modules + testing |
| Tools | Node.js 18+ (Expert: Node 22+), browser, VS Code, Git |
| Model | 20% teori, 40% demonstrasi, 40% praktik |

Materi bersifat **project-based**: satu cerita (Kopi Senja) berkembang dari variabel sampai layanan pesanan produksi. Ini membantu siswa melihat hubungan antar konsep, bukan menghafal sintaks terpisah.

---

## 2. Hasil Belajar Akhir

Setelah menyelesaikan seluruh level, siswa mampu:

1. Menulis program JavaScript dengan variabel, kondisi, perulangan, dan fungsi.
2. Mengolah array dan objek, termasuk `map`, `filter`, `reduce`, dan `sort`.
3. Memvalidasi input serta menangani error di beberapa lapisan.
4. Membuat halaman web interaktif dengan DOM dan `localStorage`.
5. Menggunakan `fetch`, Promise, dan `async/await` untuk mengambil data.
6. Memecah aplikasi menjadi modul, layer, dan komponen yang bisa diuji.
7. Menulis unit/integration test dan pipeline CI.
8. Membangun API, database transaksional, autentikasi, cache, dan SSE.
9. Menerapkan pertahanan keamanan dasar dan observability.
10. Mengoperasikan aplikasi lewat Docker dengan dokumentasi yang jelas.

---

## 3. Persiapan Sebelum Kelas

### Teknis

- [ ] Node.js terpasang di komputer pengajar dan siswa (`node --version`).
- [ ] Untuk Intermediate/Expert: Node.js **22+** dan npm tersedia.
- [ ] Browser modern tersedia (Chrome/Edge/Firefox).
- [ ] Folder materi sudah dibagikan; siswa membuka `01-beginner/`, `02-intermediate/`, atau `03-expert/`.
- [ ] Proyektor/layar untuk live coding sudah diuji.
- [ ] Server lokal untuk Task 29 sudah dicoba (`npx serve .`).
- [ ] Docker tersedia untuk capstone expert (E15).
- [ ] Repository latihan dan akses GitHub Actions sudah diuji (E12).
- [ ] Contoh solusi pribadi sudah disiapkan, tetapi **tidak dibagikan**.
- [ ] Koneksi internet cadangan untuk dokumentasi MDN.

### Non-teknis

- [ ] Aturan kelas dan kebijakan AI dijelaskan di sesi pertama.
- [ ] Mekanisme pengumpulan tugas ditentukan (folder, LMS, atau Git).
- [ ] Rubrik penilaian dibagikan sejak awal.
- [ ] Grup komunikasi untuk pertanyaan di luar kelas disiapkan.

---

## 4. Alur Sesi 120 Menit

| Tahap | Durasi | Aktivitas |
| --- | --- | --- |
| Pembukaan | 10 menit | Review task sebelumnya, tanya jawab singkat |
| Hook | 10 menit | Tunjukkan masalah nyata yang akan diselesaikan |
| Demonstrasi | 25 menit | Live coding konsep baru, siswa hanya mengamati |
| Praktik terbimbing | 25 menit | Siswa mengetik ulang contoh kecil bersama |
| Praktik mandiri | 35 menit | Siswa mengerjakan task |
| Review & penutup | 15 menit | Bahas 2–3 solusi, error umum, preview task berikutnya |

**Aturan live coding:** jangan mengetik terlalu cepat. Ucapkan apa yang sedang dilakukan. Saat error muncul, jangan langsung memperbaiki diam-diam — tunjukkan cara membaca pesan error.

---

## 5. Strategi per Level

### Level 1 — Fondasi (Task 01–08)

Tujuan: membangun rasa percaya diri dengan output yang terlihat.

- Mulai dari satu file `task-01.js`, bukan struktur folder rumit.
- Biasakan membaca output di terminal.
- Untuk percabangan, gunakan tabel kebenaran sederhana di papan.
- Untuk perulangan, minta siswa menulis 3 iterasi pertama di kertas sebelum menulis kode.
- Jangan memperkenalkan `function` sebelum Task 07; gunakan pengulangan kode secara wajar agar siswa merasakan manfaat fungsi.

**Kesalahan yang harus diantisipasi:**

| Kesalahan | Cara menjelaskan |
| --- | --- |
| `=` dipakai untuk membandingkan | Tunjukkan `if (x = 5)` selalu truthy; tekankan `===` |
| `"18000" + 1000` menghasilkan `"180001000"` | Tunjukkan `typeof` kedua nilai |
| Lupa `return` | Bandingkan fungsi yang mengembalikan `undefined` dengan yang mengembalikan angka |
| Loop tidak berhenti | Minta cetak nilai penghitung setiap iterasi |
| Indeks array mulai 1 | Tunjukkan array 3 elemen dan indeks 0,1,2 |

### Level 2 — Array & Objek (Task 09–15)

Tujuan: berpindah dari satu nilai ke kumpulan data.

- Gunakan analogi: array = daftar antrean, objek = kartu identitas.
- Untuk `map`, tekankan “mengubah setiap item”; untuk `filter`, “memilih item yang lolos syarat”.
- Saat mengajarkan `reduce`, mulai dari menjumlahkan angka sederhana, baru array of objects.
- Tunjukkan efek mutasi dengan mencetak array sebelum dan sesudah `sort`/`push`.
- Untuk data bersarang, gambar struktur di papan sebelum menulis kode.

**Latihan diagnostik:** minta siswa memprediksi output `map` vs `filter` sebelum menjalankan.

### Level 3 — Data & Logika (Task 16–23)

Tujuan: menulis kode yang lebih tahan terhadap input aneh.

- Ajarkan membaca dokumentasi MDN untuk method baru.
- Untuk `this`, mulai dari satu objek dan satu method; hindari contoh class.
- Untuk JSON, tunjukkan perbedaan objek dan string JSON secara visual.
- Untuk error handling, mulai dari `throw` sederhana, lalu `try/catch`.
- Untuk regex, jangan menghafal; gunakan tabel pola dan uji satu per satu.

### Level 4 — DOM (Task 24–27)

Tujuan: menghubungkan data dengan antarmuka.

- Selalu buka DevTools saat mengajar.
- Tekankan urutan: elemen HTML harus ada sebelum script dijalankan.
- Larang `innerHTML` untuk data pengguna; jelaskan risiko injeksi.
- Ajarkan `textContent` sebagai default.
- Untuk event, cetak `event.target` agar siswa paham apa yang diklik.
- Saat debugging, gunakan `console.log` pada nilai input, bukan langsung pada hasil akhir.

### Level 5 — Async & Capstone (Task 28–30)

Tujuan: memahami proses yang tidak selesai seketika.

- Gunakan analogi: memesan kopi di kasir, menerima nomor pesanan, lalu dipanggil saat siap.
- Tunjukkan perbedaan output sebelum dan sesudah `await`.
- Untuk `fetch`, jelaskan status HTTP dan `response.ok`.
- Saat capstone, jangan memberi solusi utuh; gunakan sesi konsultasi per fitur.
- Minta siswa mendemokan aplikasinya, bukan hanya mengumpulkan file.

### Level Intermediate (I01–I15)

Tujuan: berpindah dari “kode yang berjalan” ke “kode yang bisa dirawat”.

- Mulai dari satu file, lalu refaktor ke modul; tunjukkan rasa sakit sebelum solusi.
- Untuk closure, gunakan analogi “kotak privat” yang menyimpan state.
- Untuk class, bandingkan dengan object + function sebelum `extends`.
- Untuk error, ajarkan perbedaan error yang bisa di-retry dan yang tidak.
- Untuk testing, tulis satu test yang gagal terlebih dahulu, lalu perbaiki kode.
- Untuk CLI, selalu uji jalur sukses dan jalur error (file hilang, argumen salah).
- Untuk state DOM, gambar alur `state → render → event → state`.

**Kesalahan umum Intermediate:**

| Kesalahan | Cara menjelaskan |
| --- | --- |
| `import` tanpa ekstensi `.js` | Tunjukkan error resolusi modul |
| Closure dipakai untuk global state | Tunjukkan dua instance yang saling bocor |
| `this` hilang saat method dipisah | Bandingkan `obj.method` vs `const f = obj.method` |
| Retry mengulang error validasi | Minta siswa mengklasifikasikan error |
| `Promise.all` menggagalkan semua | Ganti ke `allSettled` dan bandingkan |
| Test bergantung waktu nyata | Injeksi clock atau mock timer |
| CLI menulis file langsung | Tunjukkan risiko file setengah jadi |
| State DOM diubah di banyak tempat | Hitung sumber kebenaran |

### Level Expert (E01–E15)

Tujuan: membangun sistem yang aman, terukur, dan bisa dioperasikan.

- Ajarkan **membaca requirement non-fungsional**, bukan hanya fitur.
- Untuk arsitektur, mulai dari satu service yang sulit diuji, lalu pecah layer.
- Untuk performa, larang optimasi tanpa baseline; minta grafik sebelum/sesudah.
- Untuk keamanan, demonya harus di lingkungan lokal dan data palsu.
- Untuk database, tekankan transaksi dan rollback, bukan hanya query berhasil.
- Untuk API, review status code dan error envelope seperti kontrak.
- Untuk observability, tunjukkan satu request yang bisa dilacak dari log ke metrics.
- Untuk CI, sengaja buat pipeline merah, lalu perbaiki.
- Untuk capstone, nilai bukti (test, load test, log, Docker), bukan klaim.

**Kesalahan umum Expert:**

| Kesalahan | Cara menjelaskan |
| --- | --- |
| Layer domain mengimpor `fs`/`http` | Tunjukkan dependency graph dan aturan layer |
| Worker mengirim seluruh data | Hitung memori dan gunakan chunk |
| Benchmark tanpa warm-up | Tunjukkan variasi hasil |
| Test integration memakai port tetap | Gunakan port `0` dan cleanup |
| SQL string concatenation | Tunjukkan payload dan prepared statement |
| Token disimpan/ dicetak | Audit log dan response |
| Cache/rate limit tanpa batas | Tunjukkan pertumbuhan memori |
| Metrics memakai ID sebagai label | Jelaskan cardinality |
| CI memakai `npm install` | Bandingkan reproducibility `npm ci` |
| Docker berjalan sebagai root | Tunjukkan `USER` dan least privilege |

---

## 6. Cara Memberi Hint Tanpa Memberi Jawaban

Gunakan tangga bantuan berikut secara berurutan:

1. **Minta siswa membaca ulang error.** “Baris berapa yang disebut? Apa jenis errornya?”
2. **Minta menjelaskan tujuan kode.** “Fungsi ini seharusnya mengembalikan apa?”
3. **Minta mencetak nilai antara.** “Coba `console.log` sebelum baris yang error.”
4. **Beri pertanyaan penuntun.** “Kalau `items` kosong, apa yang terjadi pada `items[0]`?”
5. **Tunjukkan potongan konsep**, bukan solusi penuh. Contoh: “Gunakan `Array.isArray` untuk memeriksa tipe.”
6. **Baru tunjukkan solusi** jika siswa sudah mencoba minimal dua pendekatan dan tetap buntu.

Hindari langsung mengetikkan jawaban di komputer siswa. Jika terpaksa, ketik di editor pengajar dan jelaskan setiap baris.

---

## 7. Penilaian dan Umpan Balik

Gunakan [rubrik-penilaian.md](rubrik-penilaian.md) sebagai acuan. Prinsipnya:

- **Objektif:** bandingkan dengan ekspektasi output di README task.
- **Konsisten:** gunakan komponen bobot yang sama untuk semua siswa.
- **Spesifik:** sebut perilaku yang sudah benar dan yang perlu diperbaiki.
- **Tindak lanjut:** setiap nilai di bawah 70 harus disertai satu langkah perbaikan yang jelas.

### Contoh umpan balik yang baik

> “Perhitungan diskon dan total sudah tepat, termasuk saat subtotal 0. Namun validasi nama belum menangani string berisi spasi. Coba gunakan `trim()` sebelum memeriksa panjang string, lalu uji dengan `"   "`.”

### Contoh umpan balik yang kurang membantu

> “Kodenya kurang rapi. Perbaiki.”

---

## 8. Diferensiasi

### Siswa yang cepat

- Berikan bonus di akhir task.
- Minta mereka menulis ulang solusi dengan gaya berbeda (misalnya `for` menjadi `reduce`).
- Jadikan mereka peer mentor, tetapi tetap wajib mengerjakan task sendiri.

### Siswa yang tertinggal

- Kurangi target: fokus pada bagian wajib, lewati bonus.
- Pecah task menjadi langkah lebih kecil.
- Beri contoh satu baris, lalu minta melanjutkan.
- Jadwalkan sesi tambahan untuk Level 1–2 sebelum masuk DOM.

### Siswa tanpa laptop pribadi

- Sediakan komputer kelas atau pasangan belajar.
- Pastikan file tersimpan di folder yang bisa diakses bergantian.
- Untuk task browser, gunakan browser portabel jika perlu.

---

## 9. Integritas Akademik dan AI

Aturan yang disarankan:

1. AI boleh untuk **menjelaskan konsep** dan **membantu debugging**.
2. AI tidak boleh menghasilkan seluruh solusi tanpa pemahaman.
3. Siswa wajib bisa menjelaskan kode mereka secara lisan.
4. Cantumkan bantuan AI di komentar file.
5. Plagiarisme antar siswa diberi sanksi sesuai kebijakan kelas.

Saat mencurigai jawaban hasil AI, ajukan pertanyaan seperti:

- “Mengapa kamu memilih `reduce` di sini?”
- “Apa yang terjadi jika array kosong?”
- “Coba ubah satu nilai dan prediksi outputnya.”

Jika siswa tidak bisa menjelaskan, minta mengerjakan ulang bagian tersebut secara terbimbing.

---

## 10. Troubleshooting Teknis

| Masalah | Penyebab umum | Solusi |
| --- | --- | --- |
| `node: command not found` | Node belum terpasang / PATH salah | Install Node LTS, buka ulang terminal |
| `Cannot find module` | Menjalankan dari folder salah | Jalankan dari folder file berada |
| `SyntaxError: Unexpected token` | Kurung/kurawal tidak seimbang | Cek pasangan `{}`, `()`, `[]` |
| `ReferenceError: x is not defined` | Variabel di luar scope / salah ketik | Cek nama dan posisi deklarasi |
| `TypeError: Cannot read properties of undefined` | Data belum ada / salah akses | Cetak objek sebelum mengakses properti |
| Halaman DOM kosong | Script berjalan sebelum elemen ada | Letakkan `<script>` di akhir `body` atau gunakan `DOMContentLoaded` |
| `fetch` gagal di `file://` | Browser memblokir request lokal | Jalankan `npx serve .` |
| `localStorage` tidak menyimpan | Menyimpan objek tanpa `JSON.stringify` | Simpan string, parse saat membaca |
| Output `NaN` | Operasi pada `undefined`/string non-angka | Cek `typeof` dan konversi dengan `Number()` |
| `Cannot use import statement outside a module` | `package.json` belum `"type": "module"` | Tambahkan `type`, atau pakai ekstensi `.mjs` |
| `ERR_MODULE_NOT_FOUND` | Import tanpa `.js` atau path salah | Sertakan ekstensi dan cek path relatif |
| `node:sqlite` tidak ditemukan | Node < 22 | Upgrade Node ke 22+ |
| Worker tidak pernah selesai | `terminate`/pesan error tidak ditangani | Pasang handler `error` dan `exit` |
| Port `EADDRINUSE` | Server lama masih berjalan | Hentikan proses atau pakai port `0` di test |
| `fetch` gagal ke localhost | Server belum jalan / URL salah | Jalankan server, cek base URL |
| Docker build lambat | Cache layer tidak optimal | Copy `package*.json` sebelum source |
| Pipeline CI hijau padahal test gagal | `continue-on-error` atau script salah | Hapus pengecualian, cek exit code |

---

## 11. Checklist Mengajar per Sesi

- [ ] Tujuan sesi ditulis di papan.
- [ ] Contoh kecil sudah diuji sebelum kelas.
- [ ] Siswa menjalankan minimal satu kode sendiri.
- [ ] Ada sesi membaca error bersama.
- [ ] Ada review satu solusi siswa (dengan izin).
- [ ] Task berikutnya sudah diperkenalkan.
- [ ] Siswa tahu apa yang harus dikumpulkan.

---

## 12. Setelah Kelas

- Kumpulkan tugas dan nilai memakai rubrik.
- Catat konsep yang paling sering salah untuk sesi remedial.
- Minta siswa menulis satu refleksi singkat: “Konsep yang masih sulit dan satu hal yang sudah kupahami.”
- Simpan solusi terbaik (dengan izin siswa) sebagai contoh untuk kelas berikutnya.
- Perbarui materi jika ada instruksi yang membingungkan.
