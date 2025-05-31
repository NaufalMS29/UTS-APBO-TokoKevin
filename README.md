# Perancangan website untuk warung kevin
Proyek ini disusun sebagai bentuk pemenuhan tugas Ujian Tengah Semester pada mata kuliah Analisis Pemrograman Berorientasi Objek, yang diampu oleh Bapak Adi Wahyu Pribadi, S.Si., M.Kom.

Pada proyek ini, kami dari kelompok Warung Kak Kevin merancang dan mengembangkan sebuah sistem berbasis website untuk admin yang berfungsi sebagai pusat kendali operasional warung. Website ini dirancang agar dapat membantu proses pengelolaan bisnis secara efisien, terstruktur, dan terdokumentasi dengan baik. Kami menambahkan fitur utama yang di implementasikan dalam sistem seperti pencatatan transaksi pembelian barang, pencatatan transaksi penjualan, manajemen data supplier dan manajemen stok produk.

# Anggota Kelompok 4
| No | Nama Anggota          | NPM         |
|----|-----------------------|-------------|
| 1  | Kevin Khozimah Zaki   | 4523210057  |
| 2  | Mohammad Sayifullah   | 4523210066  |
| 3  | Muhammad Zaidan Ahbab | 4523210081  |
| 4  | Naufal Maulana Saputra| 4523210017  |
| 5  | Tri Anggoro Budi      | 4523210108  | 

# Aktor yang menggunakan website warung kevin
1. Admin sebagai aktor tunggal yang menggunakan website admin

# Usecase
<img src="https://github.com/user-attachments/assets/10c2814e-757e-4a9c-a4c5-ebec55f6bb53" alt="gambar" width="650" />

# Entity Relationship Diagram
<img src="https://github.com/user-attachments/assets/39ea209a-a1bf-48ee-99ff-db0d3fc72ec3" alt="gambar" width="650" />

