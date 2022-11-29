# Laporan Proyek Machine Learning Terapan (Predictive_Analytics)- Aghni Syifa Ahmari

## Domain Proyek

Rumah merupakan kebutuhan pokok (primer) yang dibutuhkan oleh manusia, selain makanan dan pakaian. Terlepas dari itu, rumah dikatakan sebagai instrumen investasi menjanjikan karena harganya cenderung meningkat. Apalagi rumah yang berada di negara maju seperti USA, harga rumah tentunya akan lebih tinggi karena dipengaruhi oleh fasilitas umum yang disediakan yang dapat mempermudah kehidupan penghuninya. Penentuan harga rumah yang harus diperhitungkan baik kepada penjual maupun pembeli. Namun harga tidak selalu pasti dan terprediksi dengan akurat. Oleh karena itu perlu adanya sistem yang bisa memperkirakan harga rumah berdasarkan faktor pendukungnya. 


## Business Understanding

### Problem Statements

Berdasarkan latar belakang yang telah dijelaskan diatas, terdapat beberapa masalah yaitu:
- Variabel apa saja yang berpengaruh dalam menentukan harga rumah?
- Berapa prediksi harga rumah dengan variabel tertentu? 

### Goals

Untuk menjawab masalah yang ada, akan dibuat model prediksi dengan tujuan sebagai berikut:
- Mengetahui korelasi variabel yang mempengaruhi harga rumah.
- Membuat model *machine learning* yang dapat memprediksi harga rumah dengan akurat.

### Solution statements
Solusi yang dapat dilakukan berupa:
- Melakukan EDA variabel dan memvisualisasikannya menggunakan pairplot dan heatmap untuk melihat korelasi terhadap harga rumah.
- Membangun 3 model *klasifikasi* yang bervariasi untuk memprediksi harga rumah, lalu dibandingkan hasil akurasinya untuk dipilih model mana yang memiliki hasil terbaik. Berikut model yang digunakan :
	- *K-Nearest Neighbors*
	- *Random Forest*
	- *Boosting Algorithm*

