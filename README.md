# Saudi Arabia Used Cars
Contents :

1. Business Problem Understanding

2. Data Understanding

3. Data Preprocessing

4. Modeling

5. Conclusion

6. Recommendation

___

# Business Problem Understanding

**Context**

Pasar mobil bekas di Arab Saudi tumbuh pesat, dengan nilai mencapai USD 9,6 miliar pada 2024 dan diperkirakan meningkat menjadi USD 16,8 miliar pada 2033 (CAGR 6,43%). Kenaikan harga mobil baru, pajak PPN 15%, serta preferensi terhadap solusi transportasi yang terjangkau menjadi pendorong utama tren ini.

Platform seperti Syarah.com mempermudah transaksi dengan fitur inspeksi, garansi, dan pengiriman, namun penetapan harga tetap menjadi tantangan. Oleh karena itu, proyek ini bertujuan membangun model prediksi harga mobil bekas berdasarkan fitur kendaraan seperti merek, tahun, jarak tempuh, dan kondisi, guna membantu penjual dan pembeli menentukan harga yang wajar dan kompetitif.

**Goals**

Berdasarkan permasalahan tersebut, penjual mobil bekas di Arab Saudi memerlukan sebuah alat prediksi yang dapat membantu mereka menentukan harga jual mobil bekas secara tepat dan kompetitif. Mengingat adanya perbedaan karakteristik pada setiap mobil, seperti merek, tahun pembuatan, kapasitas mesin, transmisi, asal kendaraan, hingga jumlah kilometer yang telah ditempuh, maka penting untuk mempertimbangkan faktor-faktor ini dalam proses penentuan harga.

Dengan adanya prediction tool yang akurat dan berbasis data, penjual — baik individu maupun dealer — dapat menetapkan harga yang wajar, yang tidak hanya mempercepat proses penjualan, tetapi juga memaksimalkan potensi keuntungan. Di sisi lain, pembeli pun akan merasa lebih percaya diri karena mengetahui bahwa harga yang mereka bayarkan sesuai dengan kondisi dan nilai pasar kendaraan.

Bagi platform seperti Syarah.com, alat prediksi harga ini dapat meningkatkan pengalaman pengguna, memperkuat kepercayaan pelanggan, serta menarik lebih banyak listing dan transaksi di platform mereka. Hal ini pada akhirnya akan berkontribusi terhadap pertumbuhan bisnis dan pendapatan platform secara keseluruhan.

**Analytic Approach**

Langkah pertama yang perlu dilakukan adalah menganalisis data untuk mengidentifikasi pola dan hubungan antara fitur-fitur mobil, seperti merek, tahun pembuatan, jenis transmisi, kapasitas mesin, asal kendaraan, opsi tambahan, serta jarak tempuh. Analisis ini bertujuan untuk memahami bagaimana masing-masing fitur berkontribusi terhadap variasi harga mobil bekas di pasar.

Setelah pola tersebut ditemukan, kita akan membangun sebuah model regresi yang mampu memprediksi harga mobil bekas berdasarkan karakteristik yang dimiliki oleh mobil tersebut. Model ini akan berperan sebagai prediction tool yang dapat digunakan oleh penjual, dealer, maupun platform seperti Syarah untuk memperkirakan harga jual yang wajar dan kompetitif bagi mobil yang baru akan ditawarkan. Dengan begitu, proses penentuan harga menjadi lebih objektif, efisien, dan menguntungkan semua pihak yang terlibat.

**Metric Evaluation**

Evaluasi metrik yang akan digunakan adalah RMSE, MAE, dan MAPE, di mana:

RMSE (Root Mean Squared Error) adalah nilai rataan akar kuadrat dari error,

MAE (Mean Absolute Error) adalah rataan nilai absolut dari error, dan

MAPE (Mean Absolute Percentage Error) adalah rataan persentase error yang dihasilkan oleh model regresi.

Semakin kecil nilai RMSE, MAE, dan MAPE yang dihasilkan, berarti model semakin akurat dalam memprediksi harga mobil bekas sesuai dengan fitur-fitur yang digunakan.

Selain itu, kita juga dapat menggunakan nilai R-squared (R²) atau adjusted R-squared jika model yang dipilih sebagai final model adalah model linear. Nilai R-squared digunakan untuk mengukur seberapa baik model dapat merepresentasikan varians keseluruhan dari data. Semakin mendekati 1, maka semakin baik pula tingkat kecocokan model terhadap data observasi. Namun demikian, metrik ini tidak valid digunakan untuk model non-linear.

# Data Understanding

Dataset ini berisi 5.624 data mobil bekas yang dikumpulkan dari situs syarah.com. Setiap baris merepresentasikan satu mobil bekas, termasuk informasi seperti merek, model, tahun pembuatan, asal mobil, opsi fitur, kapasitas mesin, jenis transmisi, jarak tempuh, harga sesuai wilayah, dan status negosiasi harga. Setiap baris data merepresentasikan informasi terkait properti dan pemiliknya.

