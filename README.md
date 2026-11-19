# PROJECT AKHIR PENAMBANGAN DATA KELOMPOK 10

# Association Rule Mining untuk Menemukan Pola Perilaku dan Produktivitas Mahasiswa

## Team Members

| Name | NIM |
|---|---|
Yanaka Sofia Pardede | 24031554065 |
Fajria Rasmi Ridha Rumkel | 24031554191 |
Annisa Ramadhani | 24031554206 |

## Project Overview

Proyek ini bertujuan untuk menemukan pola hubungan antara kebiasaan mahasiswa dan tingkat produktivitas akademik menggunakan metode **Association Rule Mining**. Analisis dilakukan terhadap variabel waktu belajar, durasi tidur, penggunaan media sosial, tingkat stres, penggunaan ponsel, olahraga, dan kehadiran.

Data numerik terlebih dahulu dikategorikan menjadi kelompok rendah, sedang, dan tinggi, kemudian diubah ke dalam bentuk transaksi. Pola kemunculan bersama dicari menggunakan dua algoritma, yaitu **Apriori** dan **FP-Growth**, lalu dievaluasi dengan metrik **support**, **confidence**, dan **lift**. Kedua algoritma juga dibandingkan berdasarkan waktu komputasi dan jumlah pola yang dihasilkan.

## Dataset Information

- **Dataset:** Student Productivity and Behavior Dataset
- **File:** `student_productivity_distraction_dataset_20000.csv`
- **Total Records:** 20,000
- **Selected Attributes:** 8
- **Data Quality:** Tidak ditemukan missing value maupun data duplikat

### Main Attributes

- study_hours_per_day
- sleep_hours
- social_media_hours
- stress_level
- phone_usage_hours
- exercise_minutes
- attendance_percentage
- productivity_score

## Data Preparation Process

### 1. Data Understanding & Exploration

Dataset dibaca dari file CSV menggunakan Python dan Pandas. Tahap ini mencakup pengecekan ukuran data, struktur kolom, missing value, data duplikat, dan statistik deskriptif.

### 2. Preprocessing

Tahapan preprocessing meliputi:

- Seleksi 8 variabel yang relevan dengan perilaku dan produktivitas mahasiswa.
- Pengecekan outlier menggunakan boxplot.
- Eksplorasi distribusi variabel dan korelasi antarvariabel.

### 3. Discretization

Variabel numerik dikategorikan menggunakan `pd.cut` dengan batas sebagai berikut:

| Variable | Category (range) |
|---|---|
| Study hours | study_low (0–2), study_medium (2–5), study_high (5–24) |
| Sleep hours | sleep_low (0–5), sleep_good (5–7), sleep_high (7–24) |
| Social media hours | social_low (0–2), social_medium (2–5), social_high (5–24) |
| Stress level | stress_low (0–3), stress_medium (3–7), stress_high (7–10) |
| Phone usage hours | phone_low (0–3), phone_medium (3–6), phone_high (6–24) |
| Exercise minutes | exercise_low (0–20), exercise_medium (20–60), exercise_high (60–300) |
| Attendance (%) | attendance_low (0–70), attendance_medium (70–85), attendance_high (85–100) |
| Productivity score | productivity_low (0–40), productivity_medium (40–70), productivity_high (70–100) |

### 4. Transformation & Encoding

Setiap mahasiswa diubah menjadi satu transaksi yang berisi 8 item kategori. Transaksi kemudian dikodekan menjadi tabel biner (True/False) menggunakan `TransactionEncoder` dari MLxtend.

## Association Rule Mining

### Algorithms

| Algorithm | Description |
|---|---|
| Apriori | Mencari frequent itemset secara bertahap berdasarkan minimum support, lalu membentuk rule berdasarkan minimum confidence |
| FP-Growth | Mencari frequent itemset melalui struktur FP-Tree tanpa membangkitkan kandidat itemset, lalu membentuk rule |

### Parameters

| Parameter | Value |
|---|---|
| Minimum Support | 0.1 |
| Minimum Confidence | 0.5 |
| Rule Sorting | Lift (descending) |

### Evaluation Metrics

- **Support:** seberapa sering kombinasi item muncul di seluruh transaksi.
- **Confidence:** tingkat kepercayaan bahwa suatu item muncul ketika item lain sudah muncul.
- **Lift:** kekuatan hubungan dibandingkan kemunculan acak. Lift lebih dari 1 menunjukkan keterkaitan positif.

## Analysis Performed

1. Frequent Itemset Apriori
2. Frequent Itemset FP-Growth
3. Association Rule Apriori (Top 10 by Lift)
4. Association Rule FP-Growth (Top 10 by Lift)
5. Perbandingan Waktu Komputasi
6. Perbandingan Jumlah Frequent Itemset dan Association Rule
7. Hubungan Support vs Confidence

## Visualization

Visualisasi dibuat menggunakan **Matplotlib** dan **Seaborn** di dalam notebook.

| No. | Visualization |
|---|---|
| 1 | Boxplot Outlier per Variabel |
| 2 | Distribusi Variabel (Histogram dan KDE) |
| 3 | Correlation Heatmap |
| 4 | Perbandingan Waktu Komputasi Apriori vs FP-Growth |
| 5 | Support vs Confidence |

## Results

### Frequent Itemset & Rule

| Algorithm | Computation Time | Frequent Itemset | Association Rule |
|---|---:|---:|---:|
| Apriori | 0.129 s | 203 | 157 |
| FP-Growth | 12.889 s | 203 | 157 |

### Top Items by Support

| Item | Support |
|---|---:|
| attendance_low | 0.5004 |
| exercise_high | 0.4939 |
| social_medium | 0.3767 |
| study_medium | 0.3145 |
| stress_high | 0.2991 |

### Notable Rules

| Rule | Support | Confidence | Lift |
|---|---:|---:|---:|
| study_low → productivity_low | 0.115 | 0.724 | 2.613 |
| productivity_high → study_high | [isi] | 0.978 | 1.856 |

## Key Findings

Berdasarkan hasil analisis yang telah dilakukan, diperoleh beberapa temuan utama:

- Apriori dan FP-Growth menghasilkan jumlah frequent itemset dan association rule yang sama.
- Pada data dan implementasi ini, Apriori menyelesaikan proses mining lebih cepat dibandingkan FP-Growth.
- Waktu belajar memiliki keterkaitan dengan produktivitas akademik.
- Mahasiswa dengan waktu belajar rendah cenderung berproduktivitas rendah (confidence 0.724, lift 2.613).
- Mahasiswa berproduktivitas tinggi hampir selalu berada pada kategori waktu belajar tinggi (confidence 0.978).
- Rule menunjukkan keterkaitan, bukan hubungan sebab-akibat.
- Hasil bergantung pada batas diskretisasi dan ambang minimum support/confidence yang dipilih.
- Perbandingan waktu berlaku pada dataset dan implementasi yang digunakan, bukan kesimpulan umum bahwa satu algoritma selalu lebih cepat.

## How to Run

1. Buka `notebook/Kode_Project_Penambangan_Data_Kelompok_10.ipynb` di Google Colab.
2. Unggah dataset ke Google Drive, lalu ubah variabel `path` pada bagian Load Dataset.
3. Jalankan seluruh sel secara berurutan.

Untuk menjalankan di lokal, hapus sel `drive.mount` dan pasang library:

```bash
pip install pandas numpy matplotlib seaborn networkx mlxtend
```
