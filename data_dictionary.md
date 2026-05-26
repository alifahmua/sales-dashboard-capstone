# Data Dictionary

## Deskripsi Dataset

Dataset ini berisi data transaksi penjualan produk retail di Indonesia yang telah melalui proses data cleaning, transformasi data, agregasi penjualan harian, serta penambahan simulasi inventori.

Dataset digunakan untuk analisis penjualan, pendapatan, serta monitoring stok produk. Dataset akhir terdiri dari 63.161 baris dan 10 kolom tanpa missing value sehingga siap digunakan untuk exploratory data analysis (EDA), visualisasi data, forecasting, maupun pengembangan model machine learning.

---

## Proses Preprocessing Data

Beberapa tahapan preprocessing yang dilakukan pada dataset meliputi:

### 1. Data Cleaning
- Menghapus kolom yang tidak digunakan, seperti:
  - `Unnamed`
  - `Payment_Method`
  - `Store_Location`
  - `Unit Cost`
- Mengubah tipe data:
  - `Date` → `datetime`
  - `Revenue` → `float`
  - `Category` → `category`
- Mengubah format harga menjadi rupiah
- Melakukan standarisasi nama produk:
  - `Tolako Minuman Herbal` → `Tolak Linu`
  - `Indomilk UHT 1L` → `Indomilk UHT Full Cream 1L`

### 2. Data Transformation
- Menambahkan kategori produk baru:
  - `Bakery`
  - `Home`
  - `Make Up`
- Mengubah kategori pada beberapa produk baru
- Melakukan agregasi penjualan harian berdasarkan:
  - `Date`
  - `Province`
  - `Product_Name`

### 3. Feature Engineering
- Membuat kolom `Transaction_ID` sebagai identitas unik transaksi
- Menambahkan fitur simulasi inventori:
  - `Stock_In`
  - `Stock_Out`
  - `Stock_End`

### 4. Stock Simulation
Simulasi inventori dilakukan menggunakan beberapa aturan berikut:
- Restock awal untuk setiap produk
- Restock terjadwal setiap hari Senin dan Kamis
- Restock darurat ketika stok tidak mencukupi
- Batas maksimum stok sebesar 1000 unit

### 5. Data Merging
Dataset transaksi dan dataset stok digabung berdasarkan:
- `Date`
- `Product_Name`

---

## Kolom Dataset Final

| Nama Kolom | Tipe Data | Deskripsi | Contoh Nilai |
|---|---|---|---|
| Transaction_ID | object | ID unik untuk setiap transaksi | TRX000001 |
| Date | datetime64[ns] | Tanggal transaksi penjualan | 2023-01-01 |
| Product_Name | object | Nama produk yang dijual | ABC Kecap Asin 620ml |
| Category | category | Kategori produk | Groceries |
| Units_Sold | int64 | Jumlah unit produk yang terjual | 47 |
| Unit_Price | float64 | Harga per unit produk dalam rupiah | 18000 |
| Revenue | float64 | Total pendapatan transaksi | 846000 |
| Stock_In | int64 | Jumlah stok masuk akibat proses restock | 627 |
| Stock_Out | int64 | Jumlah stok keluar akibat penjualan | 47 |
| Stock_End | int64 | Jumlah stok akhir produk setelah transaksi | 580 |

---

## Variabel dalam Analisis

| Nama Variabel | Deskripsi | Rumus / Metode |
|---|---|---|
| Revenue | Total pendapatan transaksi | Units_Sold × Unit_Price |
| Stock_Out | Jumlah stok keluar akibat penjualan | Sama dengan Units_Sold |
| Stock_End | Jumlah stok akhir produk setelah proses restock dan penjualan | Stok sebelumnya + Stock_In − Stock_Out |
| Daily Sales | Total penjualan harian produk | Agregasi berdasarkan tanggal dan produk |

---

## Informasi Dataset

| Informasi | Nilai |
|---|---|
| Jumlah Baris | 63.161 |
| Jumlah Kolom | 10 |
| Missing Value | Tidak ada |
| Format Dataset | CSV |
| Dataset Final | `transactions_clean.csv` |
| Jenis Dataset | Structured Data |
| Domain Dataset | Retail Sales |

---

## Catatan Tambahan

- Dataset akhir merupakan hasil penggabungan antara dataset transaksi dan dataset stok inventori.
- Kolom inventori (`Stock_In`, `Stock_Out`, dan `Stock_End`) merupakan hasil simulasi berdasarkan aturan restock dan aktivitas penjualan produk.
- Dataset telah diurutkan berdasarkan tanggal transaksi dan nama produk.
- Dataset siap digunakan untuk exploratory data analysis (EDA), visualisasi data, forecasting, maupun pengembangan model machine learning.