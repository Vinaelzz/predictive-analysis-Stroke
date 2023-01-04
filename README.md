#  Predictive Analysis Stroke

# Domain Proyek

Stroke merupakan salah satu penyakit yang berbahaya di dunia, bahkan menurut WHO (World Health Organization) stroke adalah salah satu health problem terbesar didunia dan di Amerika Serikat storke berada di urutan ke-5 sebagai penyebab kematian terbanyak

Oleh karena itu dilakukan penelitian mengurangi resiko kematian akibat stroke, dalam melakukan penelitian perlu dicari tahu faktor apa saja yang memiliki korelasi dengan stroke dan faktor apa yang memiliki korelasi terbesar, sehingga kita bisa memprediksi kemungkinan seseorang terkena stroke dari faktor-fator tersebut.


# Business Understanding

Dikarenakannya tingkat bahaya dan jumlah penderita stroke yang sangat banyak maka proyek ini dirancang untuk membantu lembaga-lembanga atau organisasi yang bergerak dibidang kesehatan untuk membantu melakukan pengecekan terhadap para masyarat, serta dengan dirancangnya proyek ini maka masyarakat dapat dipermudah dalam melakukan pengecekan terhadap kemungkinan terkena stroke.

berikut adalah beberapa pihak yang menjadi target proyek ini :
- seluruh masrakyat umum terutama rakyat Indonesia yang memiliki kewaspadaan terhadap stroke
- Organisasi atau lembaga pemerintahan yang bergerak dibidang kesehatan 
- Lembaga atau organisasi swasta yang ingin mengurangi jumlah penderita stroke dan peduli dengan profil kesehatan di Indonesia

### Problem Statements & Goals
Berdasarkan kondisi yang telah diuraikan sebelumnya, peneliti akan mengembangkan model yang dapat memprediksi kemungkinan seseorang terkena stroke.
berikut adalah jabaran dari problem statement:

- Faktor apa yang memiliki korelasi terbesar terhadap stroke
- Faktor apa saja yang berhubungan dengan penyakit stroke
- Bagaimana cara mengurangi resiko terkena stroke

Untuk  menjawab pertanyaan tersebut, peneliti akan membuat predictive modelling dengan tujuan atau goals sebagai berikut:

- Mengetahui faktor dengan korelasi terbesar terhadap stroke
- Mengetahui faktor faktor penyebab stroke
- Mengetahui bagaimana cara mengurangi resiko terkena stroke

### Solution statements
- melakukan *data preprocessing / data cleaning* lalu data tersebut dianalisis menggunakan teknik univariate dan multivariate untuk diketahui outlinersnya, serta dapat diketahui tingkat korelasi antara faktor dengan jumlah orang yang terkena stroke
- lalu setelah selesai di analisis maka dibuatlah sebuah model untuk memprediksi apakah orang tersebut memiliki faktor resiko terkena stroke yang tinggi atau tidak melalui faktor-faktor yang ada

# Data Understanding
Dataset yang digunakan dalam proyek ini berasal dari kaggle yaitu : [Stroke Healthcare  Dataset](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset).

informasi terkait dataset :
- Dataset memiliki format CSV (Comma-Seperated Values).
- Dataset memiliki 5110 sample dengan 12 fitur/kolom.
- Dataset memiliki 4 fitur bertipe int64, 5 fitur bertipe object dan 3 fitur bertipe float64.
- Terdapat missing value dalam dataset 

berikut adalah tabel info dari dataset yang digunakan peneliti:

  Table 1 Stroke dataset info
|    | column            | Non-Null | Count    | Dtype   |
|----|-------------------|----------|----------|---------|
| 0  | id                | 5110     | non-null | int64   |
| 1  | gender            | 5110     | non-null | object  |
| 2  | age               | 5110     | non-null | float64 |
| 3  | hypertension      | 5110     | non-null | int64   |
| 4  | heart_disease     | 5110     | non-null | int64   |
| 5  | ever_married      | 5110     | non-null | object  |
| 6  | work_type         | 5110     | non-null | object  |
| 7  | Residence_type    | 5110     | non-null | objecgt |
| 8  | avg_glucose_level | 5110     | non-null | float64 |
| 9  | bmi               | 4909     | non-null | float64 |
| 10 | smoking_status    | 5110     | non-null | object  |
| 11 | stroke            | 5110     | non-null | int64   |

##### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
1) id: unique identifier
2) gender: "Male", "Female" or "Other"
3) age: age of the patient
4) hypertension: 0 if the patient doesn't have hypertension, 1 if the patient has hypertension
5) heart_disease: 0 if the patient doesn't have any heart diseases, 1 if the patient has a heart disease
6) ever_married: "No" or "Yes"
7) work_type: "children", "Govt_jov", "Never_worked", "Private" or "Self-employed"
8) Residence_type: "Rural" or "Urban"
9) avg_glucose_level: average glucose level in blood
10) bmi: body mass index
11) smoking_status: "formerly smoked", "never smoked", "smokes" or "Unknown"*
12) stroke: 1 if the patient had a stroke or 0 if not
*Note: "Unknown" in smoking_status means that the information is unavailable for this patient

# Data Preparation
Pada tahap ini akan dilakukan *data preprocessing/cleaning* terlebih dahulu untuk mengetahui apakah adanya *Missing value* lalu setelah itu data akan di analisis  untuk mengetahui apakah terdapat data *unique* atau *outliers* pada data dan pada tahap terakhir untuk persiapan pembuatan model makan akan di lakukan *One hot encoding*, *Train test split*, dan normalisasi data.

##### Data cleaning
- dari ke-12 fitur di atas fitur 'id' akan di drop dikarenakan tidak memiliki hubungan dengan penyebab terjadinya stroke
- lalu pada fitur 'bmi' ditemukan sebanyak 201 missing value, dikarenakan jumlah missing value cukup banyak maka data akan di replace menggunakan mean dari 'bmi' yang ada dengan code sebagai berikut   

##### Analysis
pada tahap analysis dilakukan 2 metode yaitu univariate dan multivariate method.

- Analysis Univariate bertujuan untuk menganalisis tiap faktor/fitur yang ada secara terpisah sehingga kita bisa mengetahui elemen unik/outliers dari faktor tersebut dan outliers tersebut akan di *drop* untuk menghindari ketidakakuratan hasil *predictive analysis*.

    Cara mengetahui adanya *outliers* atau tidak adalah dengan cara menanggregasi kan jumlah tiap kategori yang dimiliki oleh sebuah faktor, untuk *aggregate* pertama kita mengecek faktor "gender" yang dimana didalamnya memiliki 3 kategori yaitu :
    1. Male dengan jumlah data 2115
    2. Female dengan jumlah data 2994
    3. Other dengan jumlah data 1
     dari ke-3 kategori tersebut terdapat 1 kategori minor atau memiliki data yang sangat sedikit yaitu "other" 
     
    Dari hasil Univariate analysis ini menunjukan bahwa terdapat *outliers* pada faktor "gender" yaitu kategori "other" yang hanya memiliki 1 buah data. Sehingga kategori data "other" harus di hapus, yang mana bila tidak di hapus maka kategori tersebut akan menyebabkan melencengnya hasil analisis dikarenakan terdapat satu sampel kategori yang berbeda dan jumlahnya hanaya satu yaitu kategori "other"
    
    Nah lalu untuk mengatasi permasalahan *outliers* tersebut maka disini saya menggunakan metode pendistribusian data menggunakan model univariat sehingga dapat terlihat metrik/kategori mana yang menyimpang dan harus di buang atau di *replace* dengan data mean dari faktor tersebut.
    

sedangkan berikut adalah beberapa contoh faktor yang memiliki persebaran merata atau tidak memiliki *outliers* 
![image](https://user-images.githubusercontent.com/73600512/199658106-041b7277-1d02-4f0c-a315-4149ece3f019.png)
 
  Hasil dari grafik metode univariat diatas menunjukan bahwa tidak adanya outliers dengan menggunakan metode analysis *univariate* sehingga dapat terlihat apakah sebuah faktor memiliki metrik/ kategori yang menyimpang atau beda sendiri di banding kategori lainnya.
  Lalu agar hasil analisis menjadi lebih akurat makan dilakukan model linear multivariate untuk mendeteksi *outliers* dan juga mencari korelasi antara faktor yang ada

Berikut analisis dari hasil histogram  diatas :
1. Sebagian besar sample data memiliki BMI di angka 30an
2. Sebagian besar sampe memiliki kadar glukosa sebesar 80-90an
3. sampel yang digunakan sebagain besar berasal dari orang yang tidak terkena stroke dan tidak memiliki hipertensi

- Analysis Multivariate bertujuan untuk mencari korelasi antara 2 atau lebih faktor/fitur yang ada.
  Berikut adalah hasil grafik dari multivariate analysis :
  
 1. Gender
  dari histogram diatas menunjukan bahwa lebih tinggi persentase laki-laki terkena stroke dibandingkan perempuan.
  
  
    Gambar 1 Histogram gender
    
  ![image](https://user-images.githubusercontent.com/73600512/199656295-7c39e719-8bb4-4b7f-859b-14a269122bf4.png)
  
  
 2. Working type
  hasil histogram menunjukan bahwa orang yang memiliki pekerjaan "self-employed" memiliki persentase yang paling besar untuk terkena stroke.
  
    Gambar 2 Histogram pekerjaan
   ![image](https://user-images.githubusercontent.com/73600512/199656448-828d0fdd-e359-46d8-8f41-f3a28e730a85.png)
  
 3. Smoking Status
  dari faktor merokok, dapat dilihat bahwa orang yang sudah berhenti merokok memiliki persentase terkena stroke yang lebih besar dibandingkan kategori lagi yaitu masih   merokok, dan tidak merokok.
  
    Gambar 3 Histogram status merokok
   ![image](https://user-images.githubusercontent.com/73600512/199656560-4a8980d8-978f-4fdf-87d0-6987c828b6e4.png)
  
 4. Status married
  dari histogram diatas dapat dilihat bahwa cukup jomplang perbedaan antara yang sudah menikah dan yang belum, di histogram tersebut menunjukan bahwa masyarakat yang     sudah menikah memiliki korelasi yang jauh lebih tinggi untuk terkena stroke dibandingkan yang belum menikah.
  
    Gambar 4 Histogram status married
   ![image](https://user-images.githubusercontent.com/73600512/199656688-63e58435-ccf2-4778-9439-d1c80878744e.png)
  

Lalu berikut adalah hasil heatmap dari persebaran faktor yang bersifat numerik :

   Gambar 5 heatmap korelasi
   
![gambar1](https://user-images.githubusercontent.com/73600512/200104545-e6570d45-2819-4511-ac5e-61db29e8a635.png)                      


dari heatmap tersebut tidak memunculkan korelasi yang terlalu signifikan dikarenkan dataset yang digunakan memang kurang akurat, tetapi dari heatmap tersebut dapat disimpulkan faktor yang memiliki korelasi terbesar adalah "bmi" atau *body mass index* yang memiliki korelasi sebesar 0.4.

#### Setelah outliers dihapus dan data sudah dicleaning makan di lakukanlah tahap berikut
##### One Hot Encoding
One hot encoding adalah teknik mengubah data kategorik menjadi data numerik dimana setiap kategori menjadi kolom baru dengan nilai 0 atau 1.

##### Train Test Split
Train test split adalah proses untuk membagi data menjadi data latih dan data uji. Pada proyek ini dataset dengan jumlah data 5110 dibagi menjadi 4854 untuk data latih dan 256 untuk data uji.

#### Normalization
Pada tahap ini agar algoritma dari model machine learning dapat bekerja lebih optimal maka perlu dilakukan normalisasi yaitu memodelkan data yang seragam dan memiliki skala yang relatif sama.    
## Modeling

##### Modeling 

Pada tahap modeling ini, peneliti menggunakan 3 buah algoritma dan 1 buah hyperparameter model yaitu gridsearch:

- Gridsearch
Hyperparameter Tuning (Grid Search) Hyperparameter tuning adalah cara untuk mendapatkan parameter terbaik dari algoritma-algoritma yang dipakai untuk model. Salah satu teknik dalam hyperparameter tuning yang digunakan dalam proyek ini adalah grid search.
Berikut adalah tabel hasil hyperparameter :

Tabel 2 Hyperparameter gridsearch tabel

|   | Mode          | Best_score | Best_param                                     |
|---|---------------|------------|------------------------------------------------|
| 0 | knn           | -0.001489  | {'n_neighbors':15}                             |
| 1 | boosting      | 0.077877   | {'learning_rate':0.001,'n_estimators':25...    |
| 2 | random_forest | 0.071144   | {'max_depth':8, 'n_estimators':25,'random_s... |
- KNN (K-Nearest Neighbor)
K-Nearest Neighbour K-Nearest Neighbour bekerja dengan membandingkan jarak satu sampel ke sampel pelatihan lain dengan memilih sejumlah k tetangga terdekat. Proyek ini menggunakan sklearn.neighbors.KNeighborsRegressor dengan memasukkan X_train dan y_train dalam membangun model. Parameter yang digunakan pada proyek ini adalah :

  1. n_neighbors = Jumlah k tetangga tedekat.

- Random Forest
Random Forest adalah teknik dalam machine learning dengan metode ensemble. Teknik ini beroperasi dengan membangun banyak decision tree pada waktu pelatihan. Proyek ini menggunakan sklearn.ensemble.RandomForestRegressor dengan memasukkan X_train dan y_train dalam membangun model. Parameter yang digunakan pada proyek ini adalah :

  1. n_estimator: jumlah trees (pohon) di forest.
  2. max_depth: kedalaman atau panjang pohon. Ia merupakan ukuran seberapa banyak pohon dapat membelah (splitting) untuk membagi setiap node ke dalam jumlah pengamatan                  yang diinginkan.
  3. random_state: digunakan untuk mengontrol random number generator yang digunakan. 
  4. n_jobs: jumlah job (pekerjaan) yang digunakan secara paralel. Ia merupakan komponen untuk mengontrol thread atau proses yang berjalan secara paralel. n_jobs=-1                artinya semua proses berjalan secara paralel.

- Boosting Algorithm
Algoritma ini bertujuan untuk meningkatkan performa atau akurasi prediksi. Caranya adalah dengan menggabungkan beberapa model sederhana dan dianggap lemah (weak learners) sehingga membentuk suatu model yang kuat (strong ensemble learner). Algoritma boosting muncul dari gagasan mengenai apakah algoritma yang sederhana seperti linear regression dan decision tree dapat dimodifikasi untuk dapat meningkatkan performa. Berikut adalah parameter yang digunakan :
  1. learning_rate: bobot yang diterapkan pada setiap regressor di masing-masing proses iterasi boosting.
  2. random_state: digunakan untuk mengontrol random number generator yang digunakan.

dan dari 3 algoritma tersebut akan dipilih algortima yang memiliki keakuratan paling tinggi atau nilai error yang tertinggi
# Evaluation
Metrik evaluasi yang digunakan pada proyek ini adalah akurasi dan mean squared error (MSE). Akurasi menentukan tingkat kemiripan antara hasil prediksi dengan nilai yang sebenarnya (y_test). Mean squared error (MSE) mengukur error dalam model statistik dengan cara menghitung rata-rata error dari kuadrat hasil aktual dikurang hasil prediksi. 
Berikut formulan MSE :

 MSE = $\frac{1}{n} \Sigma_{i=1}^n({y}-\hat{y})^2$.
    
{n}	=	number of data points
Y_{i}	=	observed values
\hat{Y}_{i}	=	predicted values

Hasil tabel dari MSE :

Tabel 3 hasil MSE

|           | Train    | Test     |
|-----------|----------|----------|
| KKN       | 0.000037 | 0.00014  |
| rf        | 0.000024 | 0.000196 |
| Boosting  | 0.000041 | 0.000098 |

dapat dilihat dari hasil diatas yang memiliki hasil paling akurat adalah dari algorita RF (Random Forest)

Lalu berikut adalah hasil dari prediksi yang sudah dibuat dengan menggunakan model rf dikarenakam memiliki akurasi yang paling besar di banding algoritma lain

![image](https://user-images.githubusercontent.com/73600512/200104456-ae3a94f1-74f1-4a9d-bdb9-0d370e22cc3b.png)

yang dimana dari hasil grafik diatas menunjukan bahwa algoritam "rf" random forest lah yang menunjukan hasil paling signifikan

berikut adalah hasil tabel prediksi yang menunjukan y_true, prediksi KNN, prediksi_rf, dan prediksi_boosting

Tabel 4 hasil prediksi
|      | y_true | prediksi_KNN | prediksi_rf | prediksi_Boosting |
|------|--------|--------------|-------------|-------------------|
| 2823 | 0      | 0.4          | 0.3         | 0.3               |
| 1155 | 0      | 0.3          | 0.5         | 0.3               |
| 2629 | 0      | 0.3          | 0.4         | 0.3               |
| 893  | 0      | 0.1          | 0.4         | 0.3               |
| 4866 | 0      | 0.3          | 0.4         | 0.3               |
Table : asdasd
# Conclusion
Dari hasil penelitian diatas maka dapat disimpulkan bahwa dari berbagai macam faktor diatas walaupun faktor-faktor tersebut memiliki korelasi dengan stroke tetapi salah satu faktor yang memiliki korelasi tertinggi dengan stroke adalah faktor "BMI" atau *body mass index*. Tetapi tingkat korelasi dari faktor "BMI" sendiri sebenarnya masih tergolong kecil dikarenakan dataset yang kurang mendukung.

# Reference
[1] Dinata, C. A., Syafrita, Y., & Sastri, S. (2013). Artiakel Penelitian. Jurnal Kesehatan Andalas, 2(2). http://jurnal.fk.unand.ac.id


