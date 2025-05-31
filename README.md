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

CREATE TABLE `supplier` (
  `id_supplier` int NOT NULL,
  `nama_supplier` varchar(50) DEFAULT NULL,
  `telepon` varchar(15) DEFAULT NULL,
  `email` varchar(50) DEFAULT NULL,
  `alamat` text
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE `kategori` (
  `id_kategori` int NOT NULL,
  `nama_kategori` varchar(50) DEFAULT NULL,
  `keterangan` text
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE `produk` (
  `id_produk` int NOT NULL,
  `nama_produk` varchar(50) DEFAULT NULL,
  `harga_jual` int DEFAULT NULL,
  `harga_beli` int DEFAULT NULL,
  `stok` int DEFAULT NULL,
  `id_kategori` int DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

### 1. Table Relasi
CREATE TABLE `pembelian` (
  `id_pembelian` int NOT NULL,
  `tanggal` date DEFAULT NULL,
  `total_pembelian` int DEFAULT NULL,
  `id_supplier` int DEFAULT NULL,
  `id_user` int DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE `detail_pembelian` (
  `id_detail_pembelian` int NOT NULL,
  `id_pembelian` int DEFAULT NULL,
  `id_produk` int DEFAULT NULL,
  `jumlah_pembelian` int DEFAULT NULL,
  `harga_satuan` int DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE `transaksi_penjualan` (
  `id_transaksi_penjualan` int NOT NULL,
  `total_penjualan` int DEFAULT NULL,
  `tanggal` date DEFAULT NULL,
  `metode_pembayaran` enum('Tunai','E-Wallet') DEFAULT NULL,
  `id_user` int DEFAULT NULL
) 

CREATE TABLE `detail_penjualan` (
  `id_detail_penjualan` int NOT NULL,
  `jumlah_produk` int DEFAULT NULL,
  `harga_satuan` int DEFAULT NULL,
  `id_transaksi_penjualan` int DEFAULT NULL,
  `id_produk` int DEFAULT NULL
)