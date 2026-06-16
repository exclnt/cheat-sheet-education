##  DASAR-DASAR PRISMA CLI

###  `npx prisma init`

> Inisialisasi proyek Prisma (buat folder `prisma/` dan file `.env`).

 Hasil:

* `prisma/schema.prisma`
* `.env`

---

###  `npx prisma generate`

> Menghasilkan Prisma Client berdasarkan `schema.prisma`.

 Gunakan setelah mengedit model atau menjalankan migrasi.

---

###  `npx prisma migrate dev --name <nama>`

> Membuat dan menjalankan migrasi di development.

 Fungsi:

* Sinkronisasi skema ke database.
* Generate Prisma Client.

 Contoh:

```bash
npx prisma migrate dev --name init
```

---

###  `npx prisma migrate reset`

> Menghapus seluruh data & migrasi, lalu ulangi migrasi dari awal.

 **Hati-hati!** Semua data akan dihapus.

 Biasanya digunakan saat develop lokal.

---

###  `npx prisma migrate deploy`

> Menjalankan semua migrasi di **production** tanpa prompt interaktif.

 Cocok untuk CI/CD atau server production.

---

###  `npx prisma db push`

> Mendorong skema langsung ke database ​**tanpa migrasi**​.

 Cocok untuk prototyping atau project kecil.

 Tidak membuat history migrasi!

---

###  `npx prisma db seed`

> Menjalankan **script seeding** untuk mengisi data awal.

 Harus diatur dulu di `package.json`:

```json
"prisma": {
  "seed": "node prisma/seed.js"
}
```

Lalu jalankan:

```bash
npx prisma db seed
```

---

###  `npx prisma studio`

> Membuka **GUI antarmuka visual** untuk melihat dan mengedit data database.

 Sangat membantu untuk debug dan eksplorasi data.

---

###  `npx prisma format`

> Merapikan format file `schema.prisma`.

 Mirip `prettier` untuk Prisma.

---

###  `npx prisma validate`

> Mengecek apakah `schema.prisma` valid.

 Cocok untuk step CI atau sebelum deploy.

---

###  `npx prisma introspect`

> Membaca struktur dari database yang sudah ada dan generate model Prisma-nya.

 Cocok untuk project yang sudah punya database lama.

---

##  Ringkasan Praktis

| Command               | Kapan digunakan       | Penjelasan Singkat            |
| ----------------------- | ----------------------- | ------------------------------- |
| `prisma init`     | Awal setup            | Membuat struktur awal Prisma  |
| `prisma generate` | Setelah ubah model    | Regenerasi Prisma Client      |
| `migrate dev`     | Saat ubah struktur DB | Buat dan jalankan migrasi dev |
| `migrate deploy`  | Di server             | Jalankan migrasi production   |
| `db push`         | Prototyping           | Update DB tanpa migrasi       |
| `studio`          | Debug / eksplorasi    | GUI visual editor             |
| `introspect`      | Database lama         | Generate schema dari DB       |
| `format`          | Kapan aja             | Merapikan file Prisma         |
| `validate`        | Sebelum deploy        | Validasi schema               |
| `db seed`         | Isi data awal         | Eksekusi file seeding         |

