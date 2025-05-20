# Proyek Klasifikasi Gambar: Klasifikasi Retina Mata (Binary Classification)

## Deskripsi Proyek

Proyek ini mengembangkan model deep learning untuk mengklasifikasikan gambar retina dan non-retina secara biner. Dataset yang digunakan berisi gambar retina berkualitas tinggi dan gambar non-retina sebagai pembanding. Proyek ini bertujuan untuk aplikasi deteksi otomatis di bidang oftalmologi dan berpotensi dikembangkan untuk biometrik, karena pola retina tiap orang unik.

---

## Download Dataset

Dataset retina untuk klasifikasi biner ini dapat diunduh di Kaggle melalui link berikut:  
[Retina Image for Binary Classification - Kaggle](https://www.kaggle.com/datasets/hardikchhipa28/retina-image-for-binary-classification/data)

---

## Lingkup Proyek

- **Dataset**: Gambar retina (label `train_images`) dan gambar non-retina (`non-dr`).
- **Tujuan**: Melatih model deep learning untuk membedakan antara gambar retina dan non-retina dengan akurasi tinggi.
- **Aplikasi**: Deteksi otomatis pada oftalmologi, screening penyakit retina, dan potensi biometrik.

---

## Teknologi dan Library

- TensorFlow dan Keras untuk pembuatan model CNN.
- Keras Tuner untuk hyperparameter tuning.
- Scikit-learn untuk split dataset dan evaluasi.
- Google Colab untuk eksekusi dan penyimpanan data (integrasi Google Drive).
- TensorFlow.js dan TensorFlow Lite untuk konversi model ke format web dan mobile.
- Visualisasi menggunakan Matplotlib dan Seaborn.

---

## Struktur Dataset

- Dataset berisi folder berlabel `train_images` (gambar retina) dan `non-dr` (gambar non-retina).
- Total data terbagi dalam:

  - Training: 4551 gambar  
  - Validation: 1517 gambar  
  - Testing: 1517 gambar

- Resolusi gambar bervariasi, beberapa contoh resolusi disediakan di dalam notebook.

---

## Data Preparation dan Augmentasi

- Dataset dibaca menggunakan Pandas DataFrame.
- Data dibagi stratifikasi ke train, validation, dan test.
- Augmentasi gambar untuk training menggunakan `ImageDataGenerator` dengan rotasi, geser, zoom, dan flip.
- Validasi dan test hanya melakukan normalisasi piksel.

---

## Arsitektur Model

- CNN sederhana dengan satu Conv2D layer, MaxPooling, Flatten, dan Dense output layer (sigmoid) untuk binary classification.
- Hyperparameter tuning dilakukan untuk menentukan jumlah filter Conv2D terbaik (32-128).
- Optimizer: Adam; Loss: Binary Crossentropy; Metric: Accuracy.

---

## Hyperparameter Tuning dengan Keras Tuner

Untuk mendapatkan konfigurasi model terbaik, digunakan **Keras Tuner** dengan algoritma **Hyperband**.

- Fungsi `build_model(hp)` memungkinkan penyesuaian jumlah filter Conv2D dari 32 hingga 128 filter dalam langkah 32.
- Model dikompilasi dengan optimizer Adam, loss binary_crossentropy, dan metric accuracy.
- Hyperband tuner menjalankan berbagai trial untuk mencari model dengan akurasi validasi terbaik dalam maksimal 10 epoch.
- Model terbaik dipilih berdasarkan val_accuracy tertinggi (~99.87%) dan digunakan untuk pelatihan lanjutan.

---

## Pelatihan Model

- Model dilatih selama 5 epoch menggunakan data generator.
- Akurasi validasi terbaik mencapai sekitar 99.87%.
- Grafik akurasi dan loss disajikan untuk evaluasi performa.

---

## Evaluasi

- Model diuji menggunakan data test dengan akurasi akhir > 99%.
- Confusion matrix dan classification report dapat dihasilkan untuk analisis mendalam (tidak dicantumkan di notebook).

---

## Konversi Model

- Model disimpan dalam format TensorFlow SavedModel.
- Model dikonversi ke format TensorFlow Lite untuk deployment di perangkat mobile.
- Model juga dikonversi ke format TensorFlow.js untuk aplikasi web.
- Semua artefak model dapat diunduh sebagai file zip dari Google Colab.

---

## Cara Menyimpan Label

Label kelas (`non-dr` dan `train_images`) disimpan ke file `tflite/label.txt` untuk referensi saat deployment TFLite.

---

## Cara Menggunakan

1. **Persiapkan dataset** dengan struktur folder sesuai label.
2. **Jalankan notebook** untuk training, tuning, evaluasi, dan konversi model.
3. **Unduh model** dalam format yang diinginkan (SavedModel, TFLite, TensorFlow.js).
4. **Gunakan label.txt** sebagai referensi label kelas pada aplikasi deployment.

---

## Requirements

- Python 3.x
- TensorFlow >= 2.13
- Keras Tuner
- Scikit-learn
- Pillow
- Matplotlib, Seaborn
- Google Colab (opsional, untuk eksekusi notebook)

