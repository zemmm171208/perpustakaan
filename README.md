# perpustakaan

# 📚 DATABASE PERPUSTAKAAN

## Implementasi DDL, DML, JOIN, dan VIEW pada MySQL

---

# 📝 Deskripsi Proyek

Database Perpustakaan ini dibuat untuk mengelola data anggota, buku, dan transaksi peminjaman.
Dalam pembuatan database ini digunakan perintah **DDL (Data Definition Language)** untuk membuat struktur tabel, **DML (Data Manipulation Language)** untuk mengelola data, **JOIN** untuk menggabungkan beberapa tabel, dan **VIEW** untuk menyederhanakan query kompleks.

Database ini terdiri dari tiga tabel utama yaitu **anggota**, **buku**, dan **peminjaman**.
Tabel peminjaman berfungsi sebagai tabel relasi yang menghubungkan anggota dengan buku.

---

# 🧩 Struktur Database

## 1. Tabel Anggota

Menyimpan data anggota perpustakaan seperti ID anggota, nama, kelas, alamat, dan tanggal daftar.

## 2. Tabel Buku

Menyimpan data buku seperti ID buku, judul, pengarang, penerbit, tahun terbit, dan stok.

## 3. Tabel Peminjaman

Menyimpan data transaksi peminjaman buku yang menghubungkan tabel anggota dan tabel buku.

---

# 🛠️ DDL (Data Definition Language)

## Membuat Database

```sql
CREATE DATABASE perpustakaan;
USE perpustakaan;
```

Penjelasan: Membuat database baru dengan nama **perpustakaan** dan mengaktifkannya.

---

## Membuat Tabel Anggota

```sql
CREATE TABLE anggota (
    id_anggota INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(100) NOT NULL,
    kelas VARCHAR(20) NOT NULL,
    alamat TEXT,
    tanggal_daftar DATE
);
```

Penjelasan: Membuat tabel anggota untuk menyimpan data anggota perpustakaan.

---

## Membuat Tabel Buku

```sql
CREATE TABLE buku (
    id_buku INT AUTO_INCREMENT PRIMARY KEY,
    judul VARCHAR(100) NOT NULL,
    pengarang VARCHAR(100),
    penerbit VARCHAR(100),
    tahun_terbit YEAR,
    stok INT DEFAULT 0
);
```

Penjelasan: Membuat tabel buku untuk menyimpan data buku yang tersedia.

---

## Membuat Tabel Peminjaman

```sql
CREATE TABLE peminjaman (
    id_peminjaman INT AUTO_INCREMENT PRIMARY KEY,
    id_anggota INT,
    id_buku INT,
    tanggal_pinjam DATE,
    tanggal_kembali DATE,
    status VARCHAR(20),
    FOREIGN KEY (id_anggota) REFERENCES anggota(id_anggota),
    FOREIGN KEY (id_buku) REFERENCES buku(id_buku)
);
```

Penjelasan: Membuat tabel peminjaman yang berfungsi sebagai tabel relasi antara anggota dan buku.

---

# 📥 DML (Data Manipulation Language)

## Insert Data Anggota

```sql
INSERT INTO anggota (nama, kelas, alamat, tanggal_daftar) VALUES
('Andi', 'XI RPL 1', 'Bogor', '2026-01-10'),
('Budi', 'XI RPL 2', 'Cibinong', '2026-01-11'),
('Citra', 'XI RPL 1', 'Depok', '2026-01-12');
```

Penjelasan: Menambahkan data anggota ke dalam tabel anggota.

---

## Insert Data Buku

```sql
INSERT INTO buku (judul, pengarang, penerbit, tahun_terbit, stok) VALUES
('Pemrograman Java', 'Eko', 'Informatika', 2022, 10),
('Database MySQL', 'Rudi', 'Andi Offset', 2021, 5),
('Algoritma Dasar', 'Sari', 'Erlangga', 2020, 7);
```

Penjelasan: Menambahkan data buku ke dalam tabel buku.

---

## Insert Data Peminjaman

```sql
INSERT INTO peminjaman (id_anggota, id_buku, tanggal_pinjam, tanggal_kembali, status) VALUES
(1, 1, '2026-02-01', '2026-02-07', 'Dipinjam'),
(2, 2, '2026-02-02', '2026-02-08', 'Dipinjam'),
(3, 3, '2026-02-03', '2026-02-09', 'Dikembalikan');
```

Penjelasan: Menambahkan data transaksi peminjaman buku.

---

# 🔍 SELECT (Menampilkan Data)

## Menampilkan Semua Data Anggota

```sql
SELECT * FROM anggota;
```

Penjelasan: Menampilkan seluruh data anggota.

---

## Menampilkan Buku dengan Stok Lebih dari 5

```sql
SELECT * FROM buku
WHERE stok > 5;
```

Penjelasan: Menampilkan buku yang memiliki stok lebih dari 5.

---

# ✏️ UPDATE (Mengubah Data)

## Mengubah Status Peminjaman

```sql
UPDATE peminjaman
SET status = 'Dikembalikan'
WHERE id_peminjaman = 1;
```

Penjelasan: Mengubah status peminjaman menjadi dikembalikan.

---

# 🗑️ DELETE (Menghapus Data)

## Menghapus Data Anggota

```sql
DELETE FROM anggota
WHERE id_anggota = 3;
```

Penjelasan: Menghapus data anggota dengan ID 3.

---

# 🔗 JOIN (Menggabungkan Tabel)

## Menampilkan Data Peminjaman Lengkap

```sql
SELECT 
    peminjaman.id_peminjaman,
    anggota.nama AS nama_anggota,
    buku.judul,
    peminjaman.tanggal_pinjam,
    peminjaman.tanggal_kembali,
    peminjaman.status
FROM peminjaman
JOIN anggota ON peminjaman.id_anggota = anggota.id_anggota
JOIN buku ON peminjaman.id_buku = buku.id_buku;
```

Penjelasan:
Query JOIN digunakan untuk menggabungkan tiga tabel sehingga menghasilkan informasi peminjaman secara lengkap yang terdiri dari nama anggota, judul buku, tanggal pinjam, tanggal kembali, dan status.

---

# 👁️ VIEW (Tabel Virtual)

## Membuat View Peminjaman

```sql
CREATE VIEW v_peminjaman AS
SELECT 
    anggota.nama AS nama_anggota,
    buku.judul,
    peminjaman.tanggal_pinjam,
    peminjaman.tanggal_kembali,
    peminjaman.status
FROM peminjaman
JOIN anggota ON peminjaman.id_anggota = anggota.id_anggota
JOIN buku ON peminjaman.id_buku = buku.id_buku;
```

Penjelasan:
View digunakan untuk menyimpan query JOIN sehingga dapat dipanggil kembali tanpa menuliskan ulang query.

---

## Menjalankan View

```sql
SELECT * FROM v_peminjaman;
```

Penjelasan: Menampilkan data peminjaman melalui view.

---

# 📌 Kesimpulan

Database perpustakaan ini dibuat menggunakan DDL untuk membangun struktur tabel dan DML untuk mengelola data.
JOIN digunakan untuk menggabungkan data dari beberapa tabel sehingga menghasilkan informasi yang lengkap, sedangkan VIEW digunakan untuk menyederhanakan query agar lebih mudah digunakan.

Dengan adanya database ini, pengelolaan data perpustakaan menjadi lebih terstruktur, efisien, dan mudah diakses.
