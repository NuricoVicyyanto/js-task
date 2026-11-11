# Glosarium JavaScript — Beginner sampai Expert

Istilah-istilah yang muncul dalam 60 task, diurutkan alfabetis. Bagian pertama untuk fondasi; bagian kedua untuk level intermediate dan expert.

| Istilah | Arti | Contoh |
| --- | --- | --- |
| **Argument** | Nilai yang dikirim saat memanggil fungsi. | `hitungTotal(18000, 2)` → `18000` dan `2` adalah argument. |
| **Array** | Kumpulan nilai berurutan yang diakses dengan indeks mulai dari 0. | `const menu = ["Espresso", "Latte"]` |
| **Array of objects** | Array yang setiap elemennya berupa objek. | `[{ nama: "Latte", harga: 24000 }]` |
| **Arrow function** | Bentuk ringkas fungsi dengan `=>`. Tidak punya `this` sendiri. | `const kali = (a, b) => a * b;` |
| **Async/await** | Cara menulis kode asynchronous agar terlihat seperti berurutan. | `const data = await response.json();` |
| **Boolean** | Tipe data dengan dua nilai: `true` atau `false`. | `const tersedia = true;` |
| **Callback** | Fungsi yang dikirim sebagai argument dan dipanggil setelah proses selesai. | `setTimeout(() => console.log("siap"), 1000)` |
| **Chaining** | Memanggil beberapa method berurutan pada hasil sebelumnya. | `menu.filter(...).map(...)` |
| **Comparison operator** | Operator pembanding: `===`, `!==`, `>`, `<`, `>=`, `<=`. | `if (total >= 100000) { ... }` |
| **Const** | Deklarasi variabel yang tidak boleh di-reassign. | `const pajak = 0.11;` |
| **DOM** | Representasi halaman HTML yang bisa dibaca dan diubah JavaScript. | `document.querySelector("#total")` |
| **Destructuring** | Mengambil beberapa nilai dari array/objek dalam satu deklarasi. | `const { nama, harga } = menu;` |
| **Event listener** | Fungsi yang menunggu dan merespons event tertentu. | `form.addEventListener("submit", handler)` |
| **Fetch** | API browser untuk mengambil data dari URL. | `const res = await fetch("menu.json");` |
| **Filter** | Method array untuk memilih elemen yang lolos kondisi. | `menu.filter((m) => m.tersedia)` |
| **Function** | Blok kode yang bisa dipanggil berulang, bisa menerima parameter dan mengembalikan nilai. | `function hitungPajak(subtotal) { return subtotal * 0.11; }` |
| **Global scope** | Area di luar semua fungsi; variabel global bisa diakses dari mana saja. | `const namaToko = "Kopi Senja";` |
| **Immutability** | Prinsip tidak mengubah data asli; perubahan menghasilkan salinan baru. | `const baru = { ...lama, status: "diproses" };` |
| **Index** | Posisi elemen array, dimulai dari 0. | `menu[0]` adalah elemen pertama. |
| **InnerHTML** | Properti untuk mengisi HTML; berisiko untuk data pengguna. | Hindari: `el.innerHTML = nama`; gunakan `textContent`. |
| **JSON** | Format teks untuk pertukaran data, mirip objek tetapi key memakai kutip ganda. | `{"nama":"Latte","harga":24000}` |
| **Let** | Deklarasi variabel yang nilainya boleh berubah. | `let total = 0;` |
| **localStorage** | Penyimpanan key-value di browser yang bertahan setelah refresh. | `localStorage.setItem("keranjang", "[]")` |
| **Map** | Struktur key-value yang bisa memakai key non-string. | `new Map([["Minuman", 524000]])` |
| **Method** | Fungsi yang menjadi properti objek. | `keranjang.total()` |
| **Mutation** | Mengubah data asli secara langsung. | `array.push("Latte")` mengubah array asli. |
| **NaN** | “Not a Number”, hasil operasi angka yang tidak valid. | `Number("kopi")` → `NaN` |
| **Null** | Nilai yang sengaja kosong. | `let voucher = null;` |
| **Object** | Kumpulan pasangan key-value untuk menyimpan data terstruktur. | `{ nama: "Latte", harga: 24000 }` |
| **Parameter** | Variabel yang dideklarasikan di fungsi untuk menerima nilai. | `function tambah(nama, harga) { ... }` |
| **Promise** | Objek yang mewakili hasil proses asynchronous di masa depan. | `fetch(url).then((res) => res.json())` |
| **Property** | Pasangan key-value di dalam objek. | `menu.harga` |
| **Reduce** | Method array untuk menggabungkan semua elemen menjadi satu nilai. | `items.reduce((t, i) => t + i.harga, 0)` |
| **Return** | Mengembalikan nilai dari fungsi dan menghentikan eksekusi fungsi. | `return subtotal + pajak;` |
| **Scope** | Batas area tempat variabel bisa diakses. | Variabel di dalam fungsi tidak bisa diakses dari luar. |
| **Set** | Kumpulan nilai unik tanpa duplikat. | `new Set(["Minuman", "Minuman"])` → 1 nilai |
| **Sort** | Method array untuk mengurutkan; tanpa salinan, array asli ikut berubah. | `[...menu].sort((a, b) => a.harga - b.harga)` |
| **Spread** | Sintaks `...` untuk menyalin atau menggabungkan array/objek. | `{ ...pesanan, status: "baru" }` |
| **String** | Tipe data teks. | `const nama = "Sakti";` |
| **Template literal** | String dengan backtick yang bisa menyisipkan variabel `${...}`. | `` `Total: Rp${total}` `` |
| **TextContent** | Properti untuk mengisi teks biasa pada elemen; aman dari interpretasi HTML. | `el.textContent = nama;` |
| **Typeof** | Operator untuk memeriksa tipe data. | `typeof 20` → `"number"` |
| **Undefined** | Nilai default variabel yang belum diberi nilai. | `let x; // undefined` |
| **Variable** | Nama untuk menyimpan nilai. | `const harga = 18000;` |
| **While** | Perulangan yang berjalan selama kondisi bernilai benar. | `while (i >= 1) { ... }` |

