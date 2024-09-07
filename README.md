# Movie Recommendation System

## Project Overview

Sistem rekomendasi telah menjadi bagian penting dari berbagai layanan digital, seperti e-commerce, platform streaming, dan media sosial. Dalam konteks platform streaming film, sistem rekomendasi memainkan peran penting dalam meningkatkan pengalaman pengguna dengan menyarankan film yang sesuai dengan preferensi individu. Dua metode utama yang digunakan dalam sistem rekomendasi adalah content-based filtering dan collaborative filtering [^1].

Content-based filtering bekerja dengan menganalisis karakteristik atau fitur dari konten yang telah dinikmati pengguna sebelumnya, lalu merekomendasikan konten yang memiliki karakteristik serupa. Di sisi lain, collaborative filtering berfokus pada perilaku dan preferensi pengguna lain yang memiliki pola serupa, menggunakan pendekatan seperti Singular Value Decomposition (SVD) untuk memprediksi preferensi [^2].

Proyek ini menggabungkan kedua metode tersebut untuk menciptakan sistem rekomendasi film yang lebih akurat dan personal. Dengan menggabungkan content-based dan collaborative filtering, diharapkan dapat mengatasi kelemahan dari masing-masing metode. Misalnya, content-based filtering sering kali terbatas pada preferensi pengguna yang sudah ada, sementara collaborative filtering dapat menghasilkan rekomendasi yang lebih inovatif namun mungkin rentan terhadap masalah cold start.

## Pentingnya Proyek

Sistem rekomendasi yang akurat sangat penting dalam meningkatkan kepuasan pengguna dan menjaga keterlibatan pengguna dalam platform streaming. Dalam dunia di mana jumlah konten digital yang tersedia terus bertambah secara eksponensial, pengguna sering kali merasa kewalahan dengan banyaknya pilihan yang ada. Oleh karena itu, sistem rekomendasi yang dapat menyaring dan menyajikan konten yang relevan menjadi sangat berharga.

Proyek ini penting untuk diselesaikan karena akan memungkinkan platform streaming untuk menyediakan rekomendasi film yang lebih tepat sasaran, meningkatkan retensi pengguna, dan pada akhirnya, mengoptimalkan pendapatan platform tersebut. Selain itu, dengan memanfaatkan metode gabungan, proyek ini berpotensi untuk memberikan wawasan baru dalam pengembangan sistem rekomendasi yang lebih canggih di masa depan.

## Business Understanding

### Problem Statements

- Bagaimana cara memberikan rekomendasi film yang relevan kepada pengguna berdasarkan kesamaan konten dari film yang telah mereka tonton?
- Bagaimana cara memberikan rekomendasi film yang relevan kepada pengguna berdasarkan pola preferensi dan interaksi mereka dengan film sebelumnya?


### Goals

- Membangun sistem rekomendasi film berbasis konten yang dapat memberikan rekomendasi yang relevan berdasarkan kesamaan konten film yang telah ditonton pengguna. Tujuan ini akan dicapai dengan menggunakan metode content-based filtering yang menganalisis kesamaan fitur seperti genre dan tag antara film.

- Menggunakan metode collaborative filtering untuk meningkatkan personalisasi rekomendasi dengan menganalisis pola interaksi pengguna terhadap berbagai film. Sistem ini akan memanfaatkan pendekatan Singular Value Decomposition (SVD) untuk mengidentifikasi preferensi implisit pengguna dan memberikan rekomendasi yang lebih akurat.


## Solution Approach

1. Content-Based Filtering:

    Pendekatan ini menggunakan informasi yang terdapat dalam deskripsi film, seperti genre dan tag, untuk menemukan film yang mirip dengan film yang sudah ditonton oleh pengguna. Algoritma ini bekerja dengan menganalisis kesamaan antara fitur-fitur tersebut menggunakan metode `cosine similarity` untuk menghasilkan rekomendasi yang relevan.

