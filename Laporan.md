# Laporan Proyek Machine Learning Terapan - Achmad Fauzihan Bagus Sajiwo

<div align="center">
	<p>MOVIE - RECOMMENDATION SYSTEM</p>
</div>

<div align="center">
	<img src="https://github.com/fabasassa-lab/Movie_Recommendation_System/blob/main/images/movie.jpeg?raw=true">
</div>

## Project Overview

Dengan pertumbuhan pesat industri hiburan digital, pengguna dihadapkan pada ribuan pilihan film dan serial setiap hari. Platform seperti Netflix, Hulu, dan Disney+ menyediakan beragam konten, yang justru menimbulkan fenomena yang disebut sebagai information overload atau kelebihan informasi. Oleh karena itu, sistem rekomendasi menjadi komponen penting dalam meningkatkan pengalaman pengguna dengan menyaring dan menyajikan konten yang sesuai dengan preferensi individu.

Sistem rekomendasi film tidak hanya membantu pengguna menemukan film yang relevan, tetapi juga berkontribusi pada peningkatan waktu tonton dan retensi pelanggan. Studi oleh Gomez-Uribe & Hunt (2015) [1] yang dilakukan di Netflix menunjukkan bahwa sekitar 75% dari tayangan berasal dari sistem rekomendasi mereka. Hal ini menunjukkan pentingnya sistem yang mampu memahami pola dan minat pengguna secara akurat.

Pendekatan tradisional seperti content-based filtering dan collaborative filtering telah digunakan secara luas, namun memiliki keterbatasan dalam hal sparsity data dan cold-start problem. Untuk mengatasi tantangan tersebut, pendekatan deep learning telah menjadi solusi alternatif yang menjanjikan. Model deep learning seperti neural collaborative filtering (NCF) dapat menangkap hubungan non-linear antara pengguna dan item (film) yang tidak dapat ditangkap oleh metode klasik (He et al., 2017) [2].

Referensi dari proyek ini adalah sebagai berikut:

[The Netflix recommender system: Algorithms, business value, and innovation](https://dl.acm.org/doi/10.1145/2843948) [1]

[Neural collaborative filtering](https://dl.acm.org/doi/10.1145/3038912.3052569) [2]

## Business Understanding

Pada bagian ini, akan menjelaskan mengenai proses klarifikasi masalah yang terdiri dari _Problem Statement_, _Goals_ dan _Solution Statements_.

### Problem Statements

Bagaimana cara merekomendasikan film yang disukai oleh pengguna lain agar dapat direkomendasikan secara efektif kepada pengguna lainnya? Permasalahan ini muncul karena banyaknya pilihan film yang tersedia, sementara pengguna sering kali mengalami kesulitan dalam menemukan film yang sesuai dengan preferensi mereka secara cepat dan tepat.

### Goals

Tujuan dari proyek ini adalah membangun sistem rekomendasi film yang akurat dengan memanfaatkan data rating serta aktivitas pengguna pada masa lalu. Sistem ini diharapkan dapat membantu pengguna dalam menemukan film yang relevan dengan preferensinya secara efisien, serta meningkatkan pengalaman pengguna secara keseluruhan.

### Solution statements

Solusi yang ditawarkan dalam proyek ini adalah dengan mengimplementasikan dua algoritma machine learning, yaitu Content-Based Filtering dan Collaborative Filtering. 

- Collaborative Filtering:
	Algoritma ini menggunakan pendekatan berdasarkan perilaku pengguna sebelumnya, seperti riwayat pemberian rating atau interaksi terhadap film tertentu. Dengan menganalisis pola kesamaan antara pengguna, sistem dapat memprediksi dan merekomendasikan film yang disukai oleh pengguna lain yang memiliki preferensi serupa. Pendekatan ini efektif untuk mengidentifikasi minat kolektif dari komunitas pengguna.

- Content-Based Filtering:
	Algoritma ini merekomendasikan film kepada pengguna berdasarkan kesamaan karakteristik antar item (film), seperti genre, sutradara, pemeran, atau sinopsis. Sistem menganalisis film-film yang disukai oleh pengguna di masa lalu, lalu mencari film lain dengan konten yang serupa. Dengan demikian, rekomendasi yang dihasilkan bersifat personal dan relevan dengan preferensi unik setiap pengguna.


## Data Understanding
Data yang digunakan dalam proyek ini adalah data **Movies & Ratings for Recommendation System** yang dapat diunduh dari situs [Kaggle](https://www.kaggle.com/datasets/nicoletacilibiu/movies-and-ratings-for-recommendation-system).

### Variabel-variabel pada Movies & Ratings for Recommendation System dataset adalah sebagai berikut:

1. Movie	
- Judul movie yang tersedia

2. Rating	
- Daftar penilaian dari user mengenai movie yang tersedia

### Explanatory Data Analysis

1. Distribusi Stroke Risk

![stroke_risk](https://github.com/fabasassa-lab/Stroke-Risk-Prediction/blob/main/image/risk.png?raw=true)

Pada Gambar 1, _plot_ di atas diperlihatkan bahwa data yang risk statusnya 0 (No) lebih banyak daripada data yang risk statusnya 1 (Yes).

2. Distribusi Usia
 
![age_distribution](https://github.com/fabasassa-lab/Stroke-Risk-Prediction/blob/main/image/age_distribution.png?raw=true)

Pada Gambar 2, _plot_ di atas melihatkan distribusi usia pada dataset **Stroke Risk Prediction Dataset based on Literature**. Usia paling banyak terdapat pada rentang 30-34 tahun.

3. Distribusi Gender vs Risk
 
![gender_risk](https://github.com/fabasassa-lab/Stroke-Risk-Prediction/blob/main/image/gender_risk.png?raw=true)

Pada Gambar 3, _plot_ di atas melihatkan distribusi gender pada dataset **Stroke Risk Prediction Dataset based on Literature**. Gender yang terkena penyakit stroke kebanyakan dari gender male.

4. Correlation Matrix

![cm_analysis](https://github.com/fabasassa-lab/Stroke-Risk-Prediction/blob/main/image/cm_analysis.png?raw=true)

Pada Gambar 4, _plot_ di atas melihatkan observasi korelasi antara fitur _numerical_ dengan fitur target

## Data Preparation

1. Seleksi Data
- Pada tahap awal, dilakukan pemeriksaan terhadap nilai yang hilang (missing values) di setiap kolom dataset. Jika ditemukan, nilai tersebut dapat diatasi dengan metode seperti imputasi (mean, median, modus) atau dihapus tergantung pada proporsi dan pentingnya kolom tersebut.
- Alasan: Missing values dapat menyebabkan error saat pelatihan model atau menghasilkan hasil yang bias jika tidak ditangani dengan tepat.

2. Label Encoding
- Variabel kategorik seperti gender dikonversi ke dalam bentuk numerik menggunakan metode Label Encoding agar bisa digunakan oleh algoritma pembelajaran mesin.
- Alasan: Sebagian besar algoritma machine learning tidak dapat bekerja langsung dengan data kategorik, sehingga perlu diubah ke dalam representasi numerik.

3. Feature Selection
- Pemilihan fitur dilakukan untuk menyaring variabel-variabel yang benar-benar berkontribusi terhadap prediksi atau **redundan**. Misalnya dengan menghindari fitur yang memiliki korelasi sangat tinggi satu sama lain atau yang tidak memiliki hubungan dengan variabel target at_risk.
- Alasan: Feature selection bertujuan untuk meningkatkan akurasi model, menghindari overfitting, dan mempercepat waktu pelatihan dengan hanya menyertakan fitur yang penting.

4. Splitting Data
- Dataset dibagi menjadi dua bagian: data latih (train) dan data uji (test), biasanya dengan perbandingan 80:20.
- Alasan: Tujuannya adalah untuk mengevaluasi kemampuan generalisasi model. Model dilatih pada data latih dan dievaluasi pada data uji yang tidak pernah dilihat sebelumnya.

## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Tahapan ini menggunakan tiga algoritma, yaitu **KNN**, **Random Forest** dan **AdaBoost**. Hasil akhirnya adalah untuk mencari model terbaik sebagai solusi.

**KNN**

- **Cara kerja** : Dalam membangun model **KNN (K-Nearest Neighbors)**, digunakan module KNeighborsClassifier dari library sklearn. Digunakan parameter n_neighbors=5 dan weights='uniform' untuk membangun model. Untuk melakukan training, digunakan .fit(X_train, y_train) untuk fitting. Kemudian, untuk melakukan prediksi, digunakan .predict(X_test).

- Kelebihan:
	- Mudah dipahami dan diimplementasikan: KNN merupakan salah satu algoritma yang paling sederhana dan mudah dipahami.
	- Non-parametric: KNN tidak membuat asumsi tentang distribusi data, sehingga sangat berguna untuk data yang tidak memiliki distribusi tertentu.
	- Dapat digunakan untuk klasifikasi dan regresi: Meskipun lebih sering digunakan untuk klasifikasi, KNN juga bisa digunakan untuk regresi.
	- Adaptif dengan data baru: KNN dapat segera diadaptasi dengan data baru tanpa memerlukan pelatihan ulang.
- Kekurangan:
	- Kompleksitas tinggi saat data besar: KNN membutuhkan waktu komputasi yang lama pada dataset yang besar karena harus menghitung jarak antara titik data dengan semua data lainnya.
	- Sensitif terhadap fitur yang tidak relevan: Kinerja KNN dapat sangat dipengaruhi oleh data fitur yang tidak relevan atau memiliki skala yang berbeda.
	- Memerlukan memori besar: KNN membutuhkan penyimpanan seluruh dataset karena memerlukan data tersebut untuk melakukan prediksi.
	-Skalabilitas buruk: Dengan bertambahnya data, KNN mengalami kesulitan dalam hal kecepatan dan performa.

**Random Forest**

- **Cara kerja** : Dalam membangun model **Random Forest**, digunakan module RandomForestClassifier dari library sklearn. Digunakan parameter n_estimators=100, max_depth=None dan random_state=42 untuk membangun model. Untuk melakukan training, digunakan .fit(X_train, y_train) untuk fitting. Kemudian, untuk melakukan prediksi, digunakan .predict(X_test).

- Kelebihan:
	- Kinerja yang baik pada dataset besar: Random Forest adalah algoritma ensemble yang terdiri dari banyak pohon keputusan dan dapat menangani dataset besar dengan baik.
	- Robust terhadap overfitting: Karena menggunakan metode bootstrap aggregation (bagging), Random Forest cenderung lebih tahan terhadap overfitting dibandingkan pohon keputusan tunggal.
	-Dapat menangani data yang hilang (missing data): Random Forest dapat mengatasi data yang hilang tanpa memerlukan imputasi atau pengisian data yang hilang.
	- Menangani data yang sangat tidak seimbang dengan baik: Random Forest dapat menangani masalah kelas yang tidak seimbang dengan lebih baik.
- Kekurangan:
	- Kebutuhan komputasi tinggi: Model Random Forest membutuhkan lebih banyak sumber daya komputasi dan waktu pelatihan, terutama dengan jumlah pohon yang sangat banyak.
	- Kurang interpretatif: Model Random Forest menghasilkan banyak pohon keputusan, yang membuatnya lebih sulit untuk diinterpretasikan dibandingkan dengan model pohon keputusan tunggal.
	- Tidak cocok untuk masalah dengan data spasial atau urut (sequential data): Random Forest tidak dapat menangani urutan waktu atau data yang berhubungan secara spasial secara efektif.

**AdaBoost**

- **Cara kerja** : Dalam membangun model **AdaBoost**, digunakan module AdaBoostClassifier dari library sklearn. Digunakan parameter n_estimators=50, learning_rate=1.0, dan random_state=42 untuk membangun model. Untuk melakukan training, digunakan .fit(X_train, y_train) untuk fitting. Kemudian, untuk melakukan prediksi, digunakan .predict(X_test).

- Kelebihan:
	- Meningkatkan kinerja model lemah: AdaBoost meningkatkan performa model dasar (weak learners) dengan menggabungkan hasil prediksi beberapa model.
	- Tahan terhadap overfitting: Pada dataset dengan ukuran kecil hingga sedang, AdaBoost cenderung lebih tahan terhadap overfitting.
	- Kemampuan untuk menangani data yang kompleks: AdaBoost bisa menangani data dengan distribusi yang kompleks.
	- Memperbaiki kesalahan model sebelumnya: Dengan memfokuskan lebih banyak perhatian pada data yang salah diklasifikasikan oleh model sebelumnya, AdaBoost dapat memberikan hasil yang lebih baik.
- Kekurangan:
	- Sensitif terhadap outlier: AdaBoost dapat menjadi sangat sensitif terhadap outlier karena memberikan bobot yang lebih besar pada data yang sulit untuk diklasifikasikan.
	- Memerlukan banyak iterasi: Kadang-kadang AdaBoost membutuhkan banyak iterasi untuk memberikan hasil yang baik, yang bisa mempengaruhi waktu pelatihan.
	- Rentan terhadap model dasar yang lemah: Jika model dasar (weak learner) yang digunakan terlalu sederhana atau tidak cukup kuat, AdaBoost mungkin tidak menghasilkan model yang baik.

## Evaluation
Dalam proyek ini, akurasi digunakan sebagai metrik evaluasi utama untuk mengukur kinerja setiap model dalam klasifikasi penyakit stroke. Akurasi mengukur persentase prediksi yang benar dari total prediksi yang dilakukan oleh model.

Akurasi (Accuracy):

- Akurasi mengukur proporsi prediksi yang benar terhadap total prediksi yang dilakukan. Ini adalah metrik yang sangat umum digunakan dalam masalah klasifikasi. Akurasi dihitung dengan rumus:

<div align="center">
	<img src="https://github.com/fabasassa-lab/Stroke-Risk-Prediction/blob/main/image/akurasi.png?raw=true">
</div>

Dimana:

- Jumlah Prediksi yang Benar adalah jumlah prediksi yang sesuai dengan label yang sebenarnya (true positives + true negatives).
- Jumlah Total Data adalah jumlah total sampel data yang diprediksi (termasuk yang benar dan yang salah)​
 
Pada kasus ini, akurasi digunakan untuk menilai seberapa baik model dapat memprediksi status "at_risk" (mempunyai kemungkinan terkena stroke atau tidak) berdasarkan data yang tersedia.

<div align="center">
	<img src="https://github.com/fabasassa-lab/Stroke-Risk-Prediction/blob/main/image/nilai.png?raw=true">
</div>

Pada Gambar di atas, _plot_ yang disajikan di atas, dapat diketahui bahwa model **Random Forest** memberikan nilai akurasi yang paling tinggi. Sehingga, model **Random Forest** lah yang dipilih sebagai model terbaik untuk melakukan klasifikasi penyakit stroke.

Tabel 1. Hasil Evaluasi Model
|                 | train	  |	test        |
|-----------------|-----------|-------------|
|KNN		      | 0.933464  |	0.903571    |
|AdaBoost	      | 0.933857  |	0.934286    |
|RandomForest	  | 1.0  |	0.973286    |

Hasil dari _modeling_ dapat dilihat pada Tabel 1. Tabel diatas memberikan informasi detail terkait hasil _training_ dan _testing_

Tabel 2. Hasil Prediksi

|    | y_true |	prediksi_KNN | prediksi_AdaBoost     | prediksi_RandomForest |
|----|--------|--------------|-----------------------|-----------------------|
|17813  | 1      | 1          | 0                   | 0                   |
|6857| 0      | 0          | 0                   | 0                   |
|7672| 1      | 1          | 1                   | 1                   |
|9704| 1      | 1          | 1                   | 1                   |
|14303| 0      | 0          | 0                   | 0                   |
|26304| 1      | 1          | 1                   | 1                   |
|3202| 0      | 0          | 0                   | 0                   |
|27310| 0      | 0          | 0                   | 0                   |
|11215| 0      | 0          | 0                   | 0                   |
|20490| 0      | 0          | 0                   | 0                   |

Pada Tabel 2, disajikan informasi hasil prediksi dari model yang digunakan. Dari tabel yang disajikan dapat dilihat bahwa prediksi menggunakan **Random Forest**, **KNN** maupun **AdaBoost** memiliki hasil sesuai dengan data aslinya _`y_true`_. Melihat hasil prediksi dan nilai akurasi yang telah didapat, model **Random Forest** lah yang dipilih sebagai model terbaik untuk melakukan klasifikasi penyakit stroke. Dan melihat dari keberhasilan prediksi menggunakan **Random Forest** maka proyek ini mampu dan berhasil menyelesaikan _Goals_ yang diinginkan.

**---Akhir Laporan---**

_Github:_
https://github.com/fabasassa-lab/Movie_Recommendation_System

_Referensi:_
[1] Gomez-Uribe, C. A., & Hunt, N. (2015). The Netflix recommender system: Algorithms, business value, and innovation. ACM Transactions on Management Information Systems (TMIS), 6(4), 1–19. https://doi.org/10.1145/2843948

[2] He, X., Liao, L., Zhang, H., Nie, L., Hu, X., & Chua, T. S. (2017). Neural collaborative filtering. Proceedings of the 26th International Conference on World Wide Web (WWW '17), 173–182. https://doi.org/10.1145/3038912.3052569

[3] movies-and-ratings-for-recommendation-system. https://www.kaggle.com/datasets/nicoletacilibiu/movies-and-ratings-for-recommendation-system