---

## Istilah yang Sering Tertukar

| Pasangan | Perbedaan Singkat |
| --- | --- |
| `let` vs `const` | `let` boleh diubah; `const` tidak boleh di-reassign. |
| `==` vs `===` | `==` melakukan konversi tipe; `===` membandingkan nilai dan tipe. Selalu gunakan `===`. |
| `null` vs `undefined` | `null` sengaja dikosongkan; `undefined` belum diberi nilai. |
| `map` vs `filter` | `map` mengubah setiap elemen; `filter` memilih sebagian elemen. |
| `map` vs `forEach` | `map` mengembalikan array baru; `forEach` tidak mengembalikan apa pun. |
| `push` vs `unshift` | `push` menambah di akhir; `unshift` menambah di awal. |
| `shift` vs `pop` | `shift` menghapus dari awal; `pop` menghapus dari akhir. |
| `slice` vs `splice` | `slice` menyalin sebagian array; `splice` mengubah array asli. |
| `innerHTML` vs `textContent` | `innerHTML` membaca HTML; `textContent` hanya teks. Untuk data pengguna, gunakan `textContent`. |
| `localStorage` vs variabel | `localStorage` bertahan setelah refresh; variabel hilang saat halaman dimuat ulang. |
| Callback vs Promise | Callback adalah fungsi yang dipanggil; Promise adalah objek yang mewakili hasil nanti. |
| `async` vs `await` | `async` menandai fungsi; `await` menunggu Promise di dalam fungsi async. |

---

## Istilah Intermediate & Expert

