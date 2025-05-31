# Laporan Proyek Machine Learning - Riffa Bella Wahyu S

## Project Overview - Sistem Rekomendasi Movie

## Business Understanding

### Problem Statements
- **Pernyataan Masalah 1 :** Dengan data rating yang dimiliki, bagaimana perusahaan dapat merekomendasikan movie (film) lain yang mungkin disukai dan belum pernah dibaca oleh pengguna?

- **Pernyataan Masalah 2 :** Bagaimana cara membangun sistem yang mampu merekomendasikan 10 film terbaik bagi setiap pengguna berdasarkan preferensi pribadi mereka, menggunakan data historis rating film?

### Goals
1. Menghasilkan sejumlah rekomendasi movie yang sesuai dengan preferensi pengguna dan belum pernah dibaca sebelumnya dengan teknik collaborative filtering. 
   
2. Memberikan daftar 10 rekomendasi film teratas untuk setiap pengguna, berdasarkan preferensi historis mereka.
   
### Solution Statements
- **Solusi 1 : Penerapan pendekatan NCF**, dengan membangun model menggunakan algoritma collaborative filtering berbasis matrix factorization neural network untuk memprediksi rating dan merekomendasikan movie yang sesuai preferensi user dan belum dibaca.. 

- **Solusi 2 :**

## Data Understanding
Pada proyek ini, data yang digunakan adalah Movielens Rating Dataset yang tersedia publik di [Kaggle](https://www.kaggle.com/datasets/mukeshmanral/movielens-rating-dataset?)  Dengan informasi dataset yang terdiri dari 3 file yaitu Movie, Demografi pengguna, dan Rating, sebagai berikut :
1. Movie : terdiri dari 1271 baris, dan 22 kolom
2. Demografi Pengguna : terdiri dari 943 baris, dan 5 kolom
3. Rating : terdiri dari 100000 bari, dan 4 kolom

- **Variabel-variabel pada Movielens Rating Dataset adalah sebagai berikut :**
  - **movie_info :** merupakan informasi film, yang berisi 2 kolom kategorikal yaitu kolom movie title, dan release data. Kemudian terdapat 20 kolom numerik yaitu 1 kolom movie id, dan 19 kolom genre (unknown, action, adventure, animation, children's, comedy, crime, documentary, drama, fantasy, film-noir, horor, musical, mystery, romance, Sci-Fi, Thriller, War, dan Western)

  - **user_demographics :** merupakan informasi tentang pengguna yang berisi user_id, age, gender, occupation, dan zip code.

  - **ratings :** merupakan informai penilaian atau rating yang diberikan oleh pengguna. Yang berisi user_id, movie_id, rating, dan unix_timestamp.
    
- **Exploratory Data Analysis (EDA)**

## Data Preparation
- **Teknik Data Preparation :** (sebutkan)
- **Proses Data Preparation :**
- **Alasan mengapa diperlukan tahapan data preparation tersebut**

## Modeling
- **Menjelaskan Sistem Rekomendasi untuk Menyelesaikan Permasalahan :**
- **Menyajikan top-N Recommendation sebagai output :**
- **Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda :**
- **Menjelaskan kelebihan dan kekurangan pada pendekatan yang dipilih :**

## Evaluation
- **Metrik Evaluasi yang Digunakan :**
- **Menjelaskan Hasil Proyek Berdasarkan Metrik Evaluasi :**
- **Menjelaskan Metrik Evaluasi yang Digunakan untuk Mengukur Kinerja Model :** (Formula dan cara metrik bekerja)

## Daftar Pustaka
