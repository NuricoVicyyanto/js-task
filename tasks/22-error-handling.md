# Task 22 — Error Handling: Validasi Pesanan

> **Level:** Menengah · **Estimasi:** 60 menit · **Topik:** `throw`, `try`, `catch`, `Error`, `error.message`, validasi berlapis

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Melempar error saat data tidak valid menggunakan `throw new Error()`.
2. Menangkap error dengan `try / catch`.
3. Menampilkan pesan error yang jelas tanpa menghentikan seluruh program.

## Studi Kasus

Kasir Kopi Senja menerima pesanan dari berbagai sumber. Kadang nama pelanggan kosong, daftar item kosong, atau jumlah item nol. Program tidak boleh langsung berhenti; ia harus menolak pesanan yang tidak valid dan menampilkan alasannya.

## Aturan Validasi

Periksa secara berurutan:

1. `pelanggan` wajib diisi (bukan string kosong atau hanya spasi).
2. `items` wajib berupa array dan minimal berisi 1 item.
3. Setiap `item.jumlah` harus lebih dari `0`.

Pesan error yang harus dilempar:

| Kondisi | Pesan error |
| --- | --- |
| Nama kosong | `Nama pelanggan wajib diisi` |
| Items bukan array atau kosong | `Pesanan minimal 1 item` |
| Jumlah item ≤ 0 | `Jumlah item harus lebih dari 0` |

## Yang Harus Dibuat

Buat file **`task-22.js`** dengan:

1. Fungsi `validasiPesanan(pesanan)` yang melempar error sesuai aturan di atas.
2. Jika valid, fungsi mengembalikan string `${pelanggan} (${jumlah} item)`.
3. Fungsi `cobaValidasi(nomor, pesanan)` yang memanggil `validasiPesanan` di dalam `try/catch`, lalu mencetak hasil atau pesan error.
4. Empat skenario uji: valid, nama kosong, items kosong, jumlah nol.

## Data Uji

```js
const valid = {
  pelanggan: "Nadia",
  items: [
    { nama: "Espresso", jumlah: 2 },
    { nama: "Latte", jumlah: 1 },
  ],
};

const tanpaNama = { pelanggan: "   ", items: [{ nama: "Latte", jumlah: 1 }] };
const tanpaItem = { pelanggan: "Nadia", items: [] };
const jumlahNol = { pelanggan: "Nadia", items: [{ nama: "Latte", jumlah: 0 }] };
```

## Ketentuan

- Gunakan `throw new Error("...")`, bukan `console.log` di dalam fungsi validasi.
- Gunakan `error.message` untuk menampilkan alasan.
- Jangan menghentikan program dengan `process.exit()`.
- Validasi nama harus mengabaikan spasi: `"   "` dianggap kosong.
- Periksa nama terlebih dahulu, lalu items, lalu jumlah.

## Ekspektasi Output

```text
Kasus 1: Pesanan valid: Nadia (2 item)
Kasus 2: GAGAL: Nama pelanggan wajib diisi
Kasus 3: GAGAL: Pesanan minimal 1 item
Kasus 4: GAGAL: Jumlah item harus lebih dari 0
```

## Contoh Kasus Uji

| Data | Hasil |
| --- | --- |
| `pelanggan: ""` | GAGAL: Nama pelanggan wajib diisi |
| `items: "Espresso"` | GAGAL: Pesanan minimal 1 item |
| `items: [{ jumlah: -1 }]` | GAGAL: Jumlah item harus lebih dari 0 |
| `items: [{ jumlah: 1 }]` | valid |
| `pelanggan: "Nadia "` | valid, nama di-trim |

## Checklist Sebelum Kumpul

- [ ] Tiga aturan validasi diterapkan berurutan.
- [ ] Error dilempar dengan `Error`, bukan string biasa.
- [ ] `try/catch` menangkap setiap skenario.
- [ ] Program tetap berjalan setelah satu kasus gagal.
- [ ] Pesan error sama persis dengan tabel.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Tambahkan properti `kode` pada error, misalnya `err.kode = "NAMA_KOSONG"`.
2. Gunakan `finally` untuk mencetak `--- selesai memeriksa kasus ---` setiap kali.
3. Buat error khusus `ValidasiError` yang mewarisi `Error`.
