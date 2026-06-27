# 🌦️ Klasifikasi Prediksi Hujan - Rain in Australia

Proyek Machine Learning untuk memprediksi apakah besok akan hujan berdasarkan data cuaca historis Australia.

---

## Anggota Kelompok
1. I Kadek Rio Adi Pranata Kusuma (103132400029)
2. Maysa Azhra Fauziyyah (103132430005)

---

## Deskripsi Permasalahan

Prediksi cuaca merupakan salah satu tantangan utama dalam bidang meteorologi dan machine learning. Proyek ini bertujuan untuk membangun model klasifikasi yang dapat memprediksi apakah **besok akan terjadi hujan** (`RainTomorrow`) berdasarkan berbagai indikator cuaca hari ini seperti suhu, kelembaban, tekanan udara, kecepatan angin, dan lainnya.

Permasalahan ini bersifat **binary classification**:
- `0` (No) = Tidak hujan besok
- `1` (Yes) = Hujan besok

Lalu, kenapa kami memilih data Australia dibandingkan Indonesia?
Karena "Dataset Australia dipilih karena ketersediaan data yang lengkap dan terpercaya. Meskipun data berasal dari Australia, prinsip meteorologi bersifat universal. Sebagai contoh, variabel seperti Humidity3pm dan Pressure3pm adalah indikator hujan yang berlaku di mana saja. Model ini dapat diadaptasi untuk data Indonesia dengan melatih ulang menggunakan data dari BMKG. Hal ini sejalan dengan tujuan pembelajaran untuk memahami proses end-to-end machine learning, terlepas dari geografis data."

---

## Dataset

