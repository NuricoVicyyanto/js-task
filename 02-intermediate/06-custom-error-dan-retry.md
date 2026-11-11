# Task I06 — Custom Error & Retry

> **Level:** Intermediate · **Estimasi:** 75 menit · **Topik:** `class extends Error`, `cause`, error code, retry, exponential backoff

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Membuat class error khusus dengan kode dan status.
2. Membedakan error yang boleh di-retry dan yang tidak.
3. Mengimplementasikan retry dengan jeda yang aman.

## Studi Kasus

Layanan pembayaran Kopi Senja kadang mengalami gangguan sementara. Kasir tidak boleh langsung menyerah pada gangguan sementara, tetapi juga tidak boleh mengulang error validasi seperti nominal negatif. Buat mekanisme retry yang hanya mengulang error tertentu.

## Yang Harus Dibuat

Buat file **`task-i06.js`** dengan:

### Error class

```js
class AppError extends Error {
  constructor(message, { code = "APP_ERROR", status = 500, retryable = false, cause } = {}) {
    super(message, { cause });
    this.name = "AppError";
    this.code = code;
    this.status = status;
    this.retryable = retryable;
  }
}

class ValidasiError extends AppError {
  // code "VALIDASI", status 400, retryable false
}
```

### `tidur(ms)`

Mengembalikan Promise yang selesai setelah `ms` milidetik.

### `withRetry(fn, { maxAttempts = 3, delayMs = 20 } = {})`

- Memanggil `fn()`.
- Jika sukses, kembalikan hasil.
- Jika error `retryable`, tunggu `delayMs`, lalu ulangi sampai `maxAttempts`.
- Jika error tidak `retryable`, langsung lempar ulang.
- Setiap kegagalan mencetak `Percobaan N gagal: <code>`.
- Jika semua percobaan gagal, lempar error terakhir.

### Simulasi

`prosesPembayaran()` gagal dua kali dengan `AppError("Gateway timeout", { code: "GATEWAY_TIMEOUT", status: 503, retryable: true })`, lalu berhasil mengembalikan `60000`.

Setelah itu, panggil `withRetry` pada fungsi yang melempar `ValidasiError("Nominal tidak valid")`, tangkap error, dan cetak kodenya.

## Ekspektasi Output

```text
Percobaan 1 gagal: GATEWAY_TIMEOUT
Percobaan 2 gagal: GATEWAY_TIMEOUT
Pembayaran berhasil: Rp60000
Kode error: VALIDASI
```

## Ketentuan

- Wajib memakai `class ... extends Error`.
- Error tidak boleh dilempar sebagai string.
- `cause` dipakai jika error dibungkus ulang.
- `withRetry` tidak boleh mengulang error non-retryable.
- Jangan memakai recursion tanpa batas.
- Jumlah percobaan tidak boleh melebihi `maxAttempts`.

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| Sukses pada percobaan pertama | `fn` dipanggil sekali |
| Gagal 2× lalu sukses | total 3 percobaan |
| Gagal 3× dengan max 3 | error terakhir dilempar |
| `ValidasiError` | langsung gagal, tidak retry |
| `maxAttempts: 1` | hanya satu percobaan |
| Error tanpa `retryable` | dianggap tidak retryable |

## Checklist Sebelum Kumpul

- [ ] `AppError` menyimpan `code`, `status`, `retryable`.
- [ ] `ValidasiError` mewarisi `AppError`.
- [ ] Retry berhenti setelah sukses.
- [ ] Error non-retryable tidak diulang.
- [ ] Jumlah percobaan sesuai batas.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Tambahkan exponential backoff: `delayMs * 2 ** (attempt - 1)`.
2. Tambahkan jitter acak maksimal 20% dari delay.
3. Simpan riwayat error di `error.causes` dan cetak saat semua percobaan gagal.