2. Collaborative Filtering

    Pendekatan ini menggunakan pola interaksi pengguna dengan berbagai film untuk memberikan rekomendasi. Dalam proyek ini, metode `Singular Value Decomposition (SVD)` digunakan untuk mendeteksi pola dalam preferensi pengguna, yang kemudian digunakan untuk merekomendasikan film.


## Data Understanding

Dataset yang digunakan dalam proyek ini adalah [MovieLens 20M](https://www.kaggle.com/datasets/grouplens/movielens-20m-dataset) dari Kaggle, yang terdiri dari 6 file CSV yang mencakup informasi mengenai film, tag, rating, dan relevansi tag. Dataset ini sangat kaya dengan sekitar 20 juta interaksi pengguna terhadap lebih dari 27.000 film, memberikan landasan yang kuat untuk mengembangkan sistem rekomendasi.

Data ini menggambarkan aktivitas pengguna yang memberikan rating dan tag pada film, dengan total 20 juta rating dan lebih dari 465.000 tag yang diterapkan. Dataset ini mencakup kontribusi dari lebih dari 138.000 pengguna yang aktif antara 9 Januari 1995 hingga 31 Maret 2015. Pengguna dalam dataset ini dipilih secara acak, dan setiap pengguna telah menilai setidaknya 20 film, memberikan wawasan yang mendalam tentang preferensi film mereka. Berdasarkan informasi pada halaman dataset ini terakhir diperbarui pada 17 Oktober 2016.

Namun, pada proyek ini hanya 3 file dataset yang akan digunakan, yaitu:

<!-- ### Variabel-variabel yang terdapat dalam dataset: -->

**1. movie.csv:**
| #   | Column  | Non-Null Count | Dtype  | Description        |
| --- | ------- | -------------- | ------ |-------------------|
| 0   | movieId | 27278 non-null | int64  | ID film.           |
| 1   | title   | 27278 non-null | object | Judul film.        |
| 2   | genres  | 27278 non-null | object | Genre film.        |

Memiliki 3 kolom dan data sebanyak 27.278 untuk masing-masing kolom. Tidak terdapat missing value dan duplicate.


**2. tag.csv:**

| #   | Column    | Non-Null Count | Dtype  | Description                            |
| --- | --------- | -------------- | ------ | -------------------------------------- |
| 0   | userId    | 465564 non-null | int64  | ID pengguna yang memberikan tag.       |
| 1   | movieId   | 465564 non-null | int64  | ID film yang ditag oleh pengguna.      |
| 2   | tag       | 465548 non-null | object | Tag yang diberikan oleh pengguna.      |
| 3   | timestamp | 465564 non-null | object | Waktu saat tag diberikan.              |

Memiliki 4 kolom dan data sebanyak 465.564 baris. Tidak ditemukan data duplicate, namun ditemukan adanya missing value pada data kolom tag sebanyak 16 baris data.

**3. rating.csv:**
| #   | Column    | Non-Null Count |Dtype   | Description                                      |
| --- | --------- | -------------- |------- | ------------------------------------------------ |
| 0   | userId    | 20000263 non-null |int64   | ID pengguna yang memberikan rating.              |
| 1   | movieId   | 20000263 non-null |int64   | ID film yang diberi rating.                      |
| 2   | rating    | 20000263 non-null |float64 | Nilai rating yang diberikan pengguna (skala 0.5 - 5.0). |
| 3   | timestamp | 20000263 non-null |object  | Waktu saat rating diberikan.                     |

 Memiliki 4 kolom dan data sebanyak 20.000.263 baris untuk masing-masing kolom. Tidak terdapat missing value dan duplicate.

### Exploratory Data Analysis

- Genres Distribution

  <!-- ![Genres Distribution](https://github.com/user-attachments/assets/9f705405-9ade-49ea-95b3-f67300acebd3) -->
  <img width="400" alt="Genres Distribution" src="https://github.com/user-attachments/assets/9f705405-9ade-49ea-95b3-f67300acebd3">

  Produksi film dengan genres drama merupakan genre film terbanyak dengan sekitar 1300 film dan diikuti comedy di posisi kedua sebanyak 8000 lebih film. Genre Drama dan Comedy memiliki perbedaan yang cukup signifikan dibandingkan dengan genre lainnya.

- Ratings Distribution

  <!-- ![Ratings Distribution](https://github.com/user-attachments/assets/9593dfb6-b814-480b-9777-5df89922cf93) -->
  <img width="400" alt="Ratings Distribution" src="https://github.com/user-attachments/assets/9593dfb6-b814-480b-9777-5df89922cf93">

  Kebanyakan pengguna memberikan rating dengan rentang 3 hingga 4 star. Mengindikasikan bahwa secara keseluruhan kualitas film sesuai dengan yang diharapkan oleh pengguna (konsumen).

- Trend Number of Ratings Based on Time

  <!-- ![Trend Number of Ratings Based on Time](https://github.com/user-attachments/assets/9fa17222-4bc1-4eb7-ba69-4c6cae062f9a) -->
  <img width="400" alt="Trend Number of Ratings Based on Time" src="https://github.com/user-attachments/assets/9fa17222-4bc1-4eb7-ba69-4c6cae062f9a">

  Pemberian rating terbanyak terjadi di tahun 2000 mencapai lebih dari 400.000 rating. Seiring bejalannya waktu mulai dari tahun 2005 pengguna mulai mengalami penurunan dalam pemberian rating.

## Data Preparation

- Normalization
  
  Membuat fungsi bernama `normalize_text`, yang berfungsi untuk:
    - Menghapus karakter | dan karakter lain yang tidak digunakan serta mengubah ke huruf kecil
      ```python
      text = text.replace('|', ' ').lower()
      ```
      Menggunakan metode replace() untuk mengganti karakter tertentu dengan spasi dan lower() untuk mengubah semua teks menjadi huruf kecil.

    - Menghapus tanda baca
      ```python
      text = text.translate(str.maketrans('', '', string.punctuation))
      ```      
      Menggunakan pustaka string dari Python untuk mengidentifikasi dan menghapus semua tanda baca dari teks.

    - Menghapus spasi yang berlebih
      ```python
      text = ' '.join(text.split())
      ```
      Menggunakan split() dan join() untuk menghapus spasi yang berlebih.

    - Melakukan lemmatization
      ```python
      text = ' '.join([lemmatizer.lemmatize(word) for word in text.split()])
      ```
      Menggunakan WordNetLemmatizer dari pustaka nltk untuk mengembalikan kata ke bentuk dasarnya.

    - Menghapus stopwords
      ```python
      text = ' '.join([word for word in text.split() if word not in stop_words])
      ```
      Menggunakan daftar stopwords dari nltk untuk menghapus kata-kata umum yang tidak memberikan banyak informasi.

    - Mengganti singkatan
      ```python
      text = text.replace("n't", " not").replace("'re", " are")
      ```
      Mengganti singkatan umum dalam teks seperti "n't" menjadi "not".

  Normalisasi dilakukan agar data teks terhindar dari karakter dan kata-kata yang tidak diperlukan untuk meningkatkan akurasi dan efisiensi dalam proses analisis serta pemodelan selanjutnya.


- Melakukan pengecekan kembali terhadap data, apakah terdapat data missing value maupun duplikat dengan menggunakan
    - duplicated().sum()
    - isna().sum()
  
  Setelah dilakukan pengecekan tidak ditemukan data yang missing value ataupun duplikat. Sehingga tidak diperlukan penghapusan data missing value dan duplikat. Alasan mengapa data yang tidak lengkap atau duplikat dapat menyebabkan model bias harus dihapus. Karena untuk memastikan model lebih stabil dan akurat dengan data yang bersih dan representatif.

- Menggunakan TF-IDF Vectorizer untuk mengubah deskripsi teks pada kolom `combined_clean` menjadi vektor numerik:
  ```python
  tfidf = TfidfVectorizer()
  tfidf_matrix = tfidf.fit_transform(con_bf['combined_clean'])
  ```


## Modeling

1. Content-Based Filtering:

    Content-based filtering bekerja dengan menganalisis fitur-fitur yang melekat pada film, yaitu genre dan tag untuk memberikan rekomendasi. Misalnya, jika pengguna menyukai film dengan genre "Action" dan tag "Hero," sistem akan mencari film lain yang memiliki kesamaan dalam genre dan tag tersebut.

    Implementasi model ini menggunakan data gabungan dari file `movie.csv` dan `tag.csv`. Menggunakan TF-IDF Vectorizer untuk menghilangkan mengubah deskripsi teks pada kolom `combined_features` menjadi vektor numerik pada proses sebelummnnya. Kesamaan antar-film dihitung menggunakan teknik `cosine similarity`, di mana film yang memiliki nilai kesamaan tertinggi dengan film yang telah ditonton pengguna akan direkomendasikan.

    Model ini menghasilkan daftar Top-N film yang dapat diatur sesuai dengan kebutuhan rekomendasikan untuk pengguna berdasarkan kesamaan konten. Sebagai contoh, jika seorang pengguna baru saja menonton "The Dark Knight" sistem mungkin merekomendasikan "Justice League" atau "LEGO Batman" karena kesamaan dalam genre dan tag.
    
    Lihat hasil yang direkomendasikan berikut:

    ![Rekomendasi Content Based Filtering](https://github.com/user-attachments/assets/e2d1c525-7bdd-45a4-b306-f0d503cd6669)
    <!-- <img width="500" alt="image" src="https://github.com/user-attachments/assets/838052da-6e27-4b4d-a78e-bb074422344f"> -->

      **Kelebihan Cosine Similarity:**

      - Mengukur kesamaan arah, tidak terpengaruh oleh ukuran vektor.
      - Efektif pada data dengan banyak nilai nol, seperti teks.
      - Konsep dan perhitungan yangsederhana.
      - Efektif meski panjang konten bervariasi.

      **Kekurangan Cosine Similarity:**

      - Tidak mempertimbangkan ukuran vektor.
      - Tidak menangkap hubungan kompleks atau non-linier.
      - Tidak menangani perbedaan skala antar fitur.
      - Sensitif terhadap fitur ekstrem (outlier) yang mungkin mengganggu hasil.

2. Collaborative Filtering

      Collaborative filtering menggunakan pola interaksi pengguna lain yang memiliki preferensi serupa untuk memberikan rekomendasi. Alih-alih hanya mengandalkan kesamaan konten, pendekatan ini mencari kesamaan dalam perilaku pengguna, seperti film yang mereka beri rating tinggi.

      Implementasi pendekatan ini menggunakan data gabungan dari `movie.csv` dan `rating.csv`. Model Singular Value Decomposition (SVD) digunakan untuk memprediksi film yang mungkin disukai oleh pengguna. SVD bekerja dengan mendekonstruksi matriks rating pengguna-film menjadi komponen yang lebih kecil, memungkinkan sistem untuk mengidentifikasi preferensi tersembunyi dan kesamaan antar pengguna berdasarkan pola rating yang serupa.

      Sistem ini kemudian menghasilkan daftar Top-N film yang dapat diatur sesui dengan kebutuhan rekomendasikan untuk pengguna berdasarkan perilaku pengguna lain yang serupa. Misalnya, jika pengguna A dan pengguna B memiliki rating yang mirip untuk beberapa film, dan pengguna B menyukai film yang belum ditonton oleh pengguna A, film tersebut akan direkomendasikan kepada pengguna A.

      Lihat hasil yang direkomendasikan berikut:

      ![Rekomendasi Collaborative Filtering](https://github.com/user-attachments/assets/f3079d1c-838e-475d-825c-299e6d20eb4b)
      <!-- <img width="262" alt="image" src="https://github.com/user-attachments/assets/f3079d1c-838e-475d-825c-299e6d20eb4b"> -->
      
      **Kelebihan SVD:**
      
      - Mengurangi dimensi data, sehingga lebih efisien menangani data yang jarang (sparse).
      - Memperbaiki prediksi dengan menemukan pola tersembunyi dalam data pengguna dan item.
      - Mengurangi jumlah fitur, membuat model lebih sederhana dan lebih cepat.
      - Mampu menghasilkan rekomendasi yang lebih personal berdasarkan preferensi tersembunyi.

      **Kekurangan SVD:**
      - Memerlukan data yang sudah diisi lengkap (non-sparse), sehingga perlu teknik imputasi data yang tepat.
      - Menghitung dekomposisi matriks besar membutuhkan sumber daya komputasi yang signifikan.
      - Kurang cocok untuk data yang sering berubah, seperti penambahan pengguna atau item baru.
      - Hanya menangkap hubungan linier, kurang efektif jika ada pola non-linear dalam data.

## Evaluation

### Content-Based Filtering

  Untuk Content Based filtering menggunakan metrik Precission. Metrik ini digunakan untuk mengukur akurasi sistem rekomendasi. Precision mengukur seberapa banyak item yang direkomendasikan atau diklasifikasikan sebagai positif yang benar-benar relevan atau positif.

  Formula Precission:

  <!-- ![image](https://github.com/user-attachments/assets/0ea14dd8-b8a5-4236-be77-6ab779c4b83e) -->
  <img width="173" alt="image" src="https://github.com/user-attachments/assets/0ea14dd8-b8a5-4236-be77-6ab779c4b83e">

  **Cara Kerja:**

  - True Positives (TP): Jumlah item relevan yang benar-benar direkomendasikan atau diklasifikasikan sebagai positif.
  - False Positives (FP): Jumlah item yang tidak relevan tetapi salah diklasifikasikan sebagai positif atau direkomendasikan.
  -nPerhitungan: Precision dihitung dengan membagi jumlah TP dengan jumlah total item yang direkomendasikan (TP + FP). Hasilnya menunjukkan proporsi rekomendasi yang benar-benar relevan.

   **Hasil:**
  | **Precission** |
  |----------|
  | 1.0    |

  Precision sebesar 1.0, artinya semua film yang direkomendasikan memiliki kemiripan yang tinggi dengan film dasar dalam hal konten yang dianalisis, sehingga semua rekomendasi dianggap relevan dan sesuai dengan preferensi yang diukur. Bisa dikatakan 

### Collaborative Filtering

  Untuk collaborative filtering digunakan metode `Singular Value Decomposition (SVD)` dan metrik evaluasi yang dipakai adalah `Root Mean Square Error (RMSE)`. RMSE mengukur seberapa dekat prediksi rating film dengan rating asli yang diberikan oleh pengguna.
  
  Formula RMSE sebagai berikut:

  <img width="173" alt="image" src="https://github.com/user-attachments/assets/c12c3edc-1761-4838-aad1-380625b4f3b0">
  <!-- ![Rumus RMSE](https://latex.codecogs.com/png.latex?\text{RMSE}=\sqrt{\frac{1}{n}\sum_{i=1}^{n}\left(\hat{r}_i-r_i\right)^2}) -->
    
  Di mana:

  - r̂i: rating yang diprediksi oleh model untuk pengguna dan film tertentu.
  - ri: rating asli yang diberikan oleh pengguna.
  - n : jumlah total prediksi yang dievaluasi.

  **Cara Kerja RMSE:**

  - Untuk setiap prediksi yang dihasilkan oleh model, hitung selisih antara nilai yang diprediksi dan nilai asli (rating sebenarnya). Selisih ini dikenal sebagai kesalahan prediksi.
      
    <img width="133" alt="image" src="https://github.com/user-attachments/assets/d7baa12c-eb3e-461a-8a79-8b2d9848ab13">
    <!-- Kesalahan = r̂i -ri -->
      
  - Kuadratkan setiap kesalahan prediksi untuk menghilangkan tanda negatif dan memberikan bobot lebih pada kesalahan yang lebih besar.

    <img width="71" alt="image" src="https://github.com/user-attachments/assets/ec9734db-354c-4b09-9ad4-43018807c672">
    <!-- (r̂i -ri)² -->

  - Hitung rata-rata dari semua kesalahan kuadrat (MSE). Memberikan ukuran umum dari kesalahan prediksi model, tanpa mempertimbangkan arah kesalahan (lebih tinggi atau lebih rendah dari nilai sebenarnya).
  
    <img width="158" alt="image" src="https://github.com/user-attachments/assets/5ffc5f14-5878-492b-b7ed-9381ade530b5">

  - Ambil akar kuadrat dari nilai Mean Squared Error (MSE) untuk mengembalikan ukuran kesalahan ke unit yang sama dengan nilai asli (rating) dan menghasilkan RMSE.

    <img width="227" alt="image" src="https://github.com/user-attachments/assets/d907062a-9905-4f3d-9a1e-ec48eff2746c">

  **Interpretasi RMSE:**

  - Nilai RMSE yang lebih rendah, menunjukkan bahwa model lebih akurat dalam memprediksi nilai asli, karena kesalahan prediksi rata-rata lebih kecil.
  - Nilai RMSE yang lebih tinggi, menunjukkan bahwa model kurang akurat, karena kesalahan prediksi rata-rata lebih besar.
  - Pengaruh kesalahan: RMSE memberikan bobot lebih besar pada kesalahan yang lebih besar karena kesalahan dikuadratkan. Ini berarti bahwa kesalahan akan mempengaruhi RMSE lebih signifikan daripada kesalahan kecil.

  **Hasil:**
  | **RMSE** |
  |----------|
  | 0.288    |

  RMSE (Root Mean Square Error) sebesar 0.288 menunjukkan bahwa rata-rata kesalahan antara prediksi dan nilai sebenarnya (rating yang diberikan pengguna) adalah sekitar 0.288. Menunjukkan bahwa prediksi sistem cukup dekat dengan nilai yang diharapkan dan sudah cukup baik. BIsa dikatakan model berhasil memberikan rekomendasi yang cukup relevan. Namun masih perlu ditingkatkan lagi agar mendapatkan nilai yang lebih kecil atau mendekati nol.


## Conclussion

- Sistem rekomendasi dengan Content Based dan Collaborative Filtering sudah berhasil memberikan rekomendasi film sesuai dengan problem statement dan goal yang dicapai dengan evaluasi sebagai berikut:
  - Content-Based Filtering:

    Precission: **1.0**

  - Collaborative Filtering:

    RMSE: **0.288**

  Menunjukkan bahwa model pada Content Based Filtering sudah baik baik dan Collaborative Filtering juga sudah cukup baik. Namun untuk Collaborative Filtering masih perlu dilakukan eksperimen lebih lanjut agar nilai RMSE menjadi lebih kecil atau mendekati nol. 

- Menggabungkan kedua strategi ini memungkinkan kita untuk mengembangkan sistem rekomendasi yang lebih andal dan serbaguna. Content-Based Filtering berfokus pada rekomendasi yang didasarkan pada karakteristik internal dari item itu sendiri, sedangkan Collaborative Filtering lebih efektif dalam mengidentifikasi pola preferensi pengguna melalui analisis data interaksi yang ada. Dengan memahami manfaat dan keterbatasan dari masing-masing metode, kita dapat memilih pendekatan yang paling cocok untuk memenuhi kebutuhan dan konteks khusus dari sistem rekomendasi yang dikembangkan. Memanfaatkan kedua metode ini secara bersamaan dapat meningkatkan akurasi dan relevansi rekomendasi, sehingga menawarkan pengalaman yang lebih memuaskan bagi pengguna.

## Reference

[^1]: Meel, P., et al. "Movie Recommendation Using Content-Based and Collaborative Filtering". 2020. SpringerLink. [Link Available](https://link.springer.com/chapter/10.1007/978-981-15-5113-0_22)

[^2]: Koren, Y., et al. "Matrix Factorization Techniques for Recommender Systems". 2009. IEEE. DOI: [10.1109/MC.2009.263](https://doi.org/10.1109/MC.2009.263)