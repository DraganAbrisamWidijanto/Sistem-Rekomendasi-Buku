# Laporan Proyek Machine Learning - Dragan Abrisam Widijanto
## Book Recommendation Using Content-Based Filtering

### Project Overview
Sistem rekomendasi merupakan alat generasi baru yang membantu pengguna menavigasi informasi di internet dan mendapatkan konten sesuai dengan preferensi mereka. Dalam konteks buku, sistem ini memainkan peran penting dalam menyarankan buku yang relevan berdasarkan kesamaan dengan buku yang telah dibaca sebelumnya. Dengan meningkatnya jumlah buku yang tersedia secara online, sistem rekomendasi menjadi semakin penting untuk membantu pembaca menemukan buku yang sesuai dengan minat dan preferensi mereka.

Proyek ini penting untuk diselesaikan karena dapat meningkatkan pengalaman pengguna dengan mempermudah penemuan buku yang relevan, mendukung penjualan dan loyalitas pembaca, serta mengadaptasi rekomendasi terhadap perubahan preferensi seiring waktu. Dengan demikian, sistem ini tidak hanya memberikan manfaat bagi pengguna individu, tetapi juga berdampak positif pada industri buku secara keseluruhan.

Sistem rekomendasi dirancang untuk memudahkan pengguna dalam menjelajahi informasi yang tersedia di internet serta membantu mereka memilih konten yang paling sesuai dengan preferensi masing-masing. Dalam konteks ini, pendekatan berbasis konten yang diusulkan oleh Rana dan Jain [1] memperhitungkan dimensi temporal, sehingga sistem dapat memberikan rekomendasi yang beragam dan relevan berdasarkan pembaruan informasi yang terjadi seiring waktu.

### Referensi
[1] C. Rana dan S.K. Jain, "Building a Book Recommender system using time based content filtering," WSEAS Transactions on Computers, vol. 11, no. 2, pp. 2224-2872, 2012.



## Business Understanding

### Problem Statements

1. **Pernyataan Masalah 1**: Banyak pengguna mengalami kesulitan dalam menemukan buku yang sesuai dengan minat dan preferensi mereka di antara berbagai pilihan yang tersedia secara online. Hal ini disebabkan oleh terlalu banyaknya pilihan yang membuat pengguna bingung untuk menentukan pilihan.

2. **Pernyataan Masalah 2**: Pengguna sering kali merasa kewalahan oleh jumlah informasi yang ada, sehingga mereka mungkin melewatkan buku-buku yang relevan atau menarik bagi mereka. Ini menciptakan pengalaman browsing yang tidak efisien dan mempengaruhi kepuasan pengguna.

3. **Pernyataan Masalah 3**: Terdapat kurangnya rekomendasi yang disesuaikan dengan pengalaman membaca sebelumnya, membuat rekomendasi yang diterima terasa tidak relevan. Ini mengurangi kemungkinan pengguna untuk menjelajahi dan membeli buku baru.

### Goals

1. **Jawaban Pernyataan Masalah 1**: Mengembangkan sistem rekomendasi buku yang membantu pengguna menemukan buku yang sesuai dengan minat dan preferensi mereka berdasarkan kesamaan konten dengan buku yang telah dibaca sebelumnya. Dengan cara ini, pengguna dapat dengan cepat menemukan buku yang sesuai tanpa harus melakukan pencarian yang melelahkan.

2. **Jawaban Pernyataan Masalah 2**: Menciptakan antarmuka pengguna yang intuitif dan mudah digunakan untuk menyajikan rekomendasi buku yang relevan. Antarmuka yang ramah pengguna akan mengurangi rasa kewalahan dan meningkatkan pengalaman pengguna dalam menjelajahi rekomendasi buku.

3. **Jawaban Pernyataan Masalah 3**: Memastikan rekomendasi yang diberikan lebih personal dan relevan dengan mempertimbangkan data historis pengguna serta informasi terkini tentang buku. Dengan penyesuaian ini, rekomendasi akan lebih sesuai dengan preferensi individu pengguna, sehingga meningkatkan kemungkinan mereka untuk menemukan dan membaca buku baru.

