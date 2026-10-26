# 011 - Middleware Layer

REST API sederhana menggunakan **Express.js** dan **PostgreSQL** yang mendemonstrasikan penggunaan **Middleware Layer** pada Web Service.

## Fitur

- **Middleware Logging** – Mencatat setiap request masuk (method, URL, status, durasi)
- **Middleware Validasi Body** – Validasi input menggunakan Joi sebelum masuk ke handler
- **Middleware Validasi Parameter** – Validasi parameter URL (seperti `:id`)
- **Response Envelope** – Format respons yang konsisten (sukses & error)
- **CRUD Biodata Mahasiswa** – Operasi Create, Read, Update, Delete

## Teknologi

| Teknologi | Kegunaan |
|-----------|----------|
| Node.js | Runtime JavaScript |
| Express.js v5 | Framework web server |
| PostgreSQL | Database relasional |
| node-postgres (pg) | Driver koneksi ke PostgreSQL |
| Joi | Validasi skema input |

## Struktur Database

```sql
CREATE TABLE biodata (
  id    SERIAL PRIMARY KEY,
  nama  VARCHAR(100) NOT NULL,
  nim   VARCHAR(20)  NOT NULL,
  kelas VARCHAR(20)  NOT NULL
);
```

## Endpoint API

| Method | Endpoint        | Deskripsi               |
|--------|-----------------|-------------------------|
| GET    | `/`             | Ambil semua data biodata |
| POST   | `/biodata`      | Tambah data biodata baru |
| PUT    | `/biodata/:id`  | Update data biodata      |
| DELETE | `/biodata/:id`  | Hapus data biodata       |

## Cara Menjalankan

1. Install dependencies:
   ```bash
   npm install
   ```

2. Sesuaikan konfigurasi database di `index.js`:
   ```js
   const pool = new Pool({
     user: 'postgres',
     host: 'localhost',
     database: 'mahasiswa',
     password: 'password_anda',
     port: 5432,
   })
   ```

3. Jalankan server:
   ```bash
   npm start
   ```

Server berjalan di `http://localhost:3000`

## Contoh Request

### Tambah Biodata (POST)
```json
POST /biodata
{
  "nama": "Budi Santoso",
  "nim": "12345678",
  "kelas": "TI-3A"
}
```

### Update Biodata (PUT)
```json
PUT /biodata/1
{
  "nama": "Budi Santoso",
  "nim": "12345678",
  "kelas": "TI-3B"
}
```

## Format Respons

### Sukses
```json
{
  "success": true,
  "message": "Data berhasil diambil",
  "data": [...],
  "error": null
}
```

### Error
```json
{
  "success": false,
  "message": "Validasi input gagal",
  "data": null,
  "error": [{ "field": "nama", "message": "\"nama\" is required" }]
}
```
