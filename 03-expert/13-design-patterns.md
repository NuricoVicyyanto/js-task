# Task E13 — Design Patterns: Strategy, Factory, Observer, Adapter

> **Level:** Expert · **Estimasi:** 4 jam · **Topik:** strategy, factory, observer, adapter, open/closed principle

## Tujuan

Menerapkan pola desain untuk mengganti percabangan besar dan dependency yang kaku, tanpa membuat arsitektur berlebihan.

## Studi Kasus

Kopi Senja menambah metode pembayaran (tunai, QRIS, kartu) dan kanal notifikasi (email, WhatsApp). Kode saat ini memiliki `if/else` panjang di service pembayaran dan memanggil langsung modul email/WhatsApp. Tim meminta pola yang memudahkan penambahan metode baru tanpa mengubah service.

## Yang Harus Dibuat (File)

```text
e13-patterns/
├── payment/
│   ├── strategies.js
│   └── factory.js
├── events/
│   └── event-bus.js
├── repositories/
│   ├── memory-order-repository.js
│   └── json-order-repository.js
├── service.js
└── demo.js
```

## 1. Strategy — Pembayaran

Setiap strategi memiliki bentuk:

```js
{
  nama: "QRIS",
  hitungFee(total) { /* ... */ },
  bayar(total) { return { metode: this.nama, fee, total: total + fee }; }
}
```

Aturan fee:

| Metode | Fee |
| --- | --- |
| Tunai | 0 |
| QRIS | 1% dari total |
| Kartu | 2% dari total + Rp1.000 |

Contoh total `60000`:

- QRIS: fee `600`, total `60600`.
- Kartu: fee `2200`, total `62200`.

## 2. Factory — `createPaymentMethod(type)`

- Mengembalikan strategi berdasarkan `type`.
- `type` tidak dikenal → `Error("Metode pembayaran tidak dikenal")`.
- Gunakan `Map` registry, bukan `switch` panjang.
- Menambah metode baru cukup menambah registry, bukan mengubah service.

## 3. Observer — `EventBus`

| Method | Tugas |
| --- | --- |
| `on(event, listener)` | mendaftarkan listener, mengembalikan fungsi unsubscribe |
| `off(event, listener)` | menghapus listener |
| `emit(event, payload)` | memanggil semua listener |
| `listenerCount(event)` | jumlah listener |

Aturan:

- Listener satu kanal tidak boleh menghentikan listener lain jika error; tangkap dan log error.
- `off` harus benar-benar menghentikan pemanggilan berikutnya.
- Jangan memakai EventEmitter bawaan Node untuk task ini.

## 4. Adapter — Order Repository

Dua implementasi dengan kontrak sama:

```js
// save(order) -> Promise<void>
// findById(id) -> Promise<object|null>
// count() -> Promise<number>
```

- `MemoryOrderRepository`: menyimpan di `Map`.
- `JsonOrderRepository`: menyimpan ke file JSON.
- Service hanya tahu kontrak, bukan implementasi.

## Skenario Demo

1. Bayar total `60000` dengan QRIS.
2. Daftarkan listener email dan WhatsApp pada event `order.created`.
3. Emit event untuk order `KS-001`.
4. Coba metode `"bitcoin"`.
5. Simpan order ke memory repo dan JSON repo, cetak jumlah.

## Ekspektasi Output

```text
Bayar QRIS: Rp60000 + fee Rp600 = Rp60600
Notifikasi email: KS-001
Notifikasi whatsapp: KS-001
Metode tidak dikenal: error
Repo memory: 1 order
Repo JSON: 1 order
```

## Kasus Uji

| Skenario | Hasil |
| --- | --- |
| Tambah metode baru tanpa ubah service | berhasil |
| Listener error | listener lain tetap dipanggil |
| Unsubscribe | listener tidak dipanggil lagi |
| Dua listener event sama | keduanya dipanggil |
| Repo diganti | service tetap berjalan |
| File JSON tidak ada | repo membuat file baru |
| Total `0` | fee `0`, total `0` |

## Ketentuan

- Service tidak boleh berisi `if (metode === ...)`.
- Factory tidak boleh memakai `eval`.
- Observer tidak boleh membocorkan listener setelah unsubscribe.
- Adapter tidak boleh mengubah bentuk order.
- Jangan memakai inheritance berlapis jika komposisi cukup.
- Jangan menambahkan pola yang tidak digunakan.

## Checklist Sebelum Kumpul

- [ ] Strategy dan factory terpisah.
- [ ] Penambahan metode tidak mengubah service.
- [ ] EventBus mendukung unsubscribe.
- [ ] Error listener terisolasi.
- [ ] Dua repository memenuhi kontrak yang sama.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Buat plugin registry untuk metode pembayaran.
2. Tambahkan middleware pipeline pada `beforeSave`.
3. Implementasikan circuit breaker sederhana untuk payment gateway.