### Solution Approach

1. **Content-based Filtering**: Menggunakan teknik penyaringan konten untuk menganalisis fitur-fitur buku (seperti judul, penulis, dan deskripsi) dan merekomendasikan buku yang mirip berdasarkan kesamaan konten. Pendekatan ini memanfaatkan metode seperti TF-IDF dan Cosine Similarity untuk menghitung kesamaan antara buku-buku dan membantu pengguna menemukan buku baru yang sesuai dengan yang telah mereka baca sebelumnya.

2. **Collaborative Filtering**: Mengembangkan sistem rekomendasi berbasis kolaboratif yang menganalisis interaksi pengguna dengan buku, seperti rating dan preferensi. Dengan menggunakan data historis dari pengguna lain, sistem ini dapat memberikan rekomendasi yang lebih personal berdasarkan kesamaan dalam perilaku membaca. Pendekatan ini memanfaatkan algoritma k-Nearest Neighbors (k-NN) untuk menemukan pengguna atau buku yang memiliki kemiripan berdasarkan rating yang diberikan. Dengan cara ini, sistem dapat membantu pengguna menemukan buku yang mungkin tidak mereka pertimbangkan tetapi relevan dengan minat mereka, berdasarkan apa yang disukai oleh pengguna lain dengan preferensi serupa.

### Solution Statement

Untuk mencapai tujuan yang telah ditetapkan, sistem rekomendasi buku ini akan mengintegrasikan kedua pendekatan, yaitu Content-based Filtering dan Collaborative Filtering, untuk memberikan rekomendasi yang lebih komprehensif dan relevan bagi pengguna. 

- **Integrasi Content-based Filtering** akan memastikan bahwa pengguna mendapatkan rekomendasi yang didasarkan pada kesamaan konten, sehingga mereka dapat menemukan buku baru yang relevan dengan minat mereka. 
- **Integrasi Collaborative Filtering** akan menambahkan dimensi personalisasi yang lebih dalam, memungkinkan sistem untuk memberikan rekomendasi yang relevan berdasarkan preferensi pengguna lain yang memiliki selera membaca serupa.

Dengan menggabungkan kedua pendekatan ini, sistem diharapkan dapat memberikan solusi yang efektif untuk masalah yang dihadapi pengguna dalam menemukan buku yang sesuai dengan minat dan preferensi mereka, sekaligus meningkatkan pengalaman pengguna secara keseluruhan.

## Data Understanding

