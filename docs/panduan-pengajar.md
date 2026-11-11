# Panduan Pengajar — Kelas JavaScript Beginner "Kopi Senja"

Dokumen ini membantu pengajar menyampaikan 30 task secara terstruktur, menilai dengan konsisten, dan menangani kesalahan umum siswa.

---

## 1. Ringkasan Kelas

| Item | Keterangan |
| --- | --- |
| Nama kelas | JavaScript Beginner — Studi Kasus Kopi Senja |
| Jumlah task | 30 task bertingkat |
| Estimasi total | ±32 jam belajar |
| Format | 16 sesi × 120 menit, atau 8 sesi × 150 menit |
| Prasyarat siswa | Bisa mengoperasikan komputer dan terminal dasar |
| Tools | Node.js 18+, browser modern, VS Code |
| Model | 20% teori, 40% demonstrasi, 40% praktik |

Materi bersifat **project-based**: satu cerita (Kopi Senja) berkembang dari variabel sampai aplikasi kasir. Ini membantu siswa melihat hubungan antar konsep, bukan menghafal sintaks terpisah.

---

## 2. Hasil Belajar Akhir

Setelah menyelesaikan seluruh task, siswa mampu:

1. Menulis program JavaScript dengan variabel, kondisi, perulangan, dan fungsi.
2. Mengolah array dan objek, termasuk `map`, `filter`, `reduce`, dan `sort`.
3. Memvalidasi input serta menangani error sederhana.
4. Membuat halaman web interaktif dengan DOM.
5. Menyimpan data di browser dengan `localStorage`.
6. Menggunakan `fetch`, Promise, dan `async/await` untuk mengambil data.
7. Membangun aplikasi kasir sederhana dari nol.

---

## 3. Persiapan Sebelum Kelas

### Teknis

- [ ] Node.js terpasang di komputer pengajar dan siswa (`node --version`).
- [ ] Browser modern tersedia (Chrome/Edge/Firefox).
- [ ] Folder materi sudah dibagikan; siswa bisa membuka `tasks/`.
- [ ] Proyektor/layar untuk live coding sudah diuji.
- [ ] Server lokal untuk Task 29 sudah dicoba (`npx serve .`).
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