## Data Understanding
Dataset yang digunakan pada proyek ini adalah House Sales in King County, USA. Dataset tersebut didapat dari situs kaggle (https://www.kaggle.com/datasets/harlfoxem/housesalesprediction). Kumpulan data ini berisi harga jual rumah untuk King County, yang mencakup Seattle. Ini termasuk rumah yang dijual antara Mei 2014 dan Mei 2015. Dataset terdiri dari 21613 baris dan 21 kolom(fitur) yaitu : id, date, price, bedrooms, bathrooms, sqft_living, sqft_lot, floors, waterfront, view, condition, grade, sqft_above, sqft_basement, yr_built, yr_renovated, zipcode, lat, long, sqft_living15, sqft_lot15. 



### Variabel-variabel pada Motorcycle dataset adalah sebagai berikut:  
- id: ID unik untuk setiap rumah yang terjual
- date: Tanggal penjualan rumah
- price: Harga setiap rumah terjual
- bedrooms: Jumlah kamar tidur
- bathrooms: Jumlah kamar mandi, di mana .5 merupakan kamar dengan toilet tetapi tanpa pancuran
- sqft_living: Ukuran persegi ruang tamu interior apartemen
- sqft_lot: Ukuran persegi luas tanah
- floors: Jumlah lantai
- waterfront: - Variabel dummy apakah apartemen menghadap ke tepi laut atau tidak
- view: Indeks dari 0 hingga 4 tentang seberapa bagus tampilan properti itu
- condition: - Indeks dari 1 hingga 5 pada kondisi apartemen,
- grade: Indeks dari 1 hingga 13, di mana 1-3 tidak sesuai dengan konstruksi dan desain bangunan, 7 memiliki tingkat konstruksi dan desain rata-rata, dan 11-13 memiliki tingkat kualitas konstruksi dan desain yang tinggi.
- sqft_above: Rekaman persegi ruang interior perumahan yang berada di atas permukaan tanah
- sqft_basement: Rekaman persegi ruang interior perumahan yang berada di bawah permukaan tanah
- yr_built: Tahun rumah pertama kali dibangun
- yr_renovated: Tahun renovasi terakhir rumah
- zipcode: Kode pos di area mana rumah itu berada
- lat: Lintang (latitudinal)
- long: Bujur (longitudinal)
- sqft_living15: Rekaman persegi ruang hidup perumahan interior untuk 15 tetangga terdekat
- sqft_lot15: Luas tanah kavling 15 tetangga terdekat

Untuk memahami *Motorcycle* dataset akan menggunakan beberapa tahapan dari teknik *Explanatory Data Analysis* (EDA) sebagai berikut:
1.   Deskripsi Variabel

![image](https://user-images.githubusercontent.com/89571899/204506928-1adaee97-8bc2-45c8-9d8c-10f256f2e16a.png)

Gambar 1. Info dataset

Pada Gambar 1, dapat dilihat bahwa dataset terdiri dari:
*   5 variabel bertipe float
*   15 variabel bertipe integer
*   1 variabel bertipe object

2.   Menangani *missing value & outliers*

Dataset yang dipakai tidak memiliki missing value. 
Kemudian menangani *outlier*, sampel yang nilainya sangat jauh dari cakupan umum data utama. Pada kasus ini, *outliers* akan dideteksi dengan teknik visualisasi data (boxplot). Kemudian, *ouliers* akan ditangani dengan teknik *IQR method*.

3.   Analisis *Univariate*
Fitur kategori

![univariate](https://user-images.githubusercontent.com/89571899/204507083-f82054cb-2ee5-4228-af29-cbab509d442e.png)

Gambar 2. Analisis *univariate* fitur kategori

Fitur numerik

![univariate 2](https://user-images.githubusercontent.com/89571899/204507145-0592376f-4b7c-47d7-b564-f97c8cffdde1.png)

Gambar 3. Analisis *univariate* fitur numerik

Dari visualisasi pairplot diatas, kita bisa melihat bahwa :
- Jumlah terbanyak unit rumah memiliki 3 bedroom/kamar
- Jumlah rumah yang memiliki 3 lantai kurang dari 1000 unit
- Sekitar 7000 unit rumah memiliki tingkat konstruksi dan desain rata-rata (grade=7)


4.   Analisis *Multivariate* 
Fitur Kategorik

![multivariate](https://user-images.githubusercontent.com/89571899/204507223-f5522440-51cb-46b8-949d-43f2ff5b68dd.png)

Gambar 4. Analisis *multivariate* fitur kategorik

Pada gambar 4, dapat dilihat bahwa :
*   Fitur date memiliki terlalu banyak variasi, sehingga fitur date tidak mempengaruhi fitur price

Fitur Numerik

![multivariate 2](https://user-images.githubusercontent.com/89571899/204507270-ec3a9e29-36ab-4bd1-9bda-c74c83c08060.png)

Gambar 5. Analisis *multivariate* fitur numerik

Dapat kita lihat bahwa :
*   price memiliki korelasi positif terhadap variabel sqft_living dan grade
*   namun price memiliki korelasi negatif terhadap variabel yr_built

*Correlation matrix* untuk fitur numerik

![multivariate 3](https://user-images.githubusercontent.com/89571899/204507837-ab706dde-5095-4571-8577-de3913aa9e72.png)

Gambar 6. *Correlation matrix* fitur numerik

Pada Gambar 6, Fitur yang memiliki korelasi cukup kuat dengan fitur "price" adalah  'bathrooms', 'sqft_living', 'grade', 'sqft_above', 'lat', 'sqft_living15'

## Data Preparation
Dalam *data preparation*, yang akan dilakukan sebelum memasukkan data ke model latih:

- *Standarisasi* : Standarisasi menggunakan teknik *StandarScaler* dari *library Scikitlearn*. *StandardScaler* melakukan proses standarisasi fitur dengan mengurangkan mean (nilai rata-rata) kemudian membaginya dengan standar deviasi untuk menggeser distribusi.  *StandardScaler* menghasilkan distribusi dengan standar deviasi sama dengan 1 dan mean sama dengan 0. *Scaling* ini dilaksanakan untuk membantu model *machine learning* yang akan dipakai lebih mudah diolah.
- *Train-Test-Split* : Membagi dataset menjadi data latih dan data uji dengan perbandingan 90:10 yaitu 90 persen data akan menjadi data latih dan 10 persen data akan menjadi data uji . Hal ini dilakukan supaya kita dapat melakukan validasi dengan benar tanpa bias dari model.

## Modeling

Pada tahap ini, model *machine learning* yang akan dipakai ada tiga algoritma. Lalu performa masing-masing algoritma akan dievaluasi dan menentukan algoritma mana yang memberikan hasil prediksi terbaik. Ketiga algoritma yang akan digunakan, antara lain:

1.   *K-Nearest Neighbors* (KNN) : KNN bekerja dengan membandingkan jarak satu sampel ke sampel pelatihan lain dengan memilih sejumlah k tetangga terdekat (dengan k adalah sebuah angka positif). Untuk parameter yang akan digunakan yaitu n_neighbors dengan nilai sebesar 10.
		- **kelebihan** : algoritma KNN yaitu mudah dipahami dan digunakan serta algoritma yang relatif sederhana dibandingkan dengan algoritma lain.
		- **kekurangan** : jika dihadapkan pada jumlah fitur atau dimensi yang besar
2.   *Random Forest* : Algoritma ini disusun dari banyak algoritma pohon (*decision tree*) yang pembagian data dan fiturnya dipilih secara acak.  Untuk parameter yang akan digunakan yaitu n_estimators=50, max_depth=16, random_state=55, n_jobs=-1.
		- **kelebihan** : Kuat terhadap data *outlier* (pencilan data), berjalan secara efisien pada kumpulan data yang besar, dan bekerja dengan baik dengan data non-linear.
		- **kekurangan** : Pembelajaran bisa berjalan lambat, tergantung pada parameter yang digunakan dan tidak bisa memperbaiki model yang dihasilkan secara berulang.
3.   *Boosting Algorithm* : Algoritma yang menggunakan teknik *boosting* bekerja dengan membangun model dari data latih. Kemudian ia membuat model kedua yang bertugas memperbaiki kesalahan dari model pertama. Model ditambahkan sampai data latih terprediksi dengan baik atau telah mencapai jumlah maksimum model untuk ditambahkan.  Untuk parameter yang akan digunakan yaitu learning_rate=0.05, random_state=55.
		- **kelebihan** : Algoritma ini sangat *powerful* dalam meningkatkan akurasi prediksi. Algoritma *boosting* sering mengungguli model yang lebih sederhana seperti *logistic regression* dan *random forest*
		- **kekurangan** : *Learning* secara progresif dan sangat sensitif terhadap data *noise* dan *outlier*.

*Error* dari masing-masing model:

![mse](https://user-images.githubusercontent.com/89571899/204508062-d0a88292-40b4-4b4f-be06-5612384a3430.png)

Gambar 7. Visualisasi mse dari 3 model

Pada Gambar 7, dapat diliat bahwa model *Boosting* memiliki nilai *error* yang lebih kecil dibanding model lain menandakan bahwa model *Boosting* merupakan model terbaik yang dapat digunakan untuk memprediksi harga jual rumah.

## Evaluation
Metrik yang akan kita gunakan pada prediksi ini adalah MSE atau *Mean Squared Error* yang menghitung jumlah selisih kuadrat rata-rata nilai sebenarnya dengan nilai prediksi. MSE didefinisikan dalam persamaan berikut

MSE = $\frac{1}{n} \Sigma_{i=1}^n({y}-\hat{y})^2$

Dimana :

y = Nilai Aktual permintaan

$hat{y}$ = Nilai hasil peramalan

n = banyaknya data

berikut adalah hasil evaluasi ketiga model menggunakan mse pada tabel 1.

Tabel 1. Nilai mse pada data uji dan data latih dari ketiga model

|              |       train_mse | test_mse         |
|-------------:|----------------:|------------------|
|      KNN     |   6422247.74869 | 175566180.734988 | 
| RandomForest |  1649306.154105 |   88883752.13927 |
|   Boosting   | 10655061.083537 |  42409709.805507 |


Hasil prediksi masing-masing model dari 10 data dapat dilihat pada tabel 2.

Tabel 2. Hasil prediksi ketiga model dari 10 data

|       |   y_true | prediksi_KNN | prediksi_RandomForest | prediksi_Boosting |
|------:|---------:|-------------:|----------------------:|------------------:|
| 17130 | 325000.0 |     817609.0 |              676813.0 |          541086.1 |
| 17541 | 768000.0 |     817609.0 |              677386.4 |          541086.1 |
| 20183 | 260000.0 |     817609.0 |              677386.4 |          541086.1 |
|  6774 | 480000.0 |     834614.0 |              683088.2 |          541086.1 |
|  7727 | 152000.0 |     817609.0 |              676813.0 |          541086.1 |
| 19391 | 429950.0 |     817609.0 |              685322.2 |          541086.1 |
| 11055 | 399000.0 |     817609.0 |              676813.0 |          541086.1 |
| 14088 | 335000.0 |     817609.0 |              677386.4 |          541086.1 |
| 19821 | 480000.0 |     817609.0 |              677386.4 |          541086.1 |
|  7309 | 335000.0 |     834614.0 |              676813.0 |          541086.1 |

Pada tabel 2, dapat kita lihat bahwa prediksi dari ketiga algoritma yang paling mendekati y_true adalah prediksi *Boosting* menandakan bahwa *Boosting* merupakan algoritma terbaik dibandingkan dengan algoritma yang lain.

**Kesimpulan** :  Terdapat 7 variabel yang mempengaruhi harga rumah yaitu 'bathrooms', 'sqft_living', 'grade', 'sqft_above', 'lat', 'sqft_living15'. Model *machine learning* yang memiliki nilai *error* paling rendah yaitu model *Random Forest* yang menandakan bahwa *Boosting* merupakan algoritma terbaik dibandingkan dengan algoritma yang lain dalam hal memprediksi harga rumah bekas.

**Referensi** :

[1]	Muhammad Labib, dkk. “Analisis Prediksi Harga Rumah Sesuai Spesifikasi Menggunakan Multiple Linear Regression,” JURNAL INFORMATIK Edisi ke-17, Nomor 3, Desember 2021, ISSN : 2655-139X (ONLINE).

		
**---Ini adalah bagian akhir laporan---**


