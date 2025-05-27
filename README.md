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

Tujuan dari proyek ini adalah membuat sistem rekomendasi film yang akurat dengan memanfaatkan data rating serta aktivitas pengguna pada masa lalu. Sistem ini diharapkan dapat membantu pengguna dalam menemukan film yang relevan dengan preferensinya secara efisien, serta meningkatkan pengalaman pengguna secara keseluruhan.

### Solution statements

Solusi yang ditawarkan dalam proyek ini adalah dengan mengimplementasikan dua algoritma machine learning, yaitu Content-Based Filtering dan Collaborative Filtering. 

- Collaborative Filtering:
	Algoritma ini menggunakan pendekatan berdasarkan perilaku pengguna sebelumnya, seperti riwayat pemberian rating atau interaksi terhadap film tertentu. Dengan menganalisis pola kesamaan antara pengguna, sistem dapat memprediksi dan merekomendasikan film yang disukai oleh pengguna lain yang memiliki preferensi serupa. Pendekatan ini efektif untuk mengidentifikasi minat kolektif dari komunitas pengguna.

- Content-Based Filtering:
	Algoritma ini merekomendasikan film kepada pengguna berdasarkan kesamaan karakteristik antar item (film), seperti genre, sutradara, pemeran, atau sinopsis. Sistem menganalisis film-film yang disukai oleh pengguna di masa lalu, lalu mencari film lain dengan konten yang serupa. Dengan demikian, rekomendasi yang dihasilkan bersifat personal dan relevan dengan preferensi unik setiap pengguna.


