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

# Mockup
<img src="https://github.com/user-attachments/assets/92e52e46-b30b-4841-bb73-495207306324" alt="Image">
<img src="https://github.com/user-attachments/assets/50dcb72d-66ad-481a-b674-aeaf445dd822" alt="Image">
<img src="https://github.com/user-attachments/assets/a42b6a65-b08b-4587-9047-e2054c334af7" alt="Image">
<img src="https://github.com/user-attachments/assets/c41cf3fc-2880-4def-895b-459243f92de4" alt="Image">
<img src="https://github.com/user-attachments/assets/06d421ac-05df-4971-a30a-843b11e3e756" alt="Image">
<img src="https://github.com/user-attachments/assets/175c1de6-9e38-44bc-b26e-91e059410596" alt="Image">
<img src="https://github.com/user-attachments/assets/7bf51bec-ea71-44b1-bc80-3f5cde378f2f" alt="Image">
<img src="https://github.com/user-attachments/assets/1fa47050-1150-4fb2-ac92-3e98427dd2c7" alt="Image">
<img src="https://github.com/user-attachments/assets/671b1694-3d64-4c6b-8b63-32ed8dc5b9f6" alt="Image">
<img src="https://github.com/user-attachments/assets/aeed291c-59b3-4df7-b1f8-01e3af67a619" alt="Image">
<img src="https://github.com/user-attachments/assets/5c8e7050-71e0-4c35-83d8-2db2202b49aa" alt="Image">
<img src="https://github.com/user-attachments/assets/e9d0022a-cbc6-4d73-b726-798bb53ecd39" alt="Image">
<img src="https://github.com/user-attachments/assets/496aacf9-cbe1-4095-a39d-8c4997926749" alt="Image">
<img src="https://github.com/user-attachments/assets/0bffaa2e-76d3-4da5-b887-c6ef0ef49e46" alt="Image">
<img src="https://github.com/user-attachments/assets/f4044c57-d4bb-4cac-9266-1d3ff6a773d2" alt="Image">
<img src="https://github.com/user-attachments/assets/b0a7d5f2-8654-4b8f-a974-c9fa9e2b917d" alt="Image">
<img src="https://github.com/user-attachments/assets/8fb2f1d0-5d06-4937-b17e-245631913db8" alt="Image">
<img src="https://github.com/user-attachments/assets/a145fb6b-d776-46ee-b2b5-d15757854d91" alt="Image">
<img src="https://github.com/user-attachments/assets/99565430-2f8f-4092-9b35-87a7a5e92ab1" alt="Image">
<img src="https://github.com/user-attachments/assets/ba6458fc-94d2-48a9-afd2-5dff6a77a4eb" alt="Image">
<img src="https://github.com/user-attachments/assets/5cf24000-fdda-40ba-9ed1-48cf75e51bb0" alt="Image">
<img src="https://github.com/user-attachments/assets/9ba30e81-72ef-452c-bc73-3b1cb1216a6e" alt="Image">
<img src="https://github.com/user-attachments/assets/0e26f96c-d147-4303-aa92-57b0d1fdadf7" alt="Image">
<img src="https://github.com/user-attachments/assets/3184e950-fa5d-4f78-ac20-1d53f989f3c1" alt="Image">
<img src="https://github.com/user-attachments/assets/c344e250-f939-44d0-b7fd-414233807833" alt="Image">
<img src="https://github.com/user-attachments/assets/28f956c0-b70e-402e-a200-699125be5fb6" alt="Image">
<img src="https://github.com/user-attachments/assets/7554b368-4d70-4dae-b81c-5f62c72c49c6" alt="Image">
<img src="https://github.com/user-attachments/assets/ef3314cc-20f4-4728-a869-48c00192c858" alt="Image">
<img src="https://github.com/user-attachments/assets/e8f85821-92db-425b-b0f2-88468f027855" alt="Image">
<img src="https://github.com/user-attachments/assets/b98d0fbb-900b-4682-beff-69372eb2fc29" alt="Image">
<img src="https://github.com/user-attachments/assets/b8270650-b02a-4dc3-9291-726fc30da13f" alt="Image">

