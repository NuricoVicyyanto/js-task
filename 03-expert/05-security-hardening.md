# Task E05 — Security Hardening

> **Level:** Expert · **Estimasi:** 4 jam · **Topik:** XSS, prototype pollution, SQL injection, secret redaction, security headers

## Tujuan

Mengaudit kode yang rentan dan memperbaikinya dengan pertahanan berlapis. Fokus pada kelas kerentanan yang paling sering muncul di aplikasi JavaScript, bukan pada teori kriptografi.

## Studi Kasus

Aplikasi kasir Kopi Senja menerima nama pelanggan, catatan pesanan, dan filter dari pengguna. Seorang auditor menemukan empat masalah:

1. Nama pelanggan dirender sebagai HTML → **XSS**.
2. Objek konfigurasi digabung tanpa filter → **prototype pollution**.
3. Query database disusun dengan string concatenation → **SQL injection**.
4. Password dan token masuk ke log → **kebocoran secret**.

Tim meminta perbaikan dan bukti bahwa serangan tidak lagi berhasil.

## Yang Harus Dibuat (File)

```text
e05-security/
├── sanitize.js
├── safe-merge.js
├── db.js
├── logger.js
├── headers.js
└── demo.js
```

## 1. XSS — `escapeHtml(teks)`

Escape minimal lima karakter:

| Karakter | Ganti |
| --- | --- |
| `&` | `&amp;` |
| `<` | `&lt;` |
| `>` | `&gt;` |
| `"` | `&quot;` |
| `'` | `&#39;` |

Contoh:

```text
Input : <script>alert("x")</script>
Output: &lt;script&gt;alert(&quot;x&quot;)&lt;/script&gt;
```

Aturan: escape **saat konteks HTML**, bukan sekali di awal lalu dipakai untuk semua konteks. Jangan mengandalkan `replace("<", "")`.

## 2. Prototype Pollution — `safeMerge(target, source)`

- Tolak key `__proto__`, `constructor`, dan `prototype` di semua level.
- Lakukan pengecekan rekursif untuk objek bersarang.
- Jangan memakai `Object.assign` mentah pada input pengguna.
- Buktikan `({}).polluted` tetap `undefined` setelah merge berbahaya.

Uji payload:

```js
const jahat = JSON.parse('{"__proto__":{"polluted":"ya"},"nama":"Nadia"}');
safeMerge({}, jahat);
```

## 3. SQL Injection — `db.js`

Gunakan `node:sqlite` (Node.js 22+) dan **prepared statement**.

Tabel:

```sql
CREATE TABLE pengguna (id INTEGER PRIMARY KEY, nama TEXT NOT NULL);
INSERT INTO pengguna (nama) VALUES ('Nadia'), ('Sakti');
```

Fungsi `cariPengguna(nama)`:

- Salah: `db.prepare("SELECT * FROM pengguna WHERE nama = '" + nama + "'")`.
- Benar: `db.prepare("SELECT * FROM pengguna WHERE nama = ?").all(nama)`.

Uji dengan `nama = "x' OR '1'='1"`; hasil harus `0`, dan tabel tetap ada.

## 4. Secret Redaction — `logger.js`

`logAman(data)` mencetak JSON dengan field sensitif diganti `"***"`:

- `password`, `passwordHash`, `token`, `authorization`, `cookie`.

Contoh output:

```json
{"user":"nadia","password":"***","token":"***"}
```

Jangan memodifikasi objek asli.

## 5. Security Headers — `headers.js`

`buatHeaderKeamanan()` mengembalikan:

```text
Content-Security-Policy: default-src 'self'; script-src 'self'
X-Content-Type-Options: nosniff
Referrer-Policy: no-referrer
X-Frame-Options: DENY
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

`Strict-Transport-Security` hanya ditambahkan jika request melalui HTTPS.

## Ekspektasi Output

```text
XSS: &lt;script&gt;alert(&quot;x&quot;)&lt;/script&gt;
Prototype pollution: false
SQL injection: 0 hasil
Tabel pengguna masih ada: true
Log: {"user":"nadia","password":"***","token":"***"}
CSP: default-src 'self'; script-src 'self'
```

## Kasus Uji

| Serangan | Hasil yang diharapkan |
| --- | --- |
| `<img src=x onerror=alert(1)>` | seluruh tag ter-escape |
| `__proto__` di root | ditolak |
| `constructor.prototype` bersarang | ditolak |
| `' OR 1=1 --` | tidak mengembalikan semua baris |
| `'; DROP TABLE pengguna; --` | tabel tetap ada |
| Password di nested object | tetap diredaksi |
| Input `null`/number | tidak crash |

## Ketentuan

- Jangan menulis library kriptografi sendiri.
- Jangan memakai `eval`, `new Function`, atau `innerHTML` untuk data pengguna.
- Prepared statement wajib untuk semua query berparameter.
- Redaksi harus rekursif dan tidak mengubah input.
- Header tidak boleh mengandung nilai dinamis dari pengguna.
- Demonstrasi serangan harus aman dijalankan lokal.

## Checklist Sebelum Kumpul

- [ ] XSS ter-escape di konteks HTML.
- [ ] Prototype pollution dicegah di semua level.
- [ ] Query memakai prepared statement.
- [ ] Tabel tetap utuh setelah payload SQL injection.
- [ ] Secret diredaksi tanpa mengubah objek asli.
- [ ] Header keamanan lengkap.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Rancang token CSRF untuk form berbasis cookie.
2. Tambahkan validasi allowlist untuk nama file upload.
3. Jelaskan perbedaan encoding HTML, atribut, URL, dan JavaScript.
