# Laporan Proyek Machine Learning Terapan - Achmad Fauzihan Bagus Sajiwo

<div align="center">
	<p>MOVIE - RECOMMENDATION SYSTEM</p>
</div>

<div align="center">
	<img src="https://github.com/fabasassa-lab/Stroke-Risk-Prediction/blob/main/image/stroke.png?raw=true">
</div>

## Project Overview

Stroke merupakan salah satu penyebab utama kematian dan kecacatan di Indonesia. Menurut studi Global Burden of Disease (GBD) tahun 2019, Indonesia memiliki angka kematian akibat stroke yang tinggi, dengan tingkat kematian yang disesuaikan berdasarkan usia dan jenis kelamin sebesar 193,3 per 100.000 penduduk [1].​

Prevalensi stroke di Indonesia juga menunjukkan tren peningkatan. Data dari Riset Kesehatan Dasar (Riskesdas) tahun 2018 mencatat bahwa prevalensi stroke meningkat dari 7 per 1.000 penduduk pada tahun 2013 menjadi 10,9 per 1.000 penduduk pada tahun 2018 [1].​

Faktor risiko utama stroke meliputi hipertensi, diabetes, merokok, dan gaya hidup sedentari. Deteksi dini terhadap individu dengan risiko tinggi sangat penting untuk mencegah kejadian stroke. Namun, keterbatasan dalam akses layanan kesehatan dan kurangnya kesadaran masyarakat seringkali menghambat upaya pencegahan.​

Dalam konteks ini, pemanfaatan teknologi dan data science menjadi sangat penting. Dengan memanfaatkan data historis pasien dan teknik machine learning, kita dapat membangun model prediktif yang mampu mengidentifikasi individu yang memiliki risiko tinggi terkena stroke. Model semacam ini sangat bermanfaat untuk digunakan oleh tenaga medis, instansi kesehatan, hingga masyarakat umum dalam rangka mendukung pengambilan keputusan preventif yang cepat dan akurat.​


## Business Understanding

Pada bagian ini, akan menjelaskan mengenai proses klarifikasi masalah yang terdiri dari _Problem Statement_, _Goals_ dan _Solution Statements_.

### Problem Statements

Bagaimana mengidentifikasi pasien dengan risiko tinggi terhadap stroke sebelum gejala serius muncul.

### Goals

Tujuan dari proyek ini adalah untuk mengidentifikasi pasien dengan risiko tinggi terhadap stroke sebelum gejala serius muncul dengan membangun model klasifikasi yang mampu memprediksi apakah seseorang termasuk dalam kategori "berisiko stroke" berdasarkan informasi demografis yang ada.

### Solution statements

Solusi yang diusulkan adalah membangun dan membandingkan beberapa model klasifikasi untuk memprediksi risiko stroke, yaitu:
- K-Nearest Neighbors (KNN)
- Random Forest
- AdaBoost

Untuk mengukur kinerja dari model yang dibangun, digunakan metrik evaluasi klasifikasi, yaitu:
- Akurasi (Accuracy)

## Data Understanding
Data yang digunakan dalam proyek ini adalah **35000** data **Movies & Ratings for Recommendation System** yang dapat diunduh dari situs [Kaggle](https://www.kaggle.com/datasets/nicoletacilibiu/movies-and-ratings-for-recommendation-system). Terdapat 19 fitur (kolom) yang terdapat pada dataset ini.

### Variabel-variabel pada Movies & Ratings for Recommendation System dataset adalah sebagai berikut:

1. Chest Pain	
- Integer (0/1): Menunjukkan apakah individu mengalami nyeri dada, gejala umum kondisi kardiovaskular.

2. Shortness of Breath	
- Integer (0/1): Menunjukkan apakah orang tersebut mengalami kesulitan bernapas, yang mungkin mengindikasikan masalah jantung atau paru-paru.

3. Irregular Heartbeat	
- Integer (0/1): Menunjukkan apakah orang tersebut memiliki detak jantung tidak teratur, faktor risiko stroke yang potensial.

4. Fatigue & Weakness	
- Integer (0/1): Menunjukkan kelelahan terus-menerus dan kelemahan otot, tanda-tanda umum masalah kardiovaskular.

5. Dizziness	
- Integer (0/1): Melaporkan apakah individu tersebut sering mengalami pusing, yang mungkin terkait dengan sirkulasi yang buruk.

6. Swelling (Edema)	
- Integer (0/1): Menunjukkan pembengkakan pada ekstremitas karena retensi cairan, masalah kardiovaskular yang potensial.

7. Neck/Jaw/Pain	
- Integer (0/1): Menjelaskan nyeri di area ini, yang dapat menjadi tanda peringatan stroke atau serangan jantung.

8. Excessive Sweating	
- Integer (0/1): Menunjukkan apakah individu mengalami keringat yang tidak biasa, yang dapat mengindikasikan gangguan kardiovaskular.

9. Persistent Cough	
- Integer (0/1): Menunjukkan batuk kronis, yang dapat dikaitkan dengan gagal jantung.

10. Nausea/Vomiting	
- Integer (0/1): Melaporkan mual atau muntah yang sering, yang dapat dikaitkan dengan kejadian kardiovaskular.

11. High Blood Pressure	
- Integer (0/1): Mewakili apakah orang tersebut memiliki tekanan darah tinggi, faktor risiko utama untuk stroke.

12. Chest Discomfort (Activity)	
- Integer (0/1): Menunjukkan apakah individu mengalami ketidaknyamanan dada selama aktivitas fisik.

13. Cold Hands/Feet	
- Integer (0/1): Menunjukkan apakah orang tersebut sering mengalami ekstremitas dingin, yang merupakan tanda kemungkinan masalah sirkulasi.

14. Snoring/Sleep Apnea	
- Integer (0/1): Melaporkan apakah orang tersebut mengalami apnea tidur, yang dapat meningkatkan risiko stroke.

15. Anxiety/Feeling of Doom	
- Integer (0/1): Menunjukkan apakah orang tersebut sering mengalami kecemasan atau perasaan akan datangnya malapetaka, yang dapat dikaitkan dengan gangguan kardiovaskular.

16. Stroke Risk Percentage
- Float (0-100): Perkiraan persentase risiko terkena stroke, berdasarkan tingkat keparahan gejala dan indikator medis.

17. At Risk (Binary)	
- Integer (0/1): Menunjukkan apakah orang tersebut diklasifikasikan sebagai berisiko terkena stroke (1) atau tidak (0).

18. Age	
- Integer (18-86): Usia individu, faktor penting dalam menilai risiko stroke.

19. Gender
- String: Male/Female

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
https://github.com/fabasassa-lab/Stroke-Risk-Prediction

_Referensi:_
[1] Venketasubramanian, N., Yudiarto, F. L., & Tugasworo, D. (2022). Stroke burden and stroke services in Indonesia. Frontiers in Neurology, 13, 850282. https://doi.org/10.3389/fneur.2022.850282

[2] Mahatir Ahmed Tusher, "Stroke Risk Prediction Dataset based on Literature", Kaggle, https://www.kaggle.com/datasets/mahatiratusher/stroke-risk-prediction-dataset-v2