## Data Understanding
Data yang digunakan dalam proyek ini adalah data **Movies & Ratings for Recommendation System** yang dapat diunduh dari situs [Kaggle](https://www.kaggle.com/datasets/nicoletacilibiu/movies-and-ratings-for-recommendation-system).

### Variabel-variabel pada Movies & Ratings for Recommendation System dataset adalah sebagai berikut:

1. Movie : Daftar movie yang tersedia
	- movieId : merupakan id (penanda) pada setiap movie (9742 data)
	- title : merupakan judul movie (9742 data)
	- genres : merupakan genre movie (9742 data)

2. Rating : Daftar penilaian dari user mengenai movie yang tersedia
	- userId : merupakan id (penanda) pada setiap user (100836 data)
	- movieId : merupakan id (penanda) pada setiap movie (100836 data)
	- rating : merupakan penilaian yang diberi oleh user (100836 data)
	- timestamp : merupakan catatan digital (100836 data)

### Explanatory Data Analysis

1. Movie

Gambar 1. Contoh Data Movies.

| ![movie](https://github.com/fabasassa-lab/Movie_Recommendation_System/blob/main/images/movh.png?raw=true) |

Pada Gambar 1, _table_ di atas diperlihatkan mengenai contoh data yang terdapat pada dataset movies.

2. Rating

Gambar 2. Contoh Data Ratings.

![rath](https://github.com/fabasassa-lab/Movie_Recommendation_System/blob/main/images/rath.png?raw=true)

Pada Gambar 2, _table_ di atas diperlihatkan mengenai contoh data yang terdapat pada dataset ratings.

Gambar 3. Table Distribusi Data Ratings.

![ratd](https://github.com/fabasassa-lab/Movie_Recommendation_System/blob/main/images/ratd.png?raw=true)

Pada Gambar 3, _table_ di atas diperlihatkan mengenai distribusi data yang terdapat pada dataset ratings. Dari _table_ di atas, diketahui bahwa nilai maksimum rating adalah 5 dan nilai minimumnya adalah 0. Artinya, skala rating berkisar antara 0 hingga 5.

Gambar 4. Plot Distribusi Ratings.

![plot](https://github.com/fabasassa-lab/Movie_Recommendation_System/blob/main/images/plot.png?raw=true)

Pada Gambar 4, _plot_ di atas melihatkan distribusi rating pada dataset **Movie Recommendation System**. Rating paling banyak terdapat pada rentang 4.


## Data Preparation

1. Menggabungkan Data
- Pada tahap awal, dilakukan proses penggabungan beberapa dataset, yaitu data film dan data rating.
- Alasan: Penggabungan data dilakukan untuk menyatukan informasi dari berbagai sumber

2. Mengurutkan Data
- Melakukan proses pengurutan data untuk mempermudah analisis dan pemrosesan selanjutnya.
- Alasan: Mempermudah proses analisis, mengidentifikasi pola penting, serta meningkatkan efisiensi saat membangun dan mengevaluasi model rekomendasi.

3. Konversi Data to List
- Melakukan proses konversi data ke dalam bentuk list (daftar). Konversi ini dilakukan untuk menyiapkan data dalam format yang dapat diterima oleh algoritma
- Alasan: Proses pelatihan model atau evaluasi terkadang lebih mudah jika data telah dikonversi ke bentuk dasar seperti list atau array numpy.

4. Membuat Dictionary
- Memetakan nilai asli dari suatu kolom (seperti ID pengguna atau ID film) ke dalam bentuk numerik yang dapat digunakan dalam model
- Alasan: Agar kita bisa mengubah kembali hasil prediksi ke bentuk ID atau nama film yang dikenali pengguna.

5. TF-IDF Vectorizer
- Mengubah kolom genre menjadi vektor numerik dan menghitung kemiripan antar film berdasarkan konten (fitur teks), seperti genre.
- Alasan: TF-IDF membantu model memahami bahwa dua film bisa mirip karena memiliki genre atau deskripsi yang serupa, sehingga cocok direkomendasikan ke pengguna yang menyukai salah satunya.

6. Encoding
- mengubah userId (yang berupa teks atau angka yang kompleks) menjadi representasi numerik yang lebih sederhana dan unik.
- Alasan: Memudahkan proses dalam model rekomendasi dengan menggunakan angka sebagai representasi userId daripada teks.

7. Splitting Data
- Dataset dibagi menjadi dua bagian: data latih (train) dan data uji (test), biasanya dengan perbandingan 80:20.
- Alasan: Tujuannya adalah untuk mengevaluasi kemampuan generalisasi model. Model dilatih pada data latih dan dievaluasi pada data uji yang tidak pernah dilihat sebelumnya.

## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Tahapan ini menggunakan dua algoritma, yaitu **Content Based Filtering** dan **Collaborative Filtering**. Hasil akhir yang diharapkan dari sistem rekomendasi ini adalah dapat memudahkan pengguna untuk mencari film yang diinginkan, baik berdasarkan preferensi film yang serupa, ataupun rekomendasi berdasarkan rating.

**Content Based Filtering**

- **Cara kerja** : Dalam membangun model **Content Based Filtering**, digunakan module TfidfVectorizer dari library sklearn. Mengekstraksi fitur konten (misalnya genre). Merepresentasi fitur menggunakan TF-IDF Vectorizer.  Menghitung Cosine Similarity antar film. Mencari film yang paling mirip (berdasarkan nilai cosine similarity). Mengembalikan Top-k film yang mirip dengan nama_movie. Pada fungsi tersebut juga ditetapkan k = 5 yang berarti akan mengeluarkan rekomendasi 5 film teratas berdasarkan genre.

Tabel 1. **Movie** yang disukai oleh pengguna dimasa lalu.

|      | id     | movie_name            | genre                   |
|------|--------|-----------------------|-------------------------|
| 8482 | 113604 | If I Stay (2014) | Drama |

Berdasarkan Tabel 1, terlihat bahwa pengguna menyukai film berjudul If I Stay (2014 yang memiliki genre Drama.
Sistem kemudian memberikan rekomendasi film lain yang memiliki kemiripan dengan If I Stay (2014).


Tabel 2. Rekomendasi movie yang mirip dengan **If I Stay (2014)**

|   | movie_name                                       | genre            | 
|---|--------------------------------------------------|------------------|
| 0 | Monsieur Ibrahim (Monsieur Ibrahim et les fleu... | Drama |
| 1 | Legend of 1900, The (a.k.a. The Legend of the ... | Drama |
| 2 | Away from Her (2006)                            | Drama |
| 3 | Limbo (1999                                  | Drama |
| 4 | Kiss of the Spider Woman (1985)	       | Drama |

Berdasarkan Tabel 2, dapat diketahui bahwa pengguna memiliki ketertarikan pada film berjudul If I Stay (2014) yang mengusung genre Drama.
Oleh karena itu, sistem merekomendasikan film-film lain yang memiliki karakteristik serupa dengan If I Stay (2014).

- Kelebihan **Content Based Filtering**:
	- Personalized: Rekomendasi benar-benar disesuaikan dengan preferensi unik setiap pengguna berdasarkan riwayat mereka sendiri, tanpa perlu data pengguna lain.
	- Tidak Bergantung pada Jumlah Pengguna: Tetap bisa bekerja meskipun hanya ada sedikit pengguna (tidak membutuhkan komunitas besar).
	- Bisa Merekomendasikan Item Baru (Cold Start untuk Item): Selama item tersebut memiliki informasi fitur yang lengkap (misalnya genre, deskripsi, aktor), sistem tetap bisa memberikan rekomendasi, meski belum pernah dirating oleh pengguna lain..
- Kekurangan **Content Based Filtering**:
	- Cenderung Terbatas (Overspecialization): Rekomendasi bisa menjadi terlalu mirip dengan item sebelumnya, membuat pengguna tidak menemukan hal baru (kurang keberagaman).
	- Cold Start untuk Pengguna Baru: Sulit memberikan rekomendasi jika pengguna belum memiliki riwayat interaksi atau rating sebelumnya.
	- Ketergantungan pada Fitur: Kualitas rekomendasi sangat tergantung pada kualitas dan kelengkapan informasi fitur item (genre, sinopsis, aktor, dll). Jika datanya terbatas, performa bisa menurun.

**Collaborative Filtering**

- **Cara kerja** : Dalam membangun model **Collaborative Filtering*, menggunakan pendekatan model-based dengan membuat sebuah arsitektur neural network sederhana bernama RecommenderNet. Model ini dirancang untuk mempelajari representasi (embedding) dari pengguna dan film, kemudian menghitung skor kecocokan antar keduanya. Proses pelatihan model menggunakan optimizer Adam dan dievaluasi dengan Root Mean Squared Error (RMSE) sebagai metrik. Model RecommenderNet mempelajari representasi pengguna dan film melalui dua layer embedding, lalu menghitung nilai kecocokan (match score) di antara keduanya menggunakan operasi dot product. Nilai tersebut kemudian disesuaikan dengan bias pengguna dan film, dan hasil akhirnya dipetakan ke dalam rentang 0 hingga 1 menggunakan fungsi aktivasi sigmoid.

Tabel 3. Movie genre yang direkomendasikan berdasarkan rating tertinggi.

| Movie Name                                                           | Genre                          |
| ---------------------------------------------------------------------| -------------------------------|
| Star Wars: Episode IV - A New Hope (1977) | Comedy|War               | Action|Adventure|Sci-Fi 	|
| Sin City (2005)                                               | Action|Crime|Film-Noir|Mystery|Thriller   |
| Harry Potter and the Goblet of Fire (2005)                           | Adventure|Fantasy|Thriller|IMAX |
Thank You for Smoking (2006)                                           | Comedy|Drama     |
| Star Trek Into Darkness (2013)        			| Action|Adventure|Sci-Fi|IMAX              |

Tabel 4. Movie Top 10 yang direkomendasikan.

| Movie Name                                              | Genre                          				  |
| --------------------------------------------------------| --------------------------------------------------------------|
| Heidi Fleiss: Hollywood Madam (1995)                    | Documentary		    |
| Paths of Glory (1957)                                | Drama|War                  |
| Jonah Who Will Be 25 in the Year 2000 (Jonas qui aura 25 ans en l'an 2000) (1976)                                       | Comedy                    |
| Stunt Man, The (1980)                          | Action|Adventure|Comedy|Drama|Romance|Thriller |
| Belle époque (1992)                      	| Comedy|Romance                       |
| Trial, The (Procès, Le) (1962)                                       | Drama                   |
| Adam's Rib (1949)                                    | Comedy|Romance           |
| Bad Boy Bubby (1993)                                   | Drama |
| Enter the Void (2009) 			| Drama                     |
| Brooklyn (2015)                		| Drama|Romance            |

Berdasarkan Tabel 3 dan Tabel 4, film bergenre action memperoleh rating tertinggi dari pengguna. Selanjutnya, sepuluh film teratas yang direkomendasikan oleh sistem didominasi oleh genre drama dan comedy.

- Kelebihan **Collaborative Filtering**:
	- Tidak Membutuhkan Informasi Item yang Detail: Sistem hanya membutuhkan data interaksi pengguna (seperti rating), tanpa harus tahu isi atau deskripsi dari item tersebut (misalnya genre, sinopsis).
	- Bisa Menangkap Preferensi yang Kompleks dan Tersembunyi: Karena rekomendasi dibuat dari pola kesamaan antar pengguna/item, sistem dapat menemukan hubungan menarik yang tidak eksplisit (misalnya, dua film berbeda genre tapi disukai oleh pengguna yang sama).
	- Bisa Merekomendasikan Hal Baru untuk Pengguna: Sistem bisa menyarankan item yang sangat berbeda dari histori pengguna, selama ada pengguna lain yang mirip pernah menyukai item tersebut (lebih variatif).
- Kekurangan **Collaborative Filtering**:
	- Skalabilitas: Saat jumlah pengguna dan item sangat besar, algoritma ini bisa menjadi berat secara komputasi dan membutuhkan optimisasi.
	- Sparsity: Banyak dataset interaksi yang bersifat sparse (jarang), karena pengguna hanya berinteraksi dengan sebagian kecil item. Ini bisa mengurangi akurasi prediksi.
	- Masalah Popularitas: Cenderung merekomendasikan item populer karena lebih banyak data interaksinya, sehingga item yang kurang populer bisa terabaikan meskipun berkualitas.


## Evaluation

### Content Based Filtering

Evaluasi yang dapat digunakan adalah matriks presisi. Presisi merupakan sebuah kemampuan dari alat ukur untuk menunjukkan angka yang sama bila dipakai secara berulang-ulang dalam kondisi pengukuran dan obyek ukur yang sama. Pada kasus ini, presisi akan memprediksi label yang benar terhadap keseluruhan prediksi. 

Rumus perhitungan matrik presisi:

![pres](https://github.com/fabasassa-lab/Movie_Recommendation_System/blob/main/images/pres.png?raw=true)

Dari hasil rekomendasi yang ditampilkan pada bagian modeling, diketahui bahwa pengguna akan mencari rekomendasi film terkait ` If I Stay (2014)`. Kemudian, sistem rekomendasi memberikan 5 film terkait yang memiliki genre serupa, yakni `Drama`. Berdasarkan rumus presisi di atas, diketahui bahwa keseluruhan rekomendasi yang diberikan memiliki genre serupa dengan film yang dicari rekomendasinya. Artinya, presisi sistem yang dibangun sebesar 5/5 atau 100%.

### Collaborative Filtering

Evaluasi metrik yang digunakan untuk mengukur kinerja model adalah metrik RMSE (*Root Mean Squared Error*). RMSE merupakan metode pengukuran dengan mengukur perbedaan nilai dari prediksi sebuah model sebagai estimasi atas nilai yang diobservasi, dan merupakan hasil kuadrat dari MSE. Keakuratan metode estimasi kesalahan pengukuran ditandai dengan adanya nilai RMSE yang kecil. 

Semakin kecil nilai yang diperoleh RMSE, semakin akurat juga modelnya.

Rumus perhitungan matrik MSE: 

![mse](https://github.com/fabasassa-lab/Movie_Recommendation_System/blob/main/images/mse.png?raw=true)

Gambar 5. Model Evaluasi Metriks

![rmse](https://github.com/fabasassa-lab/Movie_Recommendation_System/blob/main/images/rmse.png?raw=true)

Pada Gambar 5, visualisasi metrics memperlihatkan bahwa proses training model berjalan dengan stabil dan model mencapai konvergensi pada sekitar epoch ke-100. Dari hasil tersebut, didapatkan nilai error akhir sebesar sekitar 0.2090 dan error pada data validasi sekitar 0.2223. Hasil analisis akhir menunjukkan bahwa model tidak mengalami overfitting, karena grafik untuk data uji dan data train menunjukkan tren yang serupa dan stabil.


**---Akhir Laporan---**

_Github:_
https://github.com/fabasassa-lab/Movie_Recommendation_System

_Referensi:_
[1] Gomez-Uribe, C. A., & Hunt, N. (2015). The Netflix recommender system: Algorithms, business value, and innovation. ACM Transactions on Management Information Systems (TMIS), 6(4), 1–19. https://doi.org/10.1145/2843948

[2] He, X., Liao, L., Zhang, H., Nie, L., Hu, X., & Chua, T. S. (2017). Neural collaborative filtering. Proceedings of the 26th International Conference on World Wide Web (WWW '17), 173–182. https://doi.org/10.1145/3038912.3052569

[3] movies-and-ratings-for-recommendation-system. https://www.kaggle.com/datasets/nicoletacilibiu/movies-and-ratings-for-recommendation-system