**Nama:** Rain in Australia  
**Sumber:** [Kaggle - Weather Dataset Rattle Package](https://www.kaggle.com/datasets/jsphyg/weather-dataset-rattle-package)  
**Format:** CSV  
**Jumlah Data:** 145.460 sampel
**Jumlah Fitur:** 23 kolom 

### Fitur Dataset

| Fitur | Deskripsi | Tipe |
|-------|-----------|------|
| `Location` | Kota pengamatan | Kategorik |
| `MinTemp` | Suhu minimum hari ini (°C) | Numerik |
| `MaxTemp` | Suhu maksimum hari ini (°C) | Numerik |
| `Rainfall` | Curah hujan hari ini (mm) | Numerik |
| `Evaporation` | Penguapan (mm) | Numerik |
| `Sunshine` | Durasi sinar matahari (jam) | Numerik |
| `WindGustDir` | Arah angin kencang | Kategorik |
| `WindGustSpeed` | Kecepatan angin kencang (km/h) | Numerik |
| `WindDir9am` / `WindDir3pm` | Arah angin pagi/sore | Kategorik |
| `WindSpeed9am` / `WindSpeed3pm` | Kecepatan angin pagi/sore (km/h) | Numerik |
| `Humidity9am` / `Humidity3pm` | Kelembaban pagi/sore (%) | Numerik |
| `Pressure9am` / `Pressure3pm` | Tekanan udara pagi/sore (hPa) | Numerik |
| `Cloud9am` / `Cloud3pm` | Tutupan awan pagi/sore (okta) | Numerik |
| `Temp9am` / `Temp3pm` | Suhu pagi/sore (°C) | Numerik |
| `RainToday` | Apakah hujan hari ini? | Kategorik |
| `RainTomorrow` | **Target: Apakah hujan besok?** | Kategorik |

---

## Tahapan Preprocessing

1. **Imputasi Missing Values**
   - Fitur numerik: diisi dengan nilai **median**
   - Fitur kategorik: diisi dengan nilai **modus**

2. **Label Encoding**
   - Semua variabel kategorik diubah menjadi numerik menggunakan `LabelEncoder`
   - Target `RainTomorrow`: `No` → `0`, `Yes` → `1`

3. **Train-Test Split**
   - Rasio: **80% training / 20% testing**
   - Stratified split untuk menjaga proporsi kelas

4. **Standarisasi Fitur**
   - Menggunakan `StandardScaler` khusus untuk model Logistic Regression

---

## Metode yang Digunakan

Proyek ini membandingkan tiga algoritma Machine Learning:

| Model | Deskripsi |
|-------|-----------|
| **Logistic Regression** | Model linear sebagai baseline; bekerja baik untuk klasifikasi biner |
| **Decision Tree** | Model berbasis pohon keputusan; mudah diinterpretasikan |
| **Random Forest** | Ensemble dari banyak Decision Tree; lebih robust dan akurat |

**Metrik Evaluasi:** Accuracy, Precision, Recall, F1-Score, AUC-ROC, Confusion Matrix, Cross Validation (5-fold)

---

## Struktur Repository

```
weather-rain-prediction/
├── dataset/
│   └── weatherAUS_sample.csv         # Dataset yang digunakan
├── notebook/
│   └── Rain_Prediction_Classification.ipynb  # Notebook utama
├── images/
│   ├── 01_target_distribution.png
│   ├── 02_missing_values.png
│   ├── 03_numeric_distributions.png
│   ├── 04_correlation_heatmap.png
│   ├── 05_boxplot_features.png
│   ├── 06_confusion_matrices.png
│   ├── 07_model_comparison.png
│   ├── 08_roc_curve.png
│   └── 09_feature_importance.png
├── requirements.txt
├── .gitignore
└── README.md
```

---

## Cara Menjalankan Program

### 1. Clone repository

```bash
git clone https://github.com/username/weather-rain-prediction.git
cd weather-rain-prediction
```

### 2. Install dependensi

```bash
pip install -r requirements.txt
```

### 3. Jalankan notebook

```bash
jupyter notebook notebook/Rain_Prediction_Classification.ipynb
```

Jalankan seluruh cell secara berurutan dari atas ke bawah.

---

## Hasil Eksperimen & Evaluasi
**Perbandingan Performa Model**
| Model | Accuracy | Precision | Recall | F1-Score | AUC-ROC |
|:------|---------:|----------:|-------:|---------:|--------:|
| Logistic Regression | 84.70% | 72.39% | 48.78% | 58.29% | 86.21% |
| Decision Tree | 84.38% | 72.00% | 46.98% | 56.86% | 84.96% |
| **Random Forest** | **85.17%** | **77.58%** | 45.49% | 57.35% | **87.14%** |

> Nilai aktual dapat bervariasi sedikit tergantung environment. Jalankan notebook untuk hasil yang tepat.

**Cross Validation (5-fold)-F1-Score**
| Model | Mean F1-Score | Std Dev | Keterangan |
|:------|--------------:|--------:|:-----------|
| Logistic Regression | 0.5686 | ± 0.0018 | Stabil, variance kecil |
| Decision Tree | 0.5581 | ± 0.0106 | Variance lebih tinggi |
| Random Forest | 0.5605 | ± 0.0031 | Stabil, konsisten |

## 🏆 Model Terbaik
**Random Forest** terpilih sebagai model terbaik dengan alasan:
- Accuracy tertinggi: **85.17%**
- AUC-ROC tertinggi: **87.14%**
- Performa stabil dalam cross validation
- Robust terhadap overfitting
  
**Top 5 Fitur Terpenting (Random Forest)**
| Rank | Fitur | Importance Score |
|:----:|:------|-----------------:|
| 1 | **Humidity3pm** | **32.78%** |
| 2 | Rainfall | 9.41% |
| 3 | RainToday | 7.24% |
| 4 | Sunshine | 7.09% |
| 5 | WindGustSpeed | 6.26% |

### Visualisasi Hasil
Semua plot tersimpan di folder `images/`, meliputi:
- Distribusi kelas target
  <img width="1649" height="738" alt="image" src="https://github.com/user-attachments/assets/d583e06b-5709-42e7-bc57-4e679842b148" /> 
- Analisis missing values
  <img width="1480" height="729" alt="image" src="https://github.com/user-attachments/assets/8adfb1f3-594e-427c-a9ad-c8dfa757a987" />
- Distribusi fitur numerik
  <img width="2385" height="1769" alt="image" src="https://github.com/user-attachments/assets/022a0702-fda6-4359-8705-0240b77ec655" />
- Heatmap korelasi
  <img width="1660" height="1483" alt="image" src="https://github.com/user-attachments/assets/3b588654-8ff5-4c58-849f-853c8698605b" />
- Boxplot fitur kunci vs target
  <img width="2385" height="738" alt="image" src="https://github.com/user-attachments/assets/6ba0a567-e553-45fd-936c-dc347c046736" />
- Confusion matrix ketiga model
  <img width="2210" height="591" alt="image" src="https://github.com/user-attachments/assets/d3490c96-eed2-47c8-82c3-0f829cc4a09d" />
- Grafik perbandingan metrik
  <img width="1933" height="882" alt="image" src="https://github.com/user-attachments/assets/edaa0dd8-7d9d-419b-9bda-4d488cbccdd2" />
- ROC Curve
  <img width="1183" height="878" alt="image" src="https://github.com/user-attachments/assets/39b099f6-e86d-471b-82f9-14b080c5de8f" />
- Feature importance (Random Forest)
  <img width="1335" height="1029" alt="image" src="https://github.com/user-attachments/assets/18da5696-f4f6-4e3d-a020-dad6d08f3c1a" />

---

## Kesimpulan

1. **Random Forest** terbukti sebagai model terbaik dengan Accuracy 85.17% dan AUC-ROC 87.14%, berkat kemampuannya menggabungkan banyak pohon keputusan untuk mengurangi variance.
2.  **Fitur terpenting** dalam prediksi hujan adalah Humidity3pm, Rainfall, RainToday, Sunshine, dan WindGustSpeed — sesuai dengan pengetahuan meteorologi bahwa kelembaban dan curah hujan merupakan prediktor cuaca yang kuat.
3.  **Decision Tree** memiliki interpretabilitas lebih tinggi namun rentan terhadap overfitting dibanding Random Forest.
4.   **Logistic Regression** sebagai baseline linear masih memberikan performa cukup baik (84.70%) mengingat kesederhanaannya.

**Rekomendasi:** Random Forest dipilih sebagai model final karena lebih robust terhadap overfitting dan mampu menangani fitur dengan distribusi beragam.

---

## Referensi

- Dataset: [Kaggle - Rain in Australia](https://www.kaggle.com/datasets/jsphyg/weather-dataset-rattle-package)
- Scikit-learn Documentation: https://scikit-learn.org/stable/
- Pedregosa et al. (2011). *Scikit-learn: Machine Learning in Python*. JMLR 12, pp. 2825-2830.

## Informasi Tugas
| **Mata Kuliah** | Machine Learning |
|:---|:---|
| **Jenis Tugas** | Tugas Besar / Final Project |
| **Topik** | Klasifikasi Prediksi Hujan |
| **Algoritma** | Logistic Regression, Decision Tree, Random Forest |
| **Dataset** | Rain in Australia (Kaggle) |
| **Link Repository** | [GitHub](https://github.com/maysaazhra/Rain-Prediction-Classification) |