Dataset yang digunakan dalam proyek ini adalah *Goodbooks-10k* yang dapat diunduh dari Kaggle. Untuk mengunduh dataset dapat mengklik ini [Goodbooks-10k Dataset](https://www.kaggle.com/datasets/zygmunt/goodbooks-10k/data). Dataset ini terdiri dari lima file CSV dan satu file XML, namun hanya dua file CSV yang digunakan dalam analisis ini, yaitu `books.csv` dan `ratings.csv`, karena keterbatasan limit runtime.

### Informasi Dataset

- **Jumlah Data**: 
  - `books.csv`: 10,000 entri (buku)
  - `ratings.csv`: 981,756 entri (rating pengguna)
  
- **Kondisi Data**: 
  - `books.csv` memiliki 23 kolom, dengan beberapa kolom yang memiliki nilai null.
  - `ratings.csv` memiliki 3 kolom tanpa nilai null.

- **Missing Values**: Beberapa kolom dalam `books.csv` seperti `isbn`, `isbn13`, dan `original_publication_year` memiliki nilai null.

- **Duplikasi**: Beberapa buku ditemukan terduplikasi berdasarkan `book_id`, yang kemudian dihapus pada tahap persiapan data.

- **Outlier**: Tidak dilakukan analisis outlier karena dataset ini lebih fokus pada kesamaan konten buku berdasarkan judul dan penulis.

### Variabel pada `books.csv`

Variabel-variabel pada dataset `books.csv` adalah sebagai berikut:

1. **id**: Merupakan ID unik untuk setiap buku.
2. **book_id**: Merupakan ID buku yang dapat digunakan untuk referensi.
3. **best_book_id**: Merupakan ID buku terbaik yang dinilai oleh pengguna.
4. **work_id**: Merupakan ID karya yang berkaitan dengan buku.
5. **books_count**: Merupakan jumlah salinan buku yang tersedia.
6. **isbn**: Merupakan nomor ISBN buku (beberapa nilai mungkin null).
7. **isbn13**: Merupakan nomor ISBN-13 buku (beberapa nilai mungkin null).
8. **authors**: Merupakan nama penulis buku.
9. **original_publication_year**: Merupakan tahun publikasi asli buku (beberapa nilai mungkin null).
10. **original_title**: Merupakan judul asli buku (beberapa nilai mungkin null).
11. **title**: Merupakan judul buku.
12. **language_code**: Merupakan kode bahasa buku (beberapa nilai mungkin null).
13. **average_rating**: Merupakan rata-rata rating buku.
14. **ratings_count**: Merupakan jumlah rating yang diterima oleh buku.
15. **work_ratings_count**: Merupakan jumlah rating untuk karya terkait.
16. **work_text_reviews_count**: Merupakan jumlah ulasan teks untuk karya terkait.
17. **ratings_1**: Jumlah rating 1 bintang.
18. **ratings_2**: Jumlah rating 2 bintang.
19. **ratings_3**: Jumlah rating 3 bintang.
20. **ratings_4**: Jumlah rating 4 bintang.
21. **ratings_5**: Jumlah rating 5 bintang.
22. **image_url**: URL gambar buku.
23. **small_image_url**: URL gambar kecil buku.

### Variabel pada `ratings.csv`

Variabel-variabel pada dataset `ratings.csv` adalah sebagai berikut:

1. **book_id**: Merupakan ID buku yang dirating.
2. **user_id**: Merupakan ID unik untuk setiap pengguna.
3. **rating**: Merupakan nilai rating yang diberikan oleh pengguna (skala 1-5).

### Insight dan Visualisasi Data

Beberapa teknik visualisasi data dapat digunakan untuk memahami pola dalam dataset, seperti:

- **Histogram** untuk melihat distribusi rating buku.
- **Boxplot** untuk memahami bagaimana rating buku bervariasi berdasarkan penulis terpopuler.

Dengan melakukan analisis eksplorasi data (Exploratory Data Analysis), kita dapat mendapatkan wawasan lebih lanjut tentang preferensi pengguna dan popularitas buku.

**Insight dari Histogram**:
![Gambar 1](https://drive.google.com/uc?id=1BLTyJtCpPXGW-crNQUBiU4uo3_EVXTZ-)
- **Distribusi Normal**: Grafik menunjukkan distribusi yang menyerupai distribusi normal dengan puncak di sekitar rating 4. Ini menunjukkan bahwa sebagian besar buku mendapatkan rating yang baik, di atas rata-rata.
- **Anomali**: Terdapat beberapa buku dengan rating yang sangat rendah (sekitar 3.0) atau sangat tinggi (mendekati 4.75). Hal ini bisa menjadi fokus untuk model rekomendasi agar dapat mengidentifikasi preferensi ekstrem pengguna.

**Insight dari Boxplot**:
![Gambar 2](https://drive.google.com/uc?id=1oqeqUo3lOiqU6Luf1L9B49lVkYamfJsT)
- **Variasi Rating yang Signifikan**: Meskipun semua penulis tergolong populer, terdapat variasi yang cukup signifikan dalam rata-rata rating buku mereka. Ini menunjukkan bahwa popularitas seorang penulis tidak selalu berkorelasi langsung dengan kualitas buku yang dianggap oleh pembaca.

### Data Preparation

Pada tahap ini, data yang digunakan harus diproses terlebih dahulu agar siap untuk digunakan dalam pemodelan. **Data Preparation** sangat penting untuk memastikan bahwa data yang digunakan relevan, bersih, dan dapat diolah oleh algoritma machine learning yang dipilih. Setiap tahapan yang dilakukan dalam proyek ini bertujuan untuk meningkatkan kualitas data dan memperbaiki performa model rekomendasi. Berikut adalah tahapan lengkap beserta penjelasannya:

1. **Mengatasi Duplikasi**
   - **Tujuan**: Menghindari pengaruh yang berlebihan dari pengguna yang memberikan lebih dari satu rating pada buku yang sama.
   - **Langkah**: 
     ```python
     ratings_cleaned = ratings.drop_duplicates(subset=['user_id', 'book_id'], keep='last')
     ```
   - **Alasan**: Menghapus duplikasi dalam kolom `user_id` dan `book_id` memastikan bahwa setiap pengguna hanya berkontribusi satu rating untuk setiap buku, menjaga integritas data dan mencegah distorsi dalam analisis yang dapat memengaruhi hasil model.

2. **Menghapus Kolom Tidak Relevan**
   - **Tujuan**: Mengurangi ukuran data dan fokus pada fitur yang relevan dengan pemodelan.
   - **Langkah**:
     ```python
     books.drop(columns=['isbn', 'isbn13', 'original_title'], inplace=True)
     ```
   - **Alasan**: Menghapus kolom yang tidak relevan membantu menghindari kebisingan dalam data dan meningkatkan efisiensi analisis, sehingga model dapat bekerja lebih efektif tanpa informasi yang tidak diperlukan.

3. **Mengatasi Missing Values**
   - **Tujuan**: Menghindari masalah yang disebabkan oleh nilai kosong dalam data.
   - **Langkah**: 
     - Missing values pada kolom `original_publication_year` diisi dengan nilai **median**.
     - Missing values pada kolom `language_code` diisi dengan **mode**.
     ```python
     books['original_publication_year'].fillna(books['original_publication_year'].median(), inplace=True)
     books['language_code'].fillna(books['language_code'].mode()[0], inplace=True)
     ```
   - **Alasan**: Mengatasi missing values penting untuk memastikan bahwa model tidak menghadapi kesulitan dalam menganalisis data yang tidak lengkap, yang dapat menyebabkan kesalahan atau ketidakakuratan dalam rekomendasi.

4. **Memilih Fitur yang Relevan**
   - **Tujuan**: Memfokuskan hanya pada fitur yang dibutuhkan untuk analisis dan pembuatan model.
   - **Langkah**: 
     ```python
     columns_to_keep = ['book_id', 'authors', 'original_publication_year', 'title', 'language_code', 'average_rating']
     cleaned_books = books[columns_to_keep]
     ```
   - **Alasan**: Memilih fitur yang relevan membantu menyederhanakan model dan mengurangi kompleksitas perhitungan, sehingga proses pemodelan dapat berjalan lebih cepat dan efisien.

5. **Penggabungan Dataset (`ratings_cleaned` dan `cleaned_books`)**
   - **Tujuan**: Menggabungkan dua dataset untuk menghubungkan informasi buku dengan rating pengguna.
   - **Langkah**:
     ```python
     merged_df = pd.merge(ratings_cleaned, cleaned_books, on='book_id', how='left')
     ```
   - **Alasan**: Menggabungkan dataset ini penting untuk analisis yang lebih holistik, di mana informasi buku dan rating saling terkait, sehingga memungkinkan model untuk memberikan rekomendasi yang lebih baik.

6. **Filtering Rating Sesuai Buku yang Tersedia**
   - **Tujuan**: Mengambil hanya rating dari buku yang ada dalam dataset `cleaned_books`.
   - **Langkah**:
     ```python
     ratings_cleaned_filtered = ratings_cleaned[ratings_cleaned['book_id'].isin(cleaned_books['book_id'])]
     merged_df = pd.merge(ratings_cleaned_filtered, cleaned_books, on='book_id', how='left')
     ```
   - **Alasan**: Memfilter rating membantu menjaga fokus analisis pada data yang valid dan relevan, sehingga tidak ada informasi yang tidak diperlukan yang bisa mengganggu hasil.

7. **Pembersihan Teks (Preprocessing Teks)**
   - **Tujuan**: Mengonversi teks dalam judul dan nama penulis menjadi lebih seragam.
   - **Langkah**:
     ```python
     import re

     def clean_text(text):
         text = re.sub(r'[^A-Za-z0-9 ]+', '', text)  # Hapus karakter selain huruf, angka, dan spasi
         return text.lower()

     merged_df['title'] = merged_df['title'].apply(clean_text)
     merged_df['authors'] = merged_df['authors'].apply(clean_text)
     ```
   - **Alasan**: Pembersihan teks penting untuk memastikan konsistensi dalam analisis, mengurangi variasi yang dapat mengganggu proses perhitungan kemiripan.

8. **Sampling Data**
   - **Tujuan**: Mengurangi ukuran dataset untuk mempercepat proses komputasi.
   - **Langkah**:
     ```python
     merged_df = merged_df.sample(n=1100, random_state=42)
     ```
   - **Alasan**: Sampling membantu meningkatkan kecepatan pemrosesan sambil mempertahankan representativitas data, sehingga memudahkan eksperimen dan pengujian model.

9. **TF-IDF (Term Frequency - Inverse Document Frequency)**
   - **Tujuan**: Mengubah teks dari judul dan penulis buku menjadi representasi numerik.
   - **Langkah**:
     ```python
     from sklearn.feature_extraction.text import TfidfVectorizer
     tf = TfidfVectorizer(stop_words='english')
     tfidf_matrix = tf.fit_transform(merged_df['title'] + " " + merged_df['authors'])
     ```
   - **Alasan**: Menggunakan TF-IDF memungkinkan pengukuran kemiripan antar buku berdasarkan fitur teks secara lebih efektif, yang krusial untuk model berbasis konten.

10. **Visualisasi Sampel TF-IDF**
    - **Tujuan**: Menampilkan sampel kecil dari matriks TF-IDF.
    - **Langkah**:
      ```python
      import pandas as pd
      
      pd.DataFrame(
          tfidf_matrix.todense(),
          columns=tf.get_feature_names_out(),
          index=merged_df.title
      ).sample(22, axis=1).sample(10, axis=0)
      ```
    - **Alasan**: Memvisualisasikan sampel dari matriks TF-IDF membantu memastikan bahwa hasilnya sudah sesuai dengan harapan dan setiap kata diwakili dalam bentuk vektor.

11. **Membuat Matriks Pengguna-Buku**
    - **Tujuan**: Menghasilkan matriks yang menunjukkan interaksi antara pengguna dan buku.
    - **Langkah**:
      ```python
      user_book_matrix = book_data.pivot_table(index='user_id', columns='book_id', values='rating').fillna(0)
      ```
    - **Alasan**: Membuat matriks pengguna-buku sangat penting untuk analisis kolaboratif, di mana setiap baris mewakili `user_id`, setiap kolom mewakili `book_id`, dan nilai di dalam matriks adalah rating yang diberikan pengguna terhadap buku.

### Penjelasan Tambahan
Proses **Data Preparation** ini memastikan bahwa data yang digunakan dalam model rekomendasi adalah berkualitas tinggi, relevan, dan siap untuk dianalisis. Dengan melakukan pembersihan, penghilangan duplikasi, pengisian nilai yang hilang, serta pemilihan fitur yang relevan, kita dapat meminimalkan risiko kesalahan dalam analisis dan meningkatkan keakuratan rekomendasi. Selain itu, langkah-langkah seperti sampling dan TF-IDF membantu dalam mempercepat proses komputasi dan menyediakan representasi yang lebih baik dari data teks.

### Modeling

Tahapan ini membahas model sistem rekomendasi yang dikembangkan untuk memberikan rekomendasi buku kepada pengguna berdasarkan preferensi mereka. Dua pendekatan utama yang digunakan adalah **Content-Based Filtering** dan **Collaborative Filtering**. Masing-masing metode ini memiliki cara kerja dan algoritma yang berbeda, yang bertujuan untuk meningkatkan relevansi rekomendasi buku.

#### 1. Content-Based Filtering

**Deskripsi**: 
Sistem ini merekomendasikan buku berdasarkan kemiripan konten dari fitur-fitur yang ada, seperti judul dan penulis. Proses ini dilakukan dengan menghitung kemiripan antara buku menggunakan **Cosine Similarity**, di mana buku-buku yang memiliki nilai kemiripan tertinggi akan direkomendasikan kepada pengguna.

**Metode**: 
- **Cosine Similarity**: Mengukur kemiripan antara dua vektor (dalam hal ini, representasi buku) dengan menghitung sudut antara keduanya. Nilai 1 menunjukkan bahwa dua buku identik, sedangkan 0 menunjukkan tidak ada kemiripan.

**Fungsi yang Digunakan**:
- `buku_recommendations`: Fungsi ini digunakan untuk memberikan rekomendasi buku berdasarkan kemiripan konten. 
  - **Parameter**:
    - `nama_buku`: Judul buku yang menjadi acuan untuk mencari buku rekomendasi.
    - `similarity_data`: Matriks kemiripan buku, di mana setiap nilai menunjukkan tingkat kemiripan antar buku.
    - `items`: DataFrame yang berisi informasi buku seperti judul, penulis, dan rating rata-rata.
    - `k`: Jumlah rekomendasi buku yang ingin ditampilkan.

**Output: Contoh Top-N Recommendations**  
Misalkan pengguna memilih buku berjudul *"The Bellmaker (Redwall, #7)"*. Berikut adalah 5 buku teratas yang direkomendasikan berdasarkan kemiripan fitur:

| No.  | Judul Buku                                   | Penulis           | Rata-rata Rating |
|------|----------------------------------------------|-------------------|------------------|
| 1    | Redwall (Redwall, #1)                        | Brian Jacques     | 4.11             |
| 2    | Outcast of Redwall (Redwall, #8)             | Brian Jacques     | 3.90             |
| 3    | Salamandastron (Redwall, #5)                 | Brian Jacques     | 4.05             |
| 4    | Mattimeo (Redwall, #3)                       | Brian Jacques     | 4.13             |
| 5    | The Long Patrol (Redwall, #10)               | Brian Jacques     | 4.18             |

**Kelebihan**:
- Rekomendasi yang sangat relevan dengan preferensi pengguna.
- Tidak tergantung pada rating pengguna lain, sehingga dapat berfungsi meskipun pengguna baru.

**Kekurangan**:
- Rekomendasi mungkin kurang bervariasi dan terlalu terfokus pada buku-buku yang mirip.
- Bergantung pada kualitas fitur yang digunakan.

---

#### 2. Collaborative Filtering

**Deskripsi**:  
Pendekatan ini menggunakan interaksi pengguna dengan buku untuk memberikan rekomendasi. Model Nearest Neighbors (NN) digunakan untuk menghitung kesamaan antar pengguna berdasarkan rating yang mereka berikan kepada buku. Rekomendasi diberikan berdasarkan buku-buku yang disukai oleh pengguna dengan pola rating yang serupa.

**Metode**:  
- **Nearest Neighbors (NN)**: Mengidentifikasi pengguna yang mirip berdasarkan pola rating mereka, lalu merekomendasikan buku yang telah dibaca dan disukai oleh pengguna-pengguna tersebut.


**Fungsi yang Digunakan**:
- `top_n_recommendations`: Fungsi ini memberikan rekomendasi buku untuk pengguna tertentu berdasarkan rating yang diberikan oleh pengguna lain yang memiliki pola rating serupa.
  - **Parameter**:
    - `user_id`: ID pengguna untuk siapa rekomendasi akan diberikan.
    - `user_book_matrix`: Matriks yang menunjukkan rating pengguna terhadap buku.
    - `user_similarity_df`: DataFrame yang menunjukkan kesamaan antar pengguna.
    - `merged_df`: DataFrame yang berisi informasi buku.
    - `top_n`: Jumlah rekomendasi buku teratas yang ingin ditampilkan.

**Output: Contoh Top-N Recommendations**  
Misalkan pengguna dengan ID `user_id` memiliki rating terhadap beberapa buku. Berikut adalah contoh 5 rekomendasi teratas untuk pengguna berdasarkan kolaborasi dengan pengguna lain yang mirip:

| No. | Judul Buku                                              | Penulis                      |
|-----|--------------------------------------------------------|------------------------------|
| 1   | Harry Potter and the Prisoner of Azkaban               | J.K. Rowling, Mary GrandPré  |
| 2   | Harry Potter and the Half-Blood Prince                 | J.K. Rowling, Mary GrandPré  |
| 3   | Harry Potter and the Goblet of Fire                    | J.K. Rowling, Mary GrandPré  |
| 4   | Harry Potter Boxed Set Books 1-5                        | J.K. Rowling, Mary GrandPré  |
| 5   | Harry Potter and the Sorcerer's Stone                  | J.K. Rowling, Mary GrandPré  |

**Kelebihan**:
- Mampu merekomendasikan buku-buku baru yang mungkin belum dibaca oleh pengguna.
- Menggunakan data rating pengguna lain untuk menghasilkan rekomendasi yang lebih beragam.

**Kekurangan**:
- Dapat mengalami masalah cold start, terutama untuk pengguna atau buku baru.
- Kualitas rekomendasi sangat bergantung pada ketersediaan dan relevansi data rating.

### Evaluasi

Dalam proyek ini, kami menggunakan dua metrik evaluasi utama untuk mengukur kinerja sistem rekomendasi buku yang dikembangkan: Precision, Recall, dan F1 Score. Ketiga metrik ini relevan untuk menilai efektivitas model dalam memberikan rekomendasi buku yang sesuai dengan preferensi pengguna.

#### Metrik Evaluasi

1. **Precision**:  
   Precision mengukur proporsi buku yang direkomendasikan yang benar-benar relevan. Ini dihitung dengan membagi jumlah buku yang relevan (True Positives) dengan total buku yang direkomendasikan, yang merupakan jumlah buku relevan (True Positives) ditambah jumlah buku yang tidak relevan (False Positives). Dengan kata lain, rumus untuk Precision adalah:  
   - Precision = Jumlah Buku Relevan (True Positives) / (Jumlah Buku Relevan (True Positives) + Jumlah Buku Tidak Relevan (False Positives)).

2. **Recall**:  
   Recall mengukur proporsi buku relevan yang berhasil direkomendasikan. Ini dihitung dengan membagi jumlah buku yang relevan yang direkomendasikan (True Positives) dengan total buku relevan yang seharusnya direkomendasikan, yang merupakan jumlah buku relevan (True Positives) ditambah jumlah buku relevan yang tidak direkomendasikan (False Negatives). Dengan kata lain, rumus untuk Recall adalah:  
   - Recall = Jumlah Buku Relevan yang Direkomendasikan (True Positives) / (Jumlah Buku Relevan yang Seharusnya Direkomendasikan (True Positives) + Jumlah Buku Relevan yang Tidak Direkomendasikan (False Negatives)).

3. **F1 Score**:  
   F1 Score adalah metrik yang menggabungkan Precision dan Recall menjadi satu nilai tunggal untuk memberikan gambaran umum tentang kinerja model. F1 Score dihitung dengan menggunakan rumus yang menggabungkan Precision dan Recall. F1 Score memberikan bobot yang sama kepada kedua metrik ini, sehingga cocok digunakan ketika terdapat ketidakseimbangan antara kelas relevan dan tidak relevan. Rumus untuk F1 Score adalah:  
   - F1 Score = 2 × (Precision × Recall) / (Precision + Recall).

#### Hasil Evaluasi

Setelah melakukan evaluasi pada model rekomendasi, kami mendapatkan hasil berikut:

- **Content-Based Filtering**:
  - Precision: 1.0
  - Recall: 0.29
  - F1 Score: 0.44

- **Collaborative Filtering**:
  - Precision: 1.0
  - Recall: 0.71
  - F1 Score: 0.83

#### Benchmarking

Kami melakukan benchmarking untuk membandingkan kinerja kedua pendekatan sistem rekomendasi, yaitu Content-Based Filtering dan Collaborative Filtering, dengan menggunakan metrik evaluasi yang sama. Proses ini memungkinkan kami untuk menilai efektivitas masing-masing model dalam memberikan rekomendasi yang relevan dan sesuai dengan preferensi pengguna.

#### Penjelasan Hasil

Dari hasil evaluasi, dapat dilihat bahwa **Content-Based Filtering** memiliki Precision yang sempurna, yaitu 1.0, yang menunjukkan bahwa semua buku yang direkomendasikan relevan. Namun, Recall-nya cukup rendah, yaitu 0.29, yang berarti banyak buku relevan yang tidak direkomendasikan. Hal ini mengindikasikan bahwa meskipun rekomendasi yang diberikan tepat, model ini tidak berhasil mencakup seluruh buku relevan yang ada.

Sementara itu, **Collaborative Filtering** juga memiliki Precision yang sempurna, yaitu 1.0, menunjukkan bahwa semua rekomendasi yang diberikan juga relevan. Namun, Recall-nya lebih baik dibandingkan dengan Content-Based Filtering, yaitu 0.71, yang berarti model ini berhasil merekomendasikan lebih banyak buku relevan. F1 Score pada Collaborative Filtering adalah 0.83, yang menunjukkan bahwa ia lebih seimbang dalam hal Precision dan Recall dibandingkan dengan Content-Based Filtering.

Secara keseluruhan, hasil dari benchmarking ini menunjukkan bahwa meskipun kedua pendekatan memiliki kekuatan dalam hal memberikan rekomendasi yang relevan, Collaborative Filtering menunjukkan kinerja yang lebih baik dalam mencakup lebih banyak buku relevan. Hal ini penting untuk meningkatkan pengalaman pengguna dalam sistem rekomendasi buku.

### Kesimpulan

Dalam proyek ini, telah diidentifikasi beberapa pernyataan masalah yang sering dihadapi pengguna dalam mencari buku yang sesuai dengan minat dan preferensi mereka. Banyak pengguna mengalami kesulitan dalam menemukan buku di antara berbagai pilihan yang tersedia secara online. Selain itu, jumlah informasi yang melimpah sering kali membuat pengguna merasa bingung atau kewalahan, sehingga mereka mungkin melewatkan buku-buku yang relevan.

Untuk mengatasi masalah ini, sistem rekomendasi buku berbasis Content-Based Filtering dan Collaborative Filtering telah dirancang untuk membantu pengguna menemukan buku yang sesuai dengan minat mereka. Pendekatan berbasis konten menggunakan kesamaan fitur seperti judul dan penulis, sementara pendekatan kolaboratif memanfaatkan data interaksi pengguna untuk memberikan rekomendasi yang lebih personal.

Antarmuka pengguna yang intuitif juga diimplementasikan agar rekomendasi buku yang relevan dapat disajikan dengan cara yang mudah dipahami, sehingga pengguna tidak merasa kewalahan. Dengan kedua pendekatan ini, sistem diharapkan dapat memberikan rekomendasi yang lebih variatif dan relevan, mencakup buku-buku baru yang mungkin menarik bagi pengguna.

Secara keseluruhan, langkah-langkah yang diambil dalam proyek ini bertujuan untuk meningkatkan efektivitas sistem rekomendasi buku dan membantu pengguna menemukan buku yang sesuai dengan judul dan penulis yang mereka sukai. Dengan kombinasi pendekatan berbasis konten dan kolaboratif, diharapkan pengalaman pengguna dalam mencari buku dapat meningkat secara signifikan, dan pengguna tidak lagi melewatkan buku-buku yang sesuai dengan preferensi mereka.#   S i s t e m - R e k o m e n d a s i - B u k u  
 