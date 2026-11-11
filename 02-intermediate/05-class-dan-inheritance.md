# Task I05 — Class & Inheritance

> **Level:** Intermediate · **Estimasi:** 75 menit · **Topik:** `class`, `constructor`, `extends`, `super`, getter, static method, `instanceof`

## Tujuan Pembelajaran

Setelah task ini, kamu mampu:

1. Membuat class dengan constructor dan method.
2. Mewarisi class dan menambahkan perilaku khusus.
3. Menggunakan getter, static method, dan `instanceof`.

## Studi Kasus

Menu Kopi Senja terdiri dari minuman dan makanan. Keduanya punya nama, harga, dan kategori, tetapi minuman punya ukuran (panas/dingin) dan makanan punya porsi. Daripada menduplikasi kode, buat class dasar `MenuItem` dan dua class turunan.

## Yang Harus Dibuat

Buat file **`task-i05.js`** dengan:

### `class MenuItem`

- `constructor(nama, harga, kategori)`
- getter `hargaFormat` → `"Rp" + harga`
- method `label()` → `"<nama> | <kategori> | <hargaFormat>"`

### `class Minuman extends MenuItem`

- `constructor(nama, harga, ukuran)` memanggil `super(nama, harga, "Minuman")`
- menyimpan `ukuran`
- `label()` → label dasar + `" | " + ukuran`
- static `dariJSON({ nama, harga, ukuran })` → instance `Minuman`

### `class Makanan extends MenuItem`

- `constructor(nama, harga, porsi)` memanggil `super(nama, harga, "Makanan")`
- menyimpan `porsi`
- `label()` → label dasar + `" | porsi:" + porsi`
- static `dariJSON({ nama, harga, porsi })` → instance `Makanan`

## Skenario Program

```js
const menu = [
  new Minuman("Espresso", 18000, "panas"),
  new Minuman("Latte", 24000, "dingin"),
  new Makanan("Croissant", 25000, 1),
];

menu.forEach((item) => console.log(item.label()));
console.log("Jumlah menu:", menu.length);
console.log("Espresso adalah Minuman:", menu[0] instanceof Minuman);

const matcha = Minuman.dariJSON({ nama: "Matcha", harga: 26000, ukuran: "dingin" });
console.log("Dari JSON:", matcha.label());
```

## Ekspektasi Output

```text
Espresso | Minuman | Rp18000 | panas
Latte | Minuman | Rp24000 | dingin
Croissant | Makanan | Rp25000 | porsi:1
Jumlah menu: 3
Espresso adalah Minuman: true
Dari JSON: Matcha | Minuman | Rp26000 | dingin
```

## Ketentuan

- `Minuman` dan `Makanan` wajib memakai `extends` dan `super`.
- `label()` pada subclass wajib memanggil `super.label()`.
- Getter `hargaFormat` hanya didefinisikan sekali di class dasar.
- Static method mengembalikan instance class yang benar, bukan objek biasa.
- Jangan menduplikasi logika `nama | kategori | harga`.
- Jangan memakai function constructor lama atau `prototype` manual.

## Kasus Uji

| Pemeriksaan | Hasil |
| --- | --- |
| `menu[0] instanceof MenuItem` | `true` |
| `menu[0] instanceof Minuman` | `true` |
| `menu[2] instanceof Minuman` | `false` |
| `Minuman.dariJSON(...) instanceof Minuman` | `true` |
| `hargaFormat` saat harga `0` | `"Rp0"` |
| Subclass tanpa `super()` | harus error, bukan berjalan diam-diam |

## Checklist Sebelum Kumpul

- [ ] Tiga class ada dan hubungan warisan benar.
- [ ] `super()` dipanggil di setiap constructor turunan.
- [ ] Getter dan static method bekerja.
- [ ] `instanceof` menunjukkan hasil yang benar.
- [ ] Tidak ada duplikasi logika label.
- [ ] Output sama persis dengan contoh.

## Bonus

1. Tambahkan getter `hargaPajak` yang mengembalikan harga + 11%.
2. Tambahkan method `toJSON()` pada setiap class.
3. Buat `MenuFactory.dariJSON(data)` yang memilih class berdasarkan `kategori`.
