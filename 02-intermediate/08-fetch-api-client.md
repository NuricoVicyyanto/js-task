# Task I08 — Fetch API Client

> **Level:** Intermediate · **Estimasi:** 90 menit · **Topik:** `fetch`, `URL`, `URLSearchParams`, `AbortSignal.timeout`, error HTTP, API client

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Membuat client API yang rapi dan dapat dipakai ulang.
2. Menangani query string, timeout, dan status HTTP.
3. Mengubah response error menjadi error yang konsisten.

## Studi Kasus

Halaman kasir Kopi Senja mengambil menu dari server internal. Saat ini setiap bagian kode memanggil `fetch` dengan URL yang ditulis manual, sehingga sulit diubah dan rawan lupa menangani error. Buat satu **API client** dengan base URL, timeout, dan error yang seragam.

## Server Latihan

Buat `server.js` sederhana menggunakan `node:http` dengan endpoint:

| Method | Path | Response |
| --- | --- | --- |
| GET | `/api/menu?page=1&limit=2` | `{ data: [...2 menu], page, limit, total: 4 }` |
| GET | `/api/menu/2` | `{ id: 2, nama: "Latte", harga: 24000 }` |
| GET | `/api/menu/999` | status `404`, `{ error: "Menu tidak ditemukan" }` |
| GET | `/api/error` | status `500`, `{ error: "Kesalahan server" }` |

Jalankan server di `http://localhost:3000`. Data menu: Espresso 18000, Latte 24000, Kopi Susu 22000, Croissant 25000.

## Yang Harus Dibuat

Buat file **`client.js`** dengan fungsi `buatApiClient(baseUrl)` yang mengembalikan objek:

| Method | Tugas |
| --- | --- |
| `getMenu({ page = 1, limit = 2 })` | mengambil daftar menu dengan query string |
| `getMenuById(id)` | mengambil satu menu |
| `request(path, options)` | helper internal untuk fetch, timeout, dan error |

### Perilaku wajib

- Base URL tidak ditulis ulang di setiap method.
- Query string dibuat dengan `URL` dan `URLSearchParams`.
- Timeout memakai `AbortSignal.timeout(2000)`.
- Periksa `response.ok`; jika gagal, baca body JSON dan lempar `ApiError` berisi `status` dan `message`.
- Semua response sukses dikembalikan sebagai objek, bukan `Response`.
- Jangan menelan error; pemanggil harus bisa menangkapnya.

## Skenario Program

```js
const api = buatApiClient("http://localhost:3000");

const halaman = await api.getMenu({ page: 1, limit: 2 });
console.log("Halaman 1:", halaman.data.map((m) => m.nama).join(", "));
console.log("Total:", halaman.total);

const menu = await api.getMenuById(2);
console.log(`Menu 2: ${menu.nama} - Rp${menu.harga}`);

try {
  await api.getMenuById(999);
} catch (err) {
  console.log(`Error ${err.status}: ${err.message}`);
}
```

## Ekspektasi Output

```text
Halaman 1: Espresso, Latte
Total: 4
Menu 2: Latte - Rp24000
Error 404: Menu tidak ditemukan
```

## Ketentuan

- Gunakan `async/await`.
- Wajib memakai `URL` dan `URLSearchParams`.
- Wajib memakai `AbortSignal.timeout`.
- Wajib memeriksa `response.ok`.
- Error HTTP harus mempertahankan status dan pesan dari server.
- Jangan memakai `fetch(baseUrl + "/api/...")` dengan penggabungan string manual untuk query.

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| `getMenu()` tanpa argument | page `1`, limit `2` |
| `getMenu({ page: 2, limit: 2 })` | query benar, data halaman 2 |
| `getMenuById(999)` | `ApiError` status `404` |
| Server mati | error koneksi tertangkap pemanggil |
| Server lambat > 2 detik | error timeout, bukan menggantung |
| `/api/error` | `ApiError` status `500` |

## Checklist Sebelum Kumpul

- [ ] Base URL hanya didefinisikan sekali.
- [ ] Query string dibuat dengan `URLSearchParams`.
- [ ] Timeout bekerja.
- [ ] `response.ok` diperiksa.
- [ ] Error memiliki `status` dan `message`.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Tambahkan retry otomatis untuk status `5xx` maksimal dua kali.
2. Tambahkan cache sederhana untuk `getMenu` berdasarkan page/limit.
3. Buat method `getAllMenu()` yang mengambil semua halaman secara berurutan.
