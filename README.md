# Laporan Proyek Machine Learning - Riffa Bella Wahyu S

## Project Overview - Sistem Rekomendasi Movie

Perkembangan teknologi informasi mendorong meningkatnya kebutuhan akan hiburan digital, termasuk film. Tren film yang viral di media sosial sering kali menarik minat pengguna untuk mengakses platform penyedia film. Namun, tidak semua film tren sesuai dengan preferensi pengguna. Banyaknya pilihan dan minimnya informasi membuat pengguna kesulitan menemukan film yang sesuai. Oleh karena itu, dibutuhkan sistem rekomendasi yang dapat membantu menyajikan film berdasarkan preferensi pengguna [1].

Salah satu pendekatan yang efektif dalam sistem rekomendasi adalah Collaborative Filtering (CF), yaitu metode yang memanfaatkan data historis interaksi pengguna untuk memprediksi film yang mungkin disukai. Metode ini telah banyak digunakan oleh berbagai platform besar seperti Netflix dan Amazon [2]. Namun, pendekatan CF tradisional memiliki beberapa keterbatasan, seperti kesulitan dalam menangani pengguna atau item baru (cold start) serta ketidakmampuannya memodelkan hubungan kompleks antara pengguna dan item (data sparsity).

Untuk mengatasi keterbatasan tersebut, dikembangkan pendekatan Neural Collaborative Filtering (NCF) yang menggabungkan CF dengan arsitektur deep learning. Penelitian oleh Ayyiyah et al. menunjukkan bahwa NCF mampu memberikan hasil akurasi prediksi yang baik dalam sistem rekomendasi film, dengan nilai RMSE yang rendah. Selain itu, studi lain juga menunjukkan efektivitas NCF dalam mengatasi permasalahan non-linearitas hubungan pengguna dan item [3], [4]. Integrasi metode ini dalam sistem rekomendasi terbukti memberikan hasil yang lebih personal dan relevan.

Proyek ini bertujuan membangun sistem rekomendasi film berbasis NCF dengan menggunakan dataset dari Kaggle yang mencakup data rating dan demografi pengguna. Sistem ini diharapkan dapat merekomendasikan 10 film terbaik untuk setiap pengguna berdasarkan riwayat preferensi mereka.

## Business Understanding

### Problem Statements
- **Pernyataan Masalah 1 :** Dengan data rating yang dimiliki, bagaimana perusahaan dapat merekomendasikan movie (film) lain yang mungkin disukai dan belum pernah dibaca oleh pengguna?

- **Pernyataan Masalah 2 :** Bagaimana cara membangun sistem yang mampu merekomendasikan 10 film terbaik bagi setiap pengguna berdasarkan preferensi pribadi mereka, menggunakan data historis rating film?

### Goals
1. Menghasilkan sejumlah rekomendasi movie yang sesuai dengan preferensi pengguna dan belum pernah dibaca sebelumnya dengan teknik collaborative filtering. 
   
2. Memberikan daftar 10 rekomendasi film teratas untuk setiap pengguna, berdasarkan preferensi historis mereka.
   
### Solution Statements
- **Solusi 1 : Penerapan pendekatan NCF**, dengan membangun model menggunakan algoritma collaborative filtering berbasis matrix factorization neural network untuk memprediksi rating dan merekomendasikan movie yang sesuai preferensi user dan belum dibaca.

- **Solusi 2 :** Dengan menggunakan hasil prediksi model untuk setiap pasangan pengguna dan film, lalu melakukan pemeringkatan (ranking) terhadap seluruh film yang belum diberi rating oleh masing-masing pengguna. Dari hasil tersebut, diambil 10 film teratas dengan skor prediksi tertinggi sebagai rekomendasi personal untuk setiap pengguna.