**Attribute Information**

| Fitur         | Tipe Data | Deskripsi                                                             |
| ------------- | --------- | --------------------------------------------------------------------- |
| `Type`        | Object    | Jenis mobil bekas                                                     |
| `Region`      | Object    | Wilayah tempat mobil ditawarkan                                       |
| `Make`        | Object    | Nama perusahaan atau merek mobil                                      |
| `Gear_Type`   | Object    | Jenis transmisi mobil (otomatis/manual)                               |
| `Origin`      | Object    | Asal mobil (lokal atau impor)                                         |
| `Options`     | Object    | Fitur tambahan pada mobil (seperti Standard, Semi Full, Full)         |
| `Year`        | Integer   | Tahun pembuatan mobil                                                 |
| `Engine_Size` | Float     | Kapasitas mesin mobil dalam liter                                     |
| `Mileage`     | Integer   | Jarak tempuh mobil (dalam kilometer)                                  |
| `Negotiable`  | Boolean   | Menunjukkan apakah harga dapat dinegosiasikan (`True` jika harga = 0) |
| `Price`       | Integer   | Harga mobil bekas (dalam satuan mata uang lokal, biasanya SAR)        |

# Exploratory Data Analysis

Pada tahap EDA ini dilakukan eksplorasi awal terhadap data untuk memahami pola, distribusi, dan hubungan antar variabel yang dapat memengaruhi harga mobil bekas.

Beberapa langkah yang dilakukan antara lain:

**Visualisasi Distribusi Harga (Price)**

Distribusi harga mobil bekas divisualisasikan menggunakan histogram. Terlihat bahwa harga memiliki distribusi miring ke kanan (right-skewed), yang berarti sebagian besar mobil dihargai di bawah rata-rata, namun ada beberapa mobil dengan harga sangat tinggi (outlier).

**Analisis Korelasi antara Fitur Numerik**

Korelasi antara fitur numerik seperti Year, Mileage, Engine_Size, dan Price dihitung dan divisualisasikan dengan heatmap. Hasilnya menunjukkan bahwa Year memiliki korelasi positif dengan harga, sementara Mileage menunjukkan korelasi negatif — sesuai dengan logika bahwa mobil baru dan jarak tempuh rendah cenderung lebih mahal.

**Pengecekkan Lanjutan untuk Fitur**

Pada tahap ini dilakukan pemeriksaan terhadap kolom Negotiable, di mana ditemukan bahwa nilai True pada kolom tersebut seharusnya berkorelasi dengan Price bernilai 0. Jika terdapat baris yang menunjukkan Negotiable = True namun harga tidak nol, maka baris tersebut langsung dihapus. Selain itu, analisis juga dilakukan pada kolom Options untuk memahami isinya. Hasil EDA menunjukkan bahwa kolom ini merepresentasikan kelengkapan fitur kendaraan, dan semakin lengkap fitur yang dimiliki mobil, maka harganya cenderung lebih tinggi.

# Data Preprocessing

Pada tahap Data *PreProcessing* akan dilakukan tahapan pengolahan data agar dapat digunakan pada model machine learning nantinya. Beberapa proses yang akan dilakukan antara lain :

- Pengecekkan Data
- Penanganan Missing Value dan Duplikasi
- Konversi Tipe Data
- Penanganan Outlier
- Feature Engineering

Pada tahap **feature engineering**, dilakukan sejumlah transformasi data untuk mempersiapkan dataset agar optimal digunakan dalam proses pelatihan model machine learning. Beberapa langkah utama yang dilakukan meliputi:

**Encoding fitur kategorikal**
Fitur-fitur kategorikal seperti Make, Type, Region, Origin, dan Options diubah ke bentuk numerik menggunakan teknik encoding. Beberapa fitur di-encode menggunakan One-Hot Encoding, sementara fitur lain seperti Options yang memiliki urutan (Standard → Semi Full → Full) diencode secara ordinal.

**Feature Selection**
Fitur Price memiliki harga anomali, dimana harga mobil sangat murah atau sama dengan 0. Pada tahap ini dilakukan riset melalui berbagai sumber untuk mengetahui batas bawah dari fitur ini, sehingga nantinya dapat digunakan filtrasi untuk memperbaiki data sehingga meningkatkan akurasi model.

**Skalasi fitur numerik**
Fitur numerik seperti Year, Engine_Size, dan Mileage diskalakan menggunakan StandardScaler untuk menyesuaikan skala antar fitur agar model lebih stabil dan konvergen cepat.

**Penanganan data tidak relevan**
Fitur Negotiable dihapus karena bersifat redundan — seluruh harga yang tidak nol memiliki nilai False, sehingga kolom ini tidak memberikan informasi tambahan yang berguna bagi model.

Secara keseluruhan, tahap feature engineering ini berhasil menyederhanakan dan mempersiapkan data mentah menjadi format yang sesuai untuk modeling, dengan mempertahankan informasi penting yang memengaruhi harga mobil bekas di Arab Saudi.

# Modelling


   
