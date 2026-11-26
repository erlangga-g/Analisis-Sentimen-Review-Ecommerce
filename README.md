# Analisis Sentimen Ulasan Aplikasi Bukalapak menggunakan Naive Bayes

Repository ini berisi proyek analisis sentimen pada ulasan aplikasi **Bukalapak** di Google Play Store menggunakan algoritma **Multinomial Naive Bayes**.

## 🛠️ Alur Kerja & Metodologi

### 1. Data Scrapping (Penarikan Data)
* Menggunakan pustaka `google-play-scraper` untuk mengambil ulasan dari aplikasi Bukalapak (`com.bukalapak.android`).
* Diambil sebanyak **1200 data ulasan** versi Bahasa Indonesia (`lang='id'`, `country='id'`) dengan pengurutan ulasan yang paling relevan.
* Atribut yang digunakan dalam analisis ini difokuskan pada `content` (isi ulasan) dan `score` (rating bintang 1 hingga 5).

### 2. Data Labeling (Pemberian Label)
* Pelabelan ulasan otomatis berdasarkan skor rating bintang:
  * **Rating < 3**: Sentimen **Negatif**
  * **Rating >= 4**: Sentimen **Positif**
  * **Rating = 3**: Tidak digunakan (dihapus karena netral).

### 3. Data Cleaning & Preprocessing (Pembersihan Teks)
* **Case Folding**: Mengubah seluruh teks ulasan menjadi huruf kecil (lowercase).
* **Pembersihan Teks**: Menghapus tautan (URL), karakter non-alfabetis, tanda baca, serta angka menggunakan Regular Expression (`re`).
* **Stopword Removal**: Menghapus kata-kata umum bahasa Indonesia yang tidak memiliki nilai informasi signifikan (menggunakan `nltk` ditambah daftar kata buatan sendiri seperti *yg, aja, jg, gak, dkk*).
* **Tokenisasi**: Memotong kalimat menjadi token kata individual menggunakan `nltk.tokenize`.
* **Stemming**: Mengubah kata berimbuhan menjadi kata dasar menggunakan pustaka `Sastrawi` (contoh: *tagihan* menjadi *tagih*, *membantu* menjadi *bantu*).

### 4. Data Preparation (Persiapan Data)
* **Pembagian Data**: Memisahkan data menjadi Data Latih (Train) sebesar **80%** dan Data Uji (Test) sebesar **20%**.
* **Ekstraksi Fitur (TF-IDF)**: Mengubah teks ulasan menjadi representasi angka menggunakan `TfidfVectorizer`.
* **Handling Imbalanced Data (SMOTE)**: Mengatasi ketidakseimbangan jumlah data kelas positif dan negatif menggunakan teknik oversampling **SMOTE** agar jumlah data latih berimbang.

### 5. Modeling & Evaluasi (Pelatihan Model)
* Melatih model menggunakan algoritma **Multinomial Naive Bayes**.
* **Hasil Evaluasi Model**:
  * **Akurasi**: ~85.9%
  * **Presisi**: ~86.2%
  * **Recall**: ~85.9%
  * **F1-Score**: ~85.6%

---

## 📦 Pustaka (Libraries) yang Digunakan

Proyek ini dibangun menggunakan Python dengan pustaka-pustaka berikut:

* **Scrapping**: `google-play-scraper`
* **Manipulasi Data**: `pandas`, `numpy`
* **Visualisasi**: `matplotlib`, `seaborn`, `wordcloud`
* **Pemrosesan Bahasa Alami (NLP)**: `re`, `nltk`, `Sastrawi`
* **Machine Learning**: `scikit-learn` (untuk TF-IDF, Split Data, Naive Bayes, dan Evaluasi)
* **Oversampling**: `imblearn` (SMOTE)

---

## 📁 Struktur Repository

- `NaiveBayes.ipynb` — Notebook utama (*scraping*, *preprocessing*, TF-IDF, SMOTE, dan evaluasi Multinomial Naive Bayes)
- `scrapped_data.csv` — Data hasil *scraping* awal
- `bukalapaksentimen.csv` — Data ulasan & pelabelan sentimen
- `hasil_TextPreProcessing_bukalapak.csv` — Hasil teks setelah tahap *preprocessing*
