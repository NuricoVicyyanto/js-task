# Task I09 — Unit Testing dengan `node:test`

> **Level:** Intermediate · **Estimasi:** 90 menit · **Topik:** `node:test`, `node:assert/strict`, table-driven test, boundary test, `assert.throws`

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Menulis unit test tanpa library eksternal.
2. Menguji batas nilai (boundary) dan kasus error.
3. Menjalankan test dengan `node --test`.

## Studi Kasus

Aturan diskon Kopi Senja sering berubah dan pernah menyebabkan salah hitung di kasir. Sebelum aturan baru dipakai, tim ingin memastikan semua batas nilai diuji otomatis. Kamu diminta membuat modul harga dan test suite-nya.

## Yang Harus Dibuat (File)

```text
i09-testing/
├── pricing.js
└── pricing.test.js
```

## Modul `pricing.js`

### `hitungDiskon(subtotal, voucher)`

| Voucher | Syarat | Diskon |
| --- | --- | --- |
| `SENJA10` | subtotal ≥ 50000 | 10% |
| `SENJA20` | subtotal ≥ 100000 | 20% |
| lainnya / kosong | — | 0 |

- Jika `subtotal < 0`, lempar `RangeError("Subtotal tidak boleh negatif")`.
- Hasil diskon dibulatkan dengan `Math.round`.

### `hitungTotal(subtotal, voucher)`

- `diskon = hitungDiskon(subtotal, voucher)`
- `setelahDiskon = subtotal - diskon`
- `pajak = Math.round(setelahDiskon * 11 / 100)`
- kembalikan `setelahDiskon + pajak`

## Test yang Wajib Ada

Buat minimal **10 test** di `pricing.test.js`:

1. Tanpa voucher menghasilkan diskon `0`.
2. Voucher tidak dikenal menghasilkan diskon `0`.
3. `SENJA10` di bawah batas menghasilkan `0`.
4. `SENJA10` tepat di batas `50000` menghasilkan `5000`.
5. `SENJA10` di atas batas menghasilkan diskon yang benar.
6. `SENJA20` di bawah batas menghasilkan `0`.
7. `SENJA20` tepat di batas `100000` menghasilkan `20000`.
8. Subtotal negatif melempar `RangeError`.
9. Total untuk `60000` + `SENJA10` adalah `59940`.
10. Total tanpa voucher menghitung pajak dengan benar.

Gunakan **table-driven test** untuk empat kasus diskon pada poin 3, 4, 5, dan 7 (sehingga total tetap 10 test):

```js
const kasus = [
  { subtotal: 49999, voucher: "SENJA10", harapan: 0 },
  { subtotal: 50000, voucher: "SENJA10", harapan: 5000 },
  // ...
];

for (const { subtotal, voucher, harapan } of kasus) {
  test(`diskon ${voucher} untuk ${subtotal}`, () => {
    assert.equal(hitungDiskon(subtotal, voucher), harapan);
  });
}
```

## Ekspektasi Output

Jalankan:

```bash
node --test
```

Hasil akhir harus menunjukkan **10 pass, 0 fail**. Contoh tampilan:

```text
✔ tanpa voucher menghasilkan diskon 0
✔ voucher tidak dikenal menghasilkan diskon 0
✔ SENJA10 di bawah batas menghasilkan 0
...
ℹ tests 10
ℹ pass 10
ℹ fail 0
```

## Ketentuan

- Gunakan `node:test` dan `node:assert/strict`.
- Jangan memakai Jest, Vitest, Mocha, atau library lain.
- Setiap test harus independen; tidak bergantung urutan eksekusi.
- Jangan menguji implementasi internal; uji nilai kembalian dan error.
- Nama test harus menjelaskan perilaku yang diuji.
- Jangan menulis test yang selalu `true`.

## Kasus Batas yang Wajib Dicakup

| Nilai | Alasan penting |
| --- | --- |
| `49999` | satu di bawah batas |
| `50000` | tepat di batas |
| `99999` | satu di bawah batas kedua |
| `100000` | tepat di batas kedua |
| `0` | subtotal kosong |
| `-1` | input tidak valid |
| `""` | voucher kosong |
| `"senja10"` | salah huruf besar/kecil |

## Checklist Sebelum Kumpul

- [ ] Minimal 10 test dan semuanya lulus.
- [ ] Table-driven test dipakai.
- [ ] Batas 50000 dan 100000 diuji tepat.
- [ ] `assert.throws` dipakai untuk subtotal negatif.
- [ ] Tidak ada library test eksternal.
- [ ] Output menunjukkan `pass 10` dan `fail 0`.

## Bonus

1. Jalankan `node --test --experimental-test-coverage` dan capai line coverage ≥ 90%.
2. Kelompokkan test dengan `describe()` dan `it()`.
3. Uji fungsi yang memakai waktu dengan `t.mock.timers` agar test tidak menunggu lama.
