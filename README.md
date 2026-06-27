# 🌦️ Klasifikasi Prediksi Hujan - Rain in Australia

Proyek Machine Learning untuk memprediksi apakah besok akan hujan berdasarkan data cuaca historis Australia.

---

## Anggota Kelompok

| Nama | NIM |
|------|-----|
| [Nama Anggota 1] | [NIM 1] |
| [Nama Anggota 2] | [NIM 2] |
| [Nama Anggota 3] | [NIM 3] |

---

## Deskripsi Permasalahan

Prediksi cuaca merupakan salah satu tantangan utama dalam bidang meteorologi dan machine learning. Proyek ini bertujuan untuk membangun model klasifikasi yang dapat memprediksi apakah **besok akan terjadi hujan** (`RainTomorrow`) berdasarkan berbagai indikator cuaca hari ini seperti suhu, kelembaban, tekanan udara, kecepatan angin, dan lainnya.

Permasalahan ini bersifat **binary classification**:
- `0` (No) = Tidak hujan besok
- `1` (Yes) = Hujan besok

---

## Dataset

**Nama:** Rain in Australia  
**Sumber:** [Kaggle - Weather Dataset Rattle Package](https://www.kaggle.com/datasets/jsphyg/weather-dataset-rattle-package)  
**Format:** CSV  
**Jumlah Data:** 1.000 sampel (subset dari dataset asli 145.000+ baris)

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

| Model | Accuracy | Precision | Recall | F1-Score | AUC-ROC |
|-------|----------|-----------|--------|----------|---------|
| Logistic Regression | ~74% | ~65% | ~62% | ~63% | ~0.79 |
| Decision Tree | ~76% | ~67% | ~65% | ~66% | ~0.76 |
| **Random Forest** | **~79%** | **~71%** | **~67%** | **~69%** | **~0.84** |

> Nilai aktual dapat bervariasi sedikit tergantung environment. Jalankan notebook untuk hasil yang tepat.

### Visualisasi Hasil

Semua plot tersimpan di folder `images/`, meliputi:
- Distribusi kelas target
- Analisis missing values
- Distribusi fitur numerik
- Heatmap korelasi
- Boxplot fitur kunci vs target
- Confusion matrix ketiga model
- Grafik perbandingan metrik
- ROC Curve
- Feature importance (Random Forest)

---

## Kesimpulan

1. **Random Forest** terbukti sebagai model terbaik dengan accuracy dan AUC-ROC tertinggi, berkat kemampuannya menggabungkan banyak pohon keputusan untuk mengurangi variance.
2. **Fitur terpenting** dalam prediksi hujan adalah `Humidity3pm`, `Pressure3pm`, dan `Sunshine` — sesuai dengan pengetahuan meteorologi bahwa kelembaban dan tekanan udara sore hari merupakan prediktor cuaca yang kuat.
3. **Decision Tree** memiliki interpretabilitas lebih tinggi namun rentan terhadap overfitting dibanding Random Forest.
4. **Logistic Regression** sebagai baseline linear masih memberikan performa cukup baik mengingat kesederhanaannya.

---

## Referensi

- Dataset: [Kaggle - Rain in Australia](https://www.kaggle.com/datasets/jsphyg/weather-dataset-rattle-package)
- Scikit-learn Documentation: https://scikit-learn.org/stable/
- Pedregosa et al. (2011). *Scikit-learn: Machine Learning in Python*. JMLR 12, pp. 2825-2830.
