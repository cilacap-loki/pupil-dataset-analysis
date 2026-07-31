# **Arsitektur Program & Pipeline SOP Riset Pupil**
## **Indeks Master Standar Operasional Prosedur (SOP-01 s/d SOP-09)**

Alur kerja komputasi platform **Pupil Dataset Processor (PDP)** dibakukan ke dalam **3 Fase Utama** yang terkelompok ke dalam 3 berkas dokumentasi terpisah berikut:

---

### 📂 **1. [FASE 1: Data Preparation & Cleaning](fase1_data_preparation.md)**
* **SOP-01**: Inisialisasi Environment & Konfigurasi Workspace Setup (Google Drive Mount & Path Initialization).
* **SOP-02**: Ekstraksi Direct Frame PNG Lossless (Pemindaian Kedipan Minimal & Potong Segmen Optimal 30 Detik = 1.500 Frame).
* **SOP-03**: Pra-Pemrosesan Grayscale & Motion-Stabilized Crop ROI 800x800 px (Metode EMA Stabilization $\alpha=0.15$).

---

### 📂 **2. [FASE 2: Pipeline Otomasi & Segmentasi](fase2_pipeline_otomasi.md)**
* **SOP-04**: Segmentasi Mask Pupil Otomatis & Video Verifikasi Real-Time (Ambang batas adaptif $T = V_{\text{min}} + 25$, Glint Removal, Geometri Simetris Area-Equivalent $D = 2\sqrt{\text{Area}/\pi}$, Penyimpanan `1_Mask_Biner/`, dan Rendering 1 Video Terpadu MP4).
* **SOP-05**: Tracking Pupil, Filter Outlier Moving Median ($W=150$), & Analisis Sinyal Temporal Fluktuasi Hippus.
* **SOP-06**: Generator Laporan PDF Diagnostik Klinis Individual (ReportLab Failsafe Anti-Crash).

---

### 📂 **3. [FASE 3: Validasi Benchmark & Penyelesaian Riset](fase3_validasi_benchmark.md)**
* **SOP-07**: Validasi Benchmark Ground Truth LPW (*Labeled Pupils in the Wild*, 95 FPS, Side View Angle).
* **SOP-08**: Penyimpanan, Pengarsipan, & Tata Kelola Dataset.
* **SOP-09**: Dokumentasi Riset & Penyusunan Manuskrip Publikasi Jurnal.

---

📌 **Rujukan Master Notebook**: Seluruh alur komputasi SOP di atas dijalankan secara terpadu melalui **[`Colab_Pupil_Dataset_Processor.ipynb`](../../Colab_Pupil_Dataset_Processor.ipynb)**.
