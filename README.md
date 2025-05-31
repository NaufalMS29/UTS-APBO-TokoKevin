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
<img src="https://github.com/user-attachments/assets/0e21e461-28e4-450b-b549-47ca37b53ce9" />
<img src="https://github.com/user-attachments/assets/c0b300aa-b1b8-4387-a142-105c26fdea69" />
<img src="https://github.com/user-attachments/assets/d7c6314f-d6a7-4275-9d8a-1e9b47c5b6cc" />
<img src="https://github.com/user-attachments/assets/3ab31ec9-c9ee-4ea3-b4e7-fb6cc427dfa3" />
<img src="https://github.com/user-attachments/assets/321088ca-edb5-4e60-9fae-57f6e8431cbb" />
<img src="https://github.com/user-attachments/assets/31e3ce1c-66e0-404c-8da5-b89ea86485b5" />
<img src="https://github.com/user-attachments/assets/daef1872-cca7-4d15-96b6-218d4cdb6ae7" />
<img src="https://github.com/user-attachments/assets/73b6a5d7-1345-4b1c-acea-6b66eac2a815" />
<img src="https://github.com/user-attachments/assets/2748efa6-c740-45dd-a1a1-2e7883fcd71d" />
<img src="https://github.com/user-attachments/assets/240fede2-2eb4-4a39-ba21-d714f5ff35eb" />
<img src="https://github.com/user-attachments/assets/52bb4e4e-61d9-4147-9102-207f06740960" />
<img src="https://github.com/user-attachments/assets/49700c61-2c1d-4814-9339-9b534e7ff597" />
<img src="https://github.com/user-attachments/assets/74371695-ddd2-4676-b84b-b7ced1b7e6b0" />
<img src="https://github.com/user-attachments/assets/39c6a67d-d3be-4961-8941-dd35a25544e9" />
<img src="https://github.com/user-attachments/assets/f1af8491-e35f-400a-879e-bc06d4b8201e" />
<img src="https://github.com/user-attachments/assets/b8db120b-9368-4ad8-80d8-2e73370fc275" />
<img src="https://github.com/user-attachments/assets/3619dfae-e13b-42cd-8152-578183d04bb5" />
<img src="https://github.com/user-attachments/assets/f918b647-75f9-4f5a-9531-f7539f02cdf1" />
<img src="https://github.com/user-attachments/assets/2c70c1a9-ac31-4892-960c-a1af6ec2dfab" />
<img src="https://github.com/user-attachments/assets/0e6d05f5-a24a-476c-a964-621ab83f5971" />
<img src="https://github.com/user-attachments/assets/979a09d6-b0e8-4bc9-9455-0ff75b4b48ce" />
<img src="https://github.com/user-attachments/assets/60da9d46-a703-403f-a8ca-dff29cc948b0" />
<img src="https://github.com/user-attachments/assets/5c08ef2b-6e83-4478-a236-b67e44f73596" />
<img src="https://github.com/user-attachments/assets/9d9632c6-63ae-496e-a106-49a155202220" />
<img src="https://github.com/user-attachments/assets/433cd98e-3be3-441c-962b-479f00f765fe" />
<img src="https://github.com/user-attachments/assets/d39ceee0-f86d-4dd2-b037-d0e3b6527662" />
<img src="https://github.com/user-attachments/assets/ff0f526d-8ca6-408b-85b2-a974e70a1eaa" />
<img src="https://github.com/user-attachments/assets/7e76a06f-9bc6-4d2f-921b-202cf2933c74" />
<img src="https://github.com/user-attachments/assets/cb351a29-ecf6-4063-bbfb-1546e2d6d6ce" />
<img src="https://github.com/user-attachments/assets/99ea64d0-3d6c-49da-bee3-ff607c3e01d6" />
<img src="https://github.com/user-attachments/assets/a1eb4e79-3711-432d-8bf0-406b80660d50" />
<img src="https://github.com/user-attachments/assets/4eb393f9-1282-4311-84c4-b917e3927fee" />

