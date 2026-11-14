# Code Smell Python — SQEE

Repository ini berisi artefak eksperimen untuk penelitian tesis:

**Analisis Ensemble Learning dan Teknik Penanganan Ketidakseimbangan Kelas untuk Deteksi Code Smell pada Source Code Python**

**Peneliti:** Popo Nugroho  
**NIM:** 14250016  
**Program Studi:** Magister Ilmu Komputer (S2), Universitas Nusa Mandiri  
**Mata Kuliah:** Software Quality & Effort Estimation (SQEE)

## Ruang Lingkup Penelitian

Penelitian ini mengevaluasi deteksi dua jenis code smell pada source code Python:

- Large Class (LC)
- Long Method (LM)

Eksperimen membandingkan empat strategi penanganan ketidakseimbangan kelas:

- None
- SMOTE
- ADASYN
- Random Oversampling (ROS)

dengan lima model ensemble:

- Bagging
- Gradient Boosting
- Max Voting
- AdaBoost
- XGBoost

## Pipeline Eksperimen

Tahapan utama eksperimen:

1. Audit dataset
2. Stratified 10-Fold Cross-Validation
3. Min-Max Scaling
4. Chi-Square SelectKBest Top-10
5. Penanganan class imbalance pada training fold
6. Pelatihan model ensemble
7. Evaluasi performa
8. Statistical analysis
9. Ablation study
10. Ekspor artefak hasil

Seluruh preprocessing yang mempelajari karakteristik data dilakukan hanya pada **training fold** untuk mencegah data leakage. Test fold tidak digunakan untuk membentuk scaler, memilih fitur, ataupun melakukan resampling.

## Dataset

Dataset publik yang digunakan berasal dari:

**Sandouka & Aljamaan — Python Code Smells Detection Dataset**

Zenodo DOI:  
https://doi.org/10.5281/zenodo.7512516

Hasil audit terhadap file dataset aktual:

| Dataset | Total Observasi | Smelly | Non-Smelly | Predictor |
|---|---:|---:|---:|---:|
| Large Class | 1000 | 200 | 800 | 19 |
| Long Method | 894 | 209 | 685 | 19 |

Predictor terdiri dari 7 raw software metrics dan 12 Halstead metrics.

## Metrik Evaluasi

Metrik utama:

- Matthews Correlation Coefficient (MCC)

Metrik pendukung:

- AUC-PR
- Macro-F1
- Recall
- Accuracy
- Precision
- F1
- Cohen's Kappa
- AUC-ROC

## Statistical Analysis

Analisis statistik dilakukan menggunakan:

- Friedman Test
- Wilcoxon Signed-Rank Test
- Holm Correction
- Rank-Biserial Correlation

## Ablation Study

Empat kondisi dibandingkan secara terkontrol menggunakan XGBoost:

- Baseline
- SMOTE only
- Chi-Square only
- SMOTE + Chi-Square

## Reproducibility

Konfigurasi utama eksperimen:

- `random_state = 42`
- Stratified 10-Fold Cross-Validation
- Chi-Square Top-K = 10
- scikit-learn 1.8.0
- imbalanced-learn 0.14.1
- XGBoost 3.1.3
- SciPy 1.17.0
- statsmodels 0.14.6

## Google Colab

Notebook eksperimen dapat dibuka melalui:

https://colab.research.google.com/drive/1XMv5IvF32iSI38xDBZqQC9ZoFT0krsKB

## Notebook

Notebook utama:

`Penelitian_Code_Smell_Popo_14250016.ipynb`

## Catatan Reproducibility

Dokumentasi benchmark menyebutkan 18 fitur dan 1.000 observasi Long Method, sedangkan audit terhadap file CSV aktual menemukan 19 predictor dan 894 observasi Long Method.

Perbedaan tersebut dicatat sebagai isu reproducibility dan dilaporkan secara transparan.

Komposisi Max Voting merupakan rekonstruksi eksperimen karena detail base learner pada studi acuan tidak tersedia secara lengkap.
