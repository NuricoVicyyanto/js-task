# Glosarium JavaScript Beginner

Istilah-istilah yang muncul dalam 30 task, diurutkan alfabetis. Gunakan sebagai rujukan cepat saat membaca materi atau bertanya di kelas.

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
