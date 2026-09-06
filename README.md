# Prediksi Kelulusan Mahasiswa: Comparative Analysis Decision Tree & Gaussian Naïve Bayes

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

Proyek ini bertujuan untuk membangun dan membandingkan performa model *Machine Learning* (**Decision Tree Classifier** dan **Gaussian Naïve Bayes**) dalam memprediksi ketepatan waktu kelulusan mahasiswa berdasarkan indikator akademis dan non-akademis.

---

## Tim Penyusun

**Kelompok Machine Learning - Program Studi Informatika, Universitas Bengkulu**
* **Nayla Viona Azahra** (G1A024045)
* **Angelita Rahmatun Annisa** (G1A024067)
* **Tri Haiji Januarli** (G1A024069)

**Dosen Pengampu:** Ir. Arie Vatresia, S.T., M.T.I., Ph.D., IPP.

---

## Ringkasan Dataset & Preprocessing

Dataset yang digunakan terdiri dari **500 sampel data mahasiswa** dengan fitur-fitur utama meliputi IPK, Kehadiran, Jam Belajar, Organisasi, Penghasilan Orang Tua, Jenis Kelamin, dan Status Beasiswa.

 Tahapan *preprocessing* data yang dilakukan:
1. **Handling Missing Values:** Imputasi nilai kosong menggunakan nilai *median* pada variabel numerik (`IPK`, `Kehadiran`) dan *modus* pada variabel kategorikal.
2. **Feature Encoding:** Mengubah variabel kategorikal teks menjadi numerik menggunakan `LabelEncoder` serta pemetaan eksplisit untuk variabel target (`0: Tidak Tepat Waktu`, `1: Tepat Waktu`).
3. **Train-Test Split:** Dataset dibagi menjadi **80% Data Latih (400 sampel)** dan **20% Data Uji (100 sampel)** menggunakan teknik *stratified sampling* (`stratify=y`).

---

##  Hasil Evaluasi Performa Model

Pengujian dilakukan pada **100 data uji (test set)** dengan hasil sebagai berikut:

| Model | Akurasi | Precision (Tepat) | Recall (Tepat) | F1-Score (Tepat) | Status / Catatan |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Gaussian Naïve Bayes** | **91.00%** | **85.00%** | **91.89%** | **88.31%** | **Model Rekomendasi Utama** |
| **Decision Tree (`max_depth=3`)** | 87.00% | 78.57% | 89.19% | 83.54% | Pemangkasan mencegah overfitting |
| **Decision Tree (Full Depth)** | 83.00% | 73.81% | 83.78% | 78.48% | Terindikasi *Overfitting* |

### Temuan Utama:
* **Model Terbaik:** Gaussian Naïve Bayes meraih performa tertinggi secara menyeluruh dengan **Akurasi 91.00%** dan **Recall 91.89%**, sangat efektif meminimalisasi *False Negative* pada deteksi dini keterlambatan kelulusan.
* **Fenomena Overfitting:** Pembatasan kedalaman pohon (`max_depth=3`) berhasil meningkatkan performa *Decision Tree* sebesar 4% dibandingkan model *Full Depth* yang mengalami penataan berlebih (*overfitting*) pada data latih.

---

## Analisis Bias & Etika Algoritma

Penggunaan variabel seperti `Penghasilan_Ortu` dan `Jenis_Kelamin` berpotensi memicu bias sosial diskriminatif jika diterapkan tanpa pengawasan:
* **Mitigasi Bias:** Menerapkan *Feature Suppression* (menghapus variabel `Jenis_Kelamin` dari fitur latih) dan memisahkan `Penghasilan_Ortu` sebagai syarat kelayakan (*eligibility threshold*) terpisah.
* **Human-in-the-Loop:** Keputusan akhir kelulusan atau penerimaan beasiswa tetap berada di tangan komite manusia, di mana model hanya berfungsi sebagai sistem penunjang keputusan (*decision support tool*).
