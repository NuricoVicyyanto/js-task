# Task E08 — Authentication & RBAC

> **Level:** Expert · **Estimasi:** 5 jam · **Topik:** password hashing, `scrypt`, HMAC token, expiry, role-based access control

## Tujuan

Membangun autentikasi yang tidak menyimpan password plaintext dan otorisasi berbasis role, memakai hanya `node:crypto`.

## Studi Kasus

API Kopi Senja memiliki dua role: **kasir** (membuat pesanan) dan **admin** (mengelola menu dan pengguna). Login harus aman, token tidak boleh bisa dipalsukan, dan kasir tidak boleh mengakses endpoint admin.

## Yang Harus Dibuat (File)

```text
e08-auth/
├── auth.js
├── server.js
└── demo.js
```

## Password Hashing

Gunakan `scrypt` dari `node:crypto`.

Format penyimpanan:

```text
scrypt$<N>$<salt-base64url>$<hash-base64url>
```

- Salt acak minimal 16 byte.
- Panjang hash 64 byte.
- `N = 16384`, `r = 8`, `p = 1`.
- Verifikasi memakai `timingSafeEqual`.
- Jangan pernah menyimpan atau mencetak password asli.

Fungsi:

| Fungsi | Tugas |
| --- | --- |
| `hashPassword(password)` | menghasilkan string hash |
| `verifyPassword(password, tersimpan)` | `true`/`false`, constant-time |

## Token

Gunakan token bertanda tangan HMAC-SHA256, bukan JWT library.

Format:

```text
base64url(header).base64url(payload).base64url(signature)
```

- `header`: `{"alg":"HS256","typ":"JWT"}`.
- `payload`: `{ sub, role, iat, exp }`.
- `exp` dalam detik.
- Signature = HMAC-SHA256 atas `header.payload`.
- Verifikasi signature sebelum membaca payload.
- Tolak token kedaluwarsa dan token dengan `alg` selain `HS256`.
- Secret dibaca dari environment, bukan ditulis di kode.

Fungsi:

| Fungsi | Tugas |
| --- | --- |
| `buatToken(payload, secret, expiresInSec)` | token valid |
| `verifikasiToken(token, secret)` | payload atau melempar error |
| `requireRole(payload, role)` | melempar `403` jika role tidak cocok |

## Endpoint Demo

| Method | Path | Role |
| --- | --- | --- |
| POST | `/register` | publik |
| POST | `/login` | publik |
| GET | `/orders` | kasir/admin |
| GET | `/admin/users` | admin |

## Skenario Program

1. Register user `kasir` role `kasir`.
2. Register user `admin` role `admin`.
3. Login `kasir`, dapat token.
4. Akses `/orders` dengan token kasir → `200`.
5. Akses `/admin/users` dengan token kasir → `403`.
6. Verifikasi token kedaluwarsa → `401`.
7. Coba token dengan signature diubah → `401`.

## Ekspektasi Output

```text
Register kasir: 201
Login kasir: 200
Akses /orders: 200
Akses /admin/users: 403
Token kedaluwarsa: 401
Signature diubah: 401
Password tersimpan: scrypt$16384$...
```

Token dan salt tidak boleh dicetak lengkap.

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| Password benar | login sukses |
| Password salah | 401, pesan generik |
| Email/user tidak ada | 401, pesan sama dengan password salah |
| Token tanpa signature | 401 |
| Token `alg: none` | 401 |
| Token expired | 401 |
| Role kasir ke endpoint admin | 403 |
| Dua user dengan password sama | hash berbeda (salt acak) |

## Ketentuan

- Jangan memakai MD5/SHA-1 untuk password.
- Jangan membandingkan hash dengan `===`.
- Jangan menyimpan secret di source code.
- Jangan mengirim detail internal saat login gagal.
- Jangan mempercayai `role` dari body request; ambil dari token yang terverifikasi.
- Token harus memiliki masa berlaku.
- Jangan memakai library JWT eksternal.

## Checklist Sebelum Kumpul

- [ ] Password di-hash dengan scrypt + salt.
- [ ] Verifikasi memakai `timingSafeEqual`.
- [ ] Token ditandatangani HMAC-SHA256.
- [ ] Signature diverifikasi sebelum payload dipakai.
- [ ] Expiry dan alg dicek.
- [ ] RBAC menolak role yang tidak berhak.
- [ ] Output sesuai contoh.

## Bonus

1. Tambahkan refresh token dengan rotasi dan deteksi pemakaian ulang.
2. Tambahkan revokasi token (logout) memakai `jti`.
3. Tambahkan rate limit login per user/IP dan catat percobaan gagal.