# Table Master dan Relasi
### 1. Table Master
CREATE TABLE `user` (
  `id_user` int NOT NULL,
  `nama_user` varchar(50) DEFAULT NULL,
  `email` varchar(50) DEFAULT NULL,
  `password` varchar(50) DEFAULT NULL,
  `role` enum('Super Admin','Admin') DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom   | Tipe Data                      | Keterangan             |
|--------------|--------------------------------|------------------------|
| id_user      | INT (PK)                       | ID unik pengguna       |
| nama_user    | VARCHAR(50)                    | Nama lengkap pengguna  |
| email        | VARCHAR(50)                    | Alamat email           |
| password     | VARCHAR(50)                    | Kata sandi             |
| role         | ENUM('Super Admin','Admin')    | Peran pengguna         |


| Nama Kolom            | Tipe Data     | Keterangan                               |
|-----------------------|---------------|------------------------------------------|
| id_detail_penjualan   | INT (PK)      | ID detail penjualan                      |
| jumlah_produk         | INT           | Jumlah produk terjual                    |
| harga_satuan          | INT           | Harga satuan per produk                  |
| id_transaksi_penjualan| INT (FK)      | Referensi ke tabel `transaksi_penjualan` |
| id_produk             | INT (FK)      | Referensi ke tabel `produk`              |


CREATE TABLE `supplier` (
  `id_supplier` int NOT NULL,
  `nama_supplier` varchar(50) DEFAULT NULL,
  `telepon` varchar(15) DEFAULT NULL,
  `email` varchar(50) DEFAULT NULL,
  `alamat` text
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom     | Tipe Data     | Keterangan               |
|----------------|---------------|--------------------------|
| id_supplier    | INT (PK)      | ID unik supplier         |
| nama_supplier  | VARCHAR(50)   | Nama supplier            |
| telepon        | VARCHAR(15)   | Nomor telepon            |
| email          | VARCHAR(50)   | Alamat email             |
| alamat         | TEXT          | Alamat lengkap           |

CREATE TABLE `kategori` (
  `id_kategori` int NOT NULL,
  `nama_kategori` varchar(50) DEFAULT NULL,
  `keterangan` text
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom     | Tipe Data     | Keterangan           |
|----------------|---------------|----------------------|
| id_kategori    | INT (PK)      | ID kategori produk   |
| nama_kategori  | VARCHAR(50)   | Nama kategori        |
| keterangan     | TEXT          | Deskripsi kategori   |

CREATE TABLE `produk` (
  `id_produk` int NOT NULL,
  `nama_produk` varchar(50) DEFAULT NULL,
  `harga_jual` int DEFAULT NULL,
  `harga_beli` int DEFAULT NULL,
  `stok` int DEFAULT NULL,
  `id_kategori` int DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom     | Tipe Data     | Keterangan             |
|----------------|---------------|------------------------|
| id_produk      | INT (PK)      | ID produk              |
| nama_produk    | VARCHAR(50)   | Nama produk            |
| harga_jual     | INT           | Harga jual produk      |
| harga_beli     | INT           | Harga beli produk      |
| stok           | INT           | Stok tersedia          |
| id_kategori    | INT (FK)      | Referensi kategori     |

### 1. Table Relasi
CREATE TABLE `pembelian` (
  `id_pembelian` int NOT NULL,
  `tanggal` date DEFAULT NULL,
  `total_pembelian` int DEFAULT NULL,
  `id_supplier` int DEFAULT NULL,
  `id_user` int DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom       | Tipe Data     | Keterangan                         |
|------------------|---------------|------------------------------------|
| id_pembelian     | INT (PK)      | ID pembelian                       |
| tanggal          | DATE          | Tanggal pembelian                  |
| total_pembelian  | INT           | Total nilai pembelian              |
| id_supplier      | INT (FK)      | Referensi ke tabel `supplier`      |
| id_user          | INT (FK)      | Referensi ke tabel `user`          |

---

CREATE TABLE `detail_pembelian` (
  `id_detail_pembelian` int NOT NULL,
  `id_pembelian` int DEFAULT NULL,
  `id_produk` int DEFAULT NULL,
  `jumlah_pembelian` int DEFAULT NULL,
  `harga_satuan` int DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

| Nama Kolom         | Tipe Data     | Keterangan                              |
|--------------------|---------------|-----------------------------------------|
| id_detail_pembelian | INT (PK)     | ID detail pembelian                     |
| id_pembelian        | INT (FK)     | Referensi ke tabel `pembelian`          |
| id_produk           | INT (FK)     | Referensi ke tabel `produk`             |
| jumlah_pembelian    | INT          | Jumlah produk yang dibeli               |
| harga_satuan        | INT          | Harga satuan per produk                 |

CREATE TABLE `transaksi_penjualan` (
  `id_transaksi_penjualan` int NOT NULL,
  `total_penjualan` int DEFAULT NULL,
  `tanggal` date DEFAULT NULL,
  `metode_pembayaran` enum('Tunai','E-Wallet') DEFAULT NULL,
  `id_user` int DEFAULT NULL
) 

| Nama Kolom            | Tipe Data                        | Keterangan                          |
|-----------------------|----------------------------------|-------------------------------------|
| id_transaksi_penjualan| INT (PK)                         | ID transaksi penjualan              |
| total_penjualan       | INT                              | Total nilai penjualan               |
| tanggal               | DATE                             | Tanggal transaksi                   |
| metode_pembayaran     | ENUM('Tunai','E-Wallet')         | Metode pembayaran                   |
| id_user               | INT (FK)                         | Referensi ke tabel `user`           |


CREATE TABLE `detail_penjualan` (
  `id_detail_penjualan` int NOT NULL,
  `jumlah_produk` int DEFAULT NULL,
  `harga_satuan` int DEFAULT NULL,
  `id_transaksi_penjualan` int DEFAULT NULL,
  `id_produk` int DEFAULT NULL
)

| Nama Kolom            | Tipe Data                        | Keterangan                            |
|-----------------------|----------------------------------|---------------------------------------|
| id_transaksi_penjualan| INT (PK)                         | ID transaksi penjualan                |
| total_penjualan       | INT                              | Total nilai penjualan                 |
| tanggal               | DATE                             | Tanggal transaksi                     |
| metode_pembayaran     | ENUM('Tunai','E-Wallet')         | Metode pembayaran                     |
| id_user               | INT (FK)                         | Referensi ke tabel `user`             |

# Class Diagram
<img src="https://github.com/user-attachments/assets/d02c1c61-601f-4f44-b33f-bc9b369efe77" alt="gambar" width="650" />

# Wireframe
<img src="https://github.com/user-attachments/assets/560e086f-4c2e-4660-a5f3-fce2fb932499" alt="Image">
<img src="https://github.com/user-attachments/assets/dd9bb3f6-a53f-4517-bc78-0338a2b9c12f" alt="Image">
<img src="https://github.com/user-attachments/assets/1ad9aeea-95ab-4c9d-8bdb-c4dfc80bbe9d" alt="Image">
<img src="https://github.com/user-attachments/assets/1797e3e2-5954-4fec-967a-ff1dbaa7b211" alt="Image">
<img src="https://github.com/user-attachments/assets/e8bac065-5b30-40e3-a5ad-beba340804d6" alt="Image">
<img src="https://github.com/user-attachments/assets/df61171a-d7a1-4216-9ce2-5cdd7b890bc1" alt="Image">
<img src="https://github.com/user-attachments/assets/f511871e-4b04-41f1-9696-06994a33f41b" alt="Image">
<img src="https://github.com/user-attachments/assets/d201d33d-a5c9-4154-a937-e3db8f067b66" alt="Image">
<img src="https://github.com/user-attachments/assets/11a2687e-b778-4cd1-bd17-77d4ca826e20" alt="Image">
<img src="https://github.com/user-attachments/assets/84b21b09-f56a-4947-a0d8-65e98b3441c9" alt="Image">
<img src="https://github.com/user-attachments/assets/90c71298-e370-4240-8db2-a044cfc091cf" alt="Image">
<img src="https://github.com/user-attachments/assets/957e94a1-fffa-42b1-b072-925fdf416f6b" alt="Image">
<img src="https://github.com/user-attachments/assets/574ab14e-69db-4c21-be44-0e977b851af6" alt="Image">
<img src="https://github.com/user-attachments/assets/f7031d68-5582-4c68-b49c-71f6a60ec210" alt="Image">
<img src="https://github.com/user-attachments/assets/2b6f450d-4a41-4178-b351-8a66fa6edfb7" alt="Image">
<img src="https://github.com/user-attachments/assets/697a21bf-cb1c-46fb-8df3-22046b266105" alt="Image">
<img src="https://github.com/user-attachments/assets/97c8f6d1-68c6-480b-81bf-8d602a3b9fac" alt="Image">
<img src="https://github.com/user-attachments/assets/d342a7db-2ba3-4e6a-a0e8-8ca0630f887c" alt="Image">
<img src="https://github.com/user-attachments/assets/d99e6738-499e-4801-bf81-6500fc5e1d83" alt="Image">
<img src="https://github.com/user-attachments/assets/14813868-6353-43bf-ae90-9c280d0b9960" alt="Image">
<img src="https://github.com/user-attachments/assets/f0cd4da3-5b29-4897-8258-d869327c8bf7" alt="Image">
<img src="https://github.com/user-attachments/assets/dcf527ea-0c21-49f2-8a8a-4690493a13af" alt="Image">
<img src="https://github.com/user-attachments/assets/0f2b97c1-f986-4c08-b93c-fa5695496338" alt="Image">
<img src="https://github.com/user-attachments/assets/7100a70d-bd04-4768-89fe-bdbb3538aefb" alt="Image">
<img src="https://github.com/user-attachments/assets/8c25eb9b-0ece-4a6b-be0f-5a4f14634b18" alt="Image">
<img src="https://github.com/user-attachments/assets/6d58ae7f-9e57-4726-b6fe-b9d7cdaa2045" alt="Image">
<img src="https://github.com/user-attachments/assets/97de74f9-2c4e-4f1b-8ba8-f4d33218a1b3" alt="Image">
<img src="https://github.com/user-attachments/assets/272cfed9-176f-417c-b454-d2a01f44ddd1" alt="Image">
<img src="https://github.com/user-attachments/assets/1aa48e6f-3d81-4389-936e-59e1853c184e" alt="Image">
<img src="https://github.com/user-attachments/assets/ac3d1045-9363-47d2-9d64-cf3a0e614765" alt="Image">
<img src="https://github.com/user-attachments/assets/49ed8873-f6a6-4535-becd-8cee53f2f9b6" alt="Image">
