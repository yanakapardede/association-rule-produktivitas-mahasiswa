# PROJECT AKHIR PENAMBANGAN DATA KELOMPOK 10

# Association Rule Mining untuk Menemukan Pola Perilaku dan Produktivitas Mahasiswa

## Team Members

| Name | NIM |
|---|---|
| Yanaka Sofia Pardede | 24031554065 |
| Fajria Rasmi Ridha Rumkel | 24031554191 |
| Annisa Ramadhani | 24031554206 |

## Project Overview

Proyek ini bertujuan untuk menemukan pola hubungan antara kebiasaan mahasiswa dan tingkat produktivitas akademik menggunakan metode **Association Rule Mining**. Analisis dilakukan terhadap variabel waktu belajar, durasi tidur, penggunaan media sosial, tingkat stres, penggunaan ponsel, olahraga, dan kehadiran.

Data numerik terlebih dahulu dikategorikan menjadi kelompok rendah, sedang, dan tinggi, kemudian diubah ke dalam bentuk transaksi. Pola kemunculan bersama dicari menggunakan dua algoritma, yaitu **Apriori** dan **FP-Growth**, lalu dievaluasi dengan metrik **support**, **confidence**, dan **lift**. Kedua algoritma juga dibandingkan berdasarkan waktu komputasi dan jumlah pola yang dihasilkan.

### Tujuan

1. Mengolah data perilaku mahasiswa ke dalam bentuk transaksi untuk Frequent Pattern Mining.
2. Menemukan frequent itemset dan association rule menggunakan Apriori dan FP-Growth.
3. Mengidentifikasi hubungan antara kebiasaan mahasiswa dan tingkat produktivitas akademik.
4. Membandingkan kedua algoritma dari sisi waktu komputasi dan jumlah pola yang dihasilkan.

## Dataset Information

- **Dataset:** Student Productivity and Behavior Dataset
- **File:** `student_productivity_distraction_dataset_20000.csv`
- **Total Records:** 20,000
- **Selected Attributes:** 8
- **Data Quality:** Tidak ditemukan missing value maupun data duplikat

> File dataset tidak diunggah ke repository. Sesuaikan path dataset pada notebook sebelum menjalankannya.

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

Dataset dibaca menggunakan Python dan Pandas. Tahap ini mencakup pengecekan ukuran data, struktur kolom, missing value, data duplikat, statistik deskriptif, boxplot outlier, distribusi variabel, dan korelasi antarvariabel.

### 2. Variable Selection

Dipilih 8 variabel yang relevan dengan perilaku dan produktivitas mahasiswa.

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

**Interpretasi**

- Sekitar 11,5% mahasiswa memiliki kombinasi waktu belajar rendah dan produktivitas rendah. Dari semua mahasiswa dengan waktu belajar rendah, sekitar 72,4% berproduktivitas rendah, dan hubungan ini 2,6 kali lebih sering terjadi dibanding kemunculan acak.
- Hampir semua mahasiswa berproduktivitas tinggi (97,8%) berada pada kategori waktu belajar tinggi.

## Key Findings

- Apriori dan FP-Growth menghasilkan jumlah frequent itemset dan association rule yang sama.
- Waktu belajar memiliki keterkaitan kuat dengan produktivitas akademik, baik pada kategori rendah maupun tinggi.
- Pada data dan implementasi ini, Apriori menyelesaikan proses mining lebih cepat dibanding FP-Growth.

## Limitations

- Rule menunjukkan **keterkaitan**, bukan hubungan sebab-akibat.
- Batas kategori (rendah, sedang, tinggi) ditentukan manual, sehingga hasil rule dapat berubah jika batasnya diubah.
- Hasil juga bergantung pada ambang minimum support dan confidence yang dipilih.
- Waktu komputasi berasal dari satu kali eksekusi di Google Colab. Perbandingan ini berlaku pada dataset dan implementasi yang digunakan, bukan kesimpulan umum bahwa satu algoritma selalu lebih cepat.

## How to Run

1. Buka `notebook/Kode_Project_Penambangan_Data_Kelompok_10.ipynb` di Google Colab.
2. Unggah dataset ke Google Drive, lalu ubah variabel `path` pada bagian Load Dataset.
3. Jalankan seluruh sel secara berurutan.

Untuk menjalankan di lokal, hapus sel `drive.mount` dan pasang library:

```bash
pip install pandas numpy matplotlib seaborn mlxtend
```