| Istilah | Arti | Contoh |
| --- | --- | --- |
| **AbortSignal** | Sinyal untuk membatalkan operasi async seperti `fetch`. | `fetch(url, { signal: AbortSignal.timeout(2000) })` |
| **Adapter** | Implementasi konkret dari sebuah port/interface. | `InMemoryMenuRepository` |
| **Artifact** | Hasil build yang disimpan/diunggah CI. | `app-dist.zip` |
| **Backoff** | Jeda yang bertambah antar percobaan retry. | `delay * 2 ** attempt` |
| **Backpressure** | Kendali agar produsen tidak membanjiri konsumen. | Antrean worker maksimal 4 chunk |
| **Bundling** | Menggabungkan modul menjadi file produksi. | `vite build` |
| **Cardinality** | Jumlah kombinasi unik label metrik. | ID user sebagai label = cardinality tinggi |
| **CI/CD** | Otomatisasi integrasi dan pengiriman kode. | GitHub Actions |
| **Closure** | Fungsi yang mengingat variabel dari scope pembuatnya. | `buatPenghitung()` |
| **Code splitting** | Memecah bundle agar dimuat sesuai kebutuhan. | `import("./laporan.js")` |
| **Composition root** | Tempat merangkai semua dependency aplikasi. | `composition.js` |
| **Coverage** | Persentase kode yang dijalankan test. | `coverage line 87%` |
| **Curry** | Mengubah fungsi multi-argument menjadi rantai fungsi. | `fn(1)(2)(3)` |
| **Dependency injection** | Memberikan dependency dari luar, bukan membuat di dalam. | `createService({ repo })` |
| **Docker** | Paket aplikasi beserta environment-nya. | `docker build -t kopi .` |
| **ES Module** | Sistem modul bawaan JavaScript. | `import { menu } from "./menu.js"` |
| **Event loop** | Mekanisme Node/browser menjalankan tugas async. | Heartbeat tetap jalan saat worker aktif |
| **Graceful shutdown** | Menutup aplikasi tanpa memutus request aktif. | Tangani `SIGTERM` |
| **Health check** | Endpoint status hidup/siap melayani. | `/health/ready` |
| **Higher-order function** | Fungsi yang menerima/mengembalikan fungsi. | `map(fn)`, `buatAturanDiskon()` |
| **Histogram** | Metrik distribusi nilai (misalnya durasi). | `request_duration_ms_bucket` |
| **HMAC** | Tanda tangan pesan dengan secret bersama. | Token auth HS256 |
| **Immutability** | Tidak mengubah data asli; membuat salinan baru. | `{ ...order, status: "baru" }` |
| **Integration test** | Test beberapa komponen bersama, misalnya HTTP + DB. | Test endpoint dengan server nyata |
| **LRU** | Least Recently Used; evict item paling lama diakses. | Cache maksimal 100 item |
| **Memoization** | Menyimpan hasil fungsi berdasarkan argument. | `memoize(fib)` |
| **Metrics** | Angka terukur tentang perilaku sistem. | `http_requests_total` |
| **Migration** | Perubahan skema database yang terurut. | `001_init.sql` |
| **Mock** | Pengganti dependency untuk test. | Repo palsu yang melempar error |
| **Named capture group** | Grup regex dengan nama. | `(?<nama>.+?)` |
| **node:sqlite** | Modul SQLite bawaan Node.js 22+. | `new DatabaseSync("toko.db")` |
| **OpenAPI** | Spesifikasi kontrak REST API. | `openapi.yaml` |
| **p95** | Nilai yang 95% request berada di bawahnya. | p95 latency 80 ms |
| **Pipe** | Komposisi fungsi kiri ke kanan. | `pipe(f, g)(x)` |
| **Port** | Kontrak/interface yang dipakai service. | `MenuRepository` |
| **Prepared statement** | Query berparameter yang aman dari SQL injection. | `db.prepare("... WHERE id = ?")` |
| **Prototype pollution** | Serangan lewat key `__proto__`/`constructor`. | `safeMerge` menolak key tersebut |
| **Pure function** | Output hanya bergantung input, tanpa efek samping. | `hitungPajak(subtotal)` |
| **Rate limiting** | Membatasi jumlah request per key/waktu. | 5 login per menit |
| **RBAC** | Otorisasi berdasarkan role. | `kasir`, `admin` |
| **Repository** | Abstraksi akses data. | `orderRepo.save(order)` |
| **Retry** | Mengulang operasi yang gagal sementara. | `withRetry(fn, { maxAttempts: 3 })` |
| **scrypt** | Fungsi hash password yang lambat dan berbasis memori. | `scrypt$16384$...` |
| **SQL injection** | Injeksi SQL lewat input yang tidak divalidasi. | `' OR 1=1 --` |
| **SSE** | Server-Sent Events; push satu arah via HTTP. | `text/event-stream` |
| **Structured logging** | Log JSON dengan field konsisten. | `{"level":"info","requestId":"..."}` |
| **Test isolation** | Test tidak saling bergantung state. | Port `0`, fixture baru |
| **Transaction** | Sekumpulan operasi database atomik. | `BEGIN` / `COMMIT` / `ROLLBACK` |
| **Tree shaking** | Membuang kode yang tidak dipakai saat build. | Import hanya fungsi yang perlu |
| **TTL** | Time To Live; masa berlaku cache. | Cache menu 30 detik |
| **Worker thread** | Thread terpisah untuk pekerjaan CPU-bound. | `new Worker("./worker.js")` |
| **XSS** | Injeksi script lewat input pengguna. | Escape `<script>` |