## Data Understanding
Pada proyek ini, data yang digunakan adalah Movielens Rating Dataset yang tersedia publik di [Kaggle](https://www.kaggle.com/datasets/mukeshmanral/movielens-rating-dataset?)  Dengan informasi dataset yang terdiri dari 3 file yaitu Movie, Demografi pengguna, dan Rating, sebagai berikut :
1. Movie : terdiri dari 1271 baris, dan 22 kolom
2. Demografi Pengguna : terdiri dari 943 baris, dan 5 kolom
3. Rating : terdiri dari 100000 baris, dan 4 kolom

- **Kondisi Data**
  - Terdapat missing value pada data movie di kolom relaese_date yang kehilangan satu data. Untuk di data demografi dan rating, tidak ada data yang hilang.

- **Variabel-variabel pada Movielens Rating Dataset adalah sebagai berikut :**
  - **movie_info (movie) :** merupakan informasi film, yang berisi 2 kolom kategorikal yaitu kolom movie title, dan release date. Kemudian terdapat 20 kolom numerik yaitu 1 kolom movie id, dan 19 kolom genre (unknown, action, adventure, animation, children's, comedy, crime, documentary, drama, fantasy, film-noir, horor, musical, mystery, romance, Sci-Fi, Thriller, War, dan Western)

  - **user_demographics (demografi) :** merupakan informasi tentang pengguna yang berisi user_id, age, gender, occupation, dan zip code.

  - **ratings (rating) :** merupakan informai penilaian atau rating yang diberikan oleh pengguna. Yang berisi user_id, movie_id, rating, dan unix_timestamp.
    
- **Exploratory Data Analysis (EDA)**
1. Pada data **Movie**
   - Menampilkan jumlah baris dan kolom serta jenis data setiap kolom ``movie.info()`` yang terdapat 2 kolom kategorikal dan 20 kolom numerikal dibawah ini
       
     ![Image](https://github.com/user-attachments/assets/cbff0d1b-a7db-48da-bf3b-2703db6168ce)
     
2. Pada data **Demografi Pengguna**
   -  Menampilkan jumlah baris dan kolom serta jenis data setiap kolom ``demografi.info()`` yang terdapat 3 kolom kategorikal dan 2 kolom numerikal dibawah ini
       
      ![Image](https://github.com/user-attachments/assets/0dc7757d-487c-46a8-8fa9-eebf66d2bd56)

   - Menampilkan 5 baris pertama dari dataframe demografi ``demografi.head()``

     ![Image](https://github.com/user-attachments/assets/39615c5f-39ce-4574-8a1a-36ca9500e071)

   - Menampilkan informasi pengguna, yang memberikan informasi pekerjaan mereka

     ![Image](https://github.com/user-attachments/assets/6a9af991-0e25-4889-8528-f5c7df1a71fd)

3. Pada data **Rating**,
   - Menampilkan jumlah baris dan kolom serta jenis data setiap kolom ``rating.info()`` yang terdapat 4 kolom numerikal dibawah ini
       
     ![Image](https://github.com/user-attachments/assets/8c49f86f-2397-48bf-9178-a793ec6203c1)

   - Menampilkan 5 baris pertama dari dataframe demografi ``rating.head()``

     ![Image](https://github.com/user-attachments/assets/595bbd70-8e41-4719-9899-b968eed08fa9)

   - Menampilkan informasi pengguna yang memberikan rating, dan memberikan penilian berapa

     ![Image](https://github.com/user-attachments/assets/b174d30e-525e-4c97-9f2e-fde5fb676d62)

   - Menampilkan visualisasi distribusi rating yang diberikan pengguna
  
     ![Image](https://github.com/user-attachments/assets/77688f73-8f26-4a66-b1f1-32f771fb47f4)

     Insight :

      - Pada data rating ini memiliki 100000 baris dan 4 kolom. Yang terdiri user_id (id pengguna), movie_id, rating, dan unix timestamp.
      - Pada diagram rating diatas menunjukkan pengguna paling banyak memberikan rating 4, dan paling sedikit memberikan rating 1.
      - Pada pengecekan nilai yang hilang, data rating tidak memiliki nilai yang hilang.

- **Data Preprocessing**
   - Menggabungkan kolom pada data movie, selain kolom movie_id, movie_title dan release_date, menjadi kolom genre sebagai berikut

     ![Image](https://github.com/user-attachments/assets/8cb43cf0-d3cb-4da6-b868-e4d92bda1072)

     Penggabungan kolom pada data movie digunakan untuk mempersingkat data movie. Dan dapat tahu dalam satu film memiliki berapa genre. Sehingga sekarang pada data movie hanya memiliki 4 kolom saja.

   - Melakukan Pengecekan Missing Values, sebelumnya pada saat menampilkan movie.info pada kolom release_data mengalami perbedaan jumlah data yaitu kehilangan 1 data, sehingga dilakukan pengisian nilai "Unknown". Agar seluruh kolom pada masing-masing data tidak ada yang missing value.

      ```
      # Mengisi missing values di Movie
      movie['release_date'] = movie['release_date'].fillna('Unknown')
      
      # Memeriksa missing values
      print(movie.isnull().sum())
      print(demografi.isnull().sum())
      print(rating.isnull().sum())
      ```

     ![Image](https://github.com/user-attachments/assets/028cda6b-17a2-4765-a724-0c63e74083ca)

   - Membuat dictionary untuk data movie_id, movie_title, dan genre yang disimpan pada movie_new sebagai berikut :

     ![Image](https://github.com/user-attachments/assets/d1448791-922b-406a-a126-0354a26fb8e1)
     
   - Mengelompokkan data berdasarkan demografi pengguna 

     ![Image](https://github.com/user-attachments/assets/c3e03b3c-2810-41b8-9e77-6664336c9be9)
     
   - Mengelompokkan data berdasarkan movie

     ![Image](https://github.com/user-attachments/assets/0faf4830-0051-4650-a224-fab15f07e443)


## Data Preparation
- **Teknik Data Preparation dan Proses Data Preparation :**
  - Melakukan Encoding pada kolom user_id dan movie_id, untuk mengubah nilai aslinya menjadi indeks numerik berurutan. Hal ini dilakukan agar data dapat digunakan sebagai input ke dalam embedding layer pada model NCF. Proses ini juga disertai dengan pembuatan pemetaan balik untuk mempermudah interpretasi hasil rekomendasi. Berikut contohnya pada encoding kolom user_id

   ![Image](https://github.com/user-attachments/assets/ad217f1d-ccc2-4965-be55-6c37c8d1ba99)
     
   - Melakukan Mapping pada Hasil Encoding ke DataFrame, nilai hasil mapping ini disimpan di kolom baru (user dan movie) yang nantinya digunakan sebagai input ke dalam model. Langkah ini bertujuan untuk mengonversi data kategorikal menjadi numerik, sesuai dengan kebutuhan embedding layer dalam model NCF, tanpa menghilangkan ID asli yang masih dibutuhkan untuk interpretasi hasil rekomendasi.

  - Menghitung jumlah user dan movie unik yang di-encode. Informasi ini digunakan untuk menentukan dimensi embedding pada model rekomendasi. Selain itu, kolom rating dikonversi ke tipe data float32 agar sesuai dengan format TensorFlow, dan dilakukan pencarian nilai minimum serta maksimum rating untuk keperluan normalisasi. Langkah ini penting untuk menyesuaikan data dengan kebutuhan input model dan meningkatkan performa pelatihan. Sebagai berikut outputnya :

  ![Image](https://github.com/user-attachments/assets/a52cddb3-3eed-4772-9298-929dcdb5a195) 

  - Melakukan Pengacakan Data menggunakan metode shuffling untuk menghindari bias akibat urutan data. Proses ini penting agar pembagian data ke dalam subset training dan validasi lebih merata dan representatif, serta untuk membantu model belajar dari data yang lebih beragam, sehingga meningkatkan kemampuan generalisasi model. Sebagai berikut outputnya :

   ![Image](https://github.com/user-attachments/assets/a05fd48f-4be4-48d8-8af2-d5f86ba3a5c1)

  - Melakukan Pembagian Data untuk Training dan Validasi, dengan pembuatan fitur input (x) berupa pasangan user dan movie hasil encoding, serta label output (y) berupa rating yang telah dinormalisasi. Selanjutnya, data dibagi menjadi dua subset, yaitu 80% untuk training dan 20% untuk validasi, agar model dapat dilatih dan diuji secara adil terhadap data yang tidak pernah dilihat sebelumnya. Langkah ini bertujuan untuk memastikan model belajar secara optimal dan mampu melakukan generalisasi. Sebagai berikut outputnya :

   ![Image](https://github.com/user-attachments/assets/fb869f2d-2b7a-40f8-874d-13310f28aa13)

## Modeling
Dalam proyek ini, digunakan pendekatan **Neural Collaborative Filtering (NCF)** untuk membangun sistem rekomendasi film berbasis data historis interaksi pengguna. Model yang digunakan adalah RecommenderNet, yaitu sebuah model neural network yang mengimplementasikan teknik matrix factorization menggunakan embedding layer untuk mempelajari representasi laten (fitur tersembunyi) dari user dan movie.

Model ini dibangun dengan framework TensorFlow dan Keras, dan terdiri dari beberapa komponen utama, yaitu embedding untuk user dan movie, serta embedding bias untuk masing-masingnya. Representasi pengguna dan film dihitung melalui operasi dot product, yang kemudian dijumlahkan dengan bias, dan hasil akhirnya dilewatkan ke fungsi aktivasi sigmoid untuk menghasilkan skor prediksi dalam rentang 0 hingga 1. Skor ini merepresentasikan kemungkinan bahwa seorang pengguna akan menyukai suatu film, yang kemudian digunakan untuk menyusun rekomendasi film yang paling relevan.

- **Tahapan Modeling:**
1. Membangun Arsitektur Model (class RecommenderNet)
   Pada tahap ini, kita mendefinisikan arsitektur dari model rekomendasi yang akan digunakan, yaitu RecommenderNet, sebuah model berbasis Neural Collaborative Filtering (NCF). Model ini menggunakan pendekatan Matrix Factorization dengan embedding layer untuk mewakili user dan movie dalam bentuk representasi vektor laten berdimensi rendah. Dengan komponen utama seperti ``embedding`` ``Bias embedding`` ``dot product`` ``sigmoid``
   
2. Inisialisasi dan Kompilasi Model
   Dengan menginisialisasi model dengan parameter jumlah user, jumlah movie, dan ukuran embedding. Kemudian, model perlu dikompilasi untuk menentukan bagaimana proses belajar akan dilakukan. Dengan komponennya yaitu ``BinaryCrossentropy`` ``Adam`` ``RootMeanSquaredError``
   
3. Training Model
   Dengan melatih model menggunakan data pelatihan. Pada tahap ini, model akan belajar dari interaksi user-movie (misalnya, rating) untuk memahami pola preferensi. Parameter yang digunakan ``batch_size`` dan ``epoch``
   
- **Menyajikan top-N Recommendation untuk satu pengguna**

![Image](https://github.com/user-attachments/assets/87b9552c-b451-4fe0-8ccc-fb0c191a5b41)

## Evaluation
- **Metrik Evaluasi yang Digunakan**
  
  Pada proyek ini, menggunakan RMSE sebagai metrik evaluasi yang digunakan untuk mengukur rata-rata kesalahan prediksi model terhadap nilai sebenarnya dalam satuan yang sama dengan target (rating). Semakin kecil nilai RMSE, semakin baik model dalam memprediksi. Formulanya sebagai berikut:

$$
RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n}(y_i - \hat{y}_i)^2}
$$ 

   RMSE memberikan penalti yang lebih besar terhadap kesalahan prediksi yang besar, sehingga model diharapkan dapat meminimalkan kesalahan besar agar performanya optimal. Nilai RMSE yang lebih kecil menunjukkan bahwa prediksi model lebih akurat dan mendekati nilai sebenarnya.

- **Visualisasi Metrik Evaluasi**

   ![Image](https://github.com/user-attachments/assets/a2a06011-fe75-4035-a43b-20203d458fc6)

    Gambar di atas menampilkan plot metrik Root Mean Squared Error (RMSE) selama proses training model. Garis biru menunjukkan nilai RMSE pada data pelatihan (training) untuk setiap epoch, yang terlihat menurun tajam di awal, lalu secara bertahap menjadi stabil setelah beberapa epoch. Sementara itu, garis oranye menunjukkan nilai RMSE pada data validasi (test), yang awalnya juga menurun namun kemudian cenderung stagnan atau sedikit meningkat.

    Kondisi ini mengindikasikan bahwa model berhasil belajar dengan baik dari data pelatihan, tetapi mulai kehilangan kemampuan generalisasinya terhadap data baru setelah sekitar epoch ke-10. Hal ini merupakan indikasi awal terjadinya overfitting, di mana model terlalu menyesuaikan diri dengan data pelatihan dan kurang efektif dalam memprediksi data yang belum pernah dilihat.
   
- **Hasil Proyek Berdasarkan Metrik Evaluasi**
  
  ![Image](https://github.com/user-attachments/assets/2b0a1d55-f666-40f9-8773-f2099a5c9430)

   Gambar diatas menunjukkan bahwa RSME mendekati 0 artinya prediksi rating dari model sangat mendekati rating yang sebenarnya diberikan pengguna. Dengan nilai 0.2660 menunjukkan performa model cukup baik, karena rating biasanya berada di antara 0 dan 1 (setelah normalisasi oleh sigmoid). Model ini sudah berhasil dievaluasi dengan baik, dan mampu mempelajari reprenstasi interaksi user-movie secara efektif. 
  

## Daftar Pustaka

[1] N. K. Ayyiyah, R. Kusumaningrum, dan R. Rismiyati, “Film Recommender System Menggunakan Metode Neural Collaborative Filtering,” Jurnal Teknologi Informasi dan Ilmu Komputer (JTIIK), vol. 10, no. 3, pp. 699–708, 2023.

[2] F. Ricci, L. Rokach, dan B. Shapira, Recommender Systems Handbook, 2nd ed. Springer, 2022.

[3] K. Zhang, W. Wang, dan J. Li, “A Survey on Deep Neural Networks in Collaborative Filtering,” ResearchGate, 2023.

[4] S. Al-Otaibi, A. Alghamdi, dan M. Khan, “A Hybrid Recommendation System using Collaborative Filtering and Sentiment Analysis,” Journal of Engineering and Applied Science, SpringerOpen, vol. 71, no. 1, 2024.
