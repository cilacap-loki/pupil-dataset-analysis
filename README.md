<p align="center">
  <img src="assets/img/title.png" width="100%" alt="Pupil Dataset Analysis Header">
</p>

<p align="center">
  <a href="https://colab.research.google.com/drive/1L1kNg5T-YRJfGFKLBbLjp5Z9J1r9pVnx" target="_blank"><img src="https://img.shields.io/badge/Google%20Colab-Master%20Notebook-orange?style=for-the-badge&logo=googlecolab" alt="Google Colab"></a>&nbsp;<a href="#"><img src="https://img.shields.io/badge/Hibah%20Penelitian-Aktif%202026-blue?style=for-the-badge&logo=academic" alt="Hibah Penelitian"></a>&nbsp;<a href="#"><img src="https://img.shields.io/badge/Python-3.10%2B-green?style=for-the-badge&logo=python" alt="Python Version"></a>&nbsp;<a href="#"><img src="https://img.shields.io/badge/OpenCV-Visi%20Komputer-red?style=for-the-badge&logo=opencv" alt="OpenCV"></a>&nbsp;<a href="#"><img src="https://img.shields.io/badge/Benchmark-LPW%20%26%20OpenEDS-purple?style=for-the-badge" alt="Benchmark Validation"></a>
</p>

---

# **pupil-dataset-analysis**
## **Pengembangan Dataset Video Pupil dan Analisis Awal Dinamika Diameter Pupil Menggunakan Visi Komputer**

Repositori resmi ini memuat alur kerja otomasisasi komputasi, master notebook, dan dokumentasi **Hibah Penelitian** berfokus pada pengembangan dataset video pupil berakurasi tinggi serta analisis awal dinamika diameter pupil berbasis Visi Komputer (*Computer Vision*).

---

## **Diagram Pipeline Riset & Dokumentasi SOP**

<details>
<summary><b>Klik di sini untuk melihat Diagram Pipeline Riset (SOP-01 s/d SOP-09)</b></summary>
<br>
<p align="center">
  <img src="assets/img/pipeline_riset.webp" width="100%" alt="Diagram Pipeline Riset SOP">
</p>
</details>

### **Menu Dokumentasi Utama Riset:**
* **[FASE 1: Data Preparation & Cleaning (SOP-01 s/d SOP-03)](docs/about_program/fase1_data_preparation.md)**
* **[FASE 2: Pipeline Otomasi & Segmentasi (SOP-04 s/d SOP-06)](docs/about_program/fase2_pipeline_otomasi.md)**
* **[FASE 3: Validasi Benchmark & Penyelesaian (SOP-07 s/d SOP-09)](docs/about_program/fase3_validasi_benchmark.md)**

---

## **Cakupan, Luaran, & Batasan Riset Hibah**

### **1. Cakupan Riset (Research Scope)**
Riset ini mencakup perancangan alur komputasi terstandarisasi (9 SOP dalam 3 Fase) untuk mengolah video mentah rekaman mata menjadi dataset digital terstruktur:
* **Ekstraksi Frame Lossless**: Mengonversi video rekaman mentah menjadi 1.500 bingkai gambar berpresisi tinggi tanpa penurunan kualitas (30 Detik @ 50 FPS).
* **Stabilisasi Potongan Mata (ROI)**: Pemotongan otomatis area mata ukuran $800 \times 800\text{ px}$ yang stabil dan meredam guncangan pergerakan mata.
* **Segmentasi Pupil Adaptif**: Pemisahan warna pupil otomatis (masker biner hitam-putih) yang adaptif terhadap perubahan pencahayaan dan pembersihan pantulan cahaya LED.
* **Ekstraksi Ukuran & Gerak Pupil**: Pengukuran diameter pupil, koordinat posisi titik pusat pupil, serta penapisan otomatis saat mata terpejam (kedipan).

### **2. Luaran Utama Riset (Grant Deliverables)**
* **Master Notebook Colab**: [`Colab_Pupil_Dataset_Processor.ipynb`](https://colab.research.google.com/drive/1L1kNg5T-YRJfGFKLBbLjp5Z9J1r9pVnx) (Pipeline SOP-01 s/d SOP-06).
* **Dataset Terstruktur**: 
  - 1.500 Bingkai PNG *Lossless* (Segmen Optimal 30 Detik).
  - 1.500 Bingkai PNG ROI $800 \times 800\text{ px}$.
  - 1.500 Bingkai PNG Masker Biner Pupil (`1_Mask_Biner/`).
  - Berkas Tabular CSV Deret-Waktu (`[Nama_Responden]_laporan_analisis_sop06.csv`).
* **Media Verifikasi Visual**: Berkas Video Terpadu MP4 3-panel (Tracking + Masker Biner + Grafik Temporal Realtime).

### **3. Batasan Riset (Research Limitations)**
* **Tahap Eksplorasi Awal**: Riset ini difokuskan pada pembangunan dataset dan analisis awal dinamika pupil.
* **Tanpa Kesimpulan Klinis Akhir**: Penelitian ini **tidak mengambil kesimpulan diagnosa medis/klinis akhir**, melainkan menyediakan fondasi dataset dan pipeline yang teruji untuk riset klinis lanjutan.

---

## **Spesifikasi Hardware & Perangkat Akuisisi Dataset**

Akuisisi dataset video pupil resolusi tinggi dilakukan selama **6 Hari Sesi Perekaman (08 Juni 2026 – 14 Juni 2026)** menggunakan kombinasi perangkat optik & sinematografi profesional:

| Perangkat Hardware / Peralatan | Visual Perangkat | Spesifikasi Teknis Optik & Sinematografi | Peran dalam Akuisisi Dataset |
| :--- | :---: | :--- | :--- |
| **Camera Sony A7 IV Mirrorless** | <img src="assets/tools/Camera%20Sony%20A7%20IV%20Mirrorless.jpg" width="120" alt="Sony A7 IV"> | Full Frame 33MP, FF 4K30p / 1.5x Crop 4K60p 10-bit 4:2:2 | Perekaman video mentah resolusi tinggi dengan detail piksel mikro |
| **Sony FE 100mm F/2.8 Macro GM OSS** | <img src="assets/tools/Sony%20FE%20100mm%20F2.8%20Macro%20GM%20OSS.jpg" width="120" alt="Sony FE 100mm Macro"> | Lensa Macro 1.4x (E-mount) khusus pemotretan *close-up* | Isolasi penampang iris dan pupil tanpa distorsi optik tepi |
| **Yongnuo YN-300 IV LED Video Light** | <img src="assets/tools/Yongnuo%20YN-300%20IV%20LED%20Video%20Light.jpg" width="120" alt="Yongnuo YN-300 IV"> | Portable RGB LED Light (3200K-5600K) | Penjagaan suhu kecerahan konstan untuk mengurangi variansi bayangan |
| **Light Stand Takara Spirit-3** | <img src="assets/tools/Light%20Stand%20Takara%20Spirit-3.jpg" width="120" alt="Takara Spirit-3"> | Stand Penyangga Lampu Statis | Penyangga sumber cahaya bebas guncangan saat perekaman berlangsung |

### **Spesifikasi Video Mentah (Raw Video Dataset)**
Format video mentah (*raw*) yang dihasilkan dari proses perekaman dan digunakan sebagai *input* utama dalam *pipeline* komputasi ini memiliki spesifikasi teknis sebagai berikut:
* **Resolusi Video**: $1920 \times 1080\text{ piksel}$ (Full HD 1080p).
* **Frame Rate**: $50\text{ FPS}$ (Sangat krusial untuk menangkap dinamika pergerakan mata tingkat milidetik dan osilasi pupil).
* **Codec Video**: H.264 / AVC (MPEG-4 Part 10).
* **Video Bitrate**: $\approx 48\text{ Mbps}$ (Kualitas rekam tingkat tinggi untuk mempertahankan keutuhan tekstur iris dan ketajaman batas pupil).
* **Durasi Perekaman**: $\approx 40-60\text{ Detik}$ per sesi responden (Nantinya dipotong otomatis menjadi 30 detik murni pada SOP-02).

---

## **Petunjuk Penggunaan Master Notebook (Google Colab)**

Seluruh proses ekstraksi dataset dan analisis dinamika pupil dapat dijalankan secara terpadu melalui **Google Colab**:

1. Buka Master Notebook: **[`Colab_Pupil_Dataset_Processor.ipynb`](https://colab.research.google.com/drive/1L1kNg5T-YRJfGFKLBbLjp5Z9J1r9pVnx)**.
2. Hubungkan sesi dengan **Google Drive**.
3. Jalankan sel komputasi dari **SOP-01** hingga sel analisis akhir secara berurutan.

---

## **Struktur Luaran Dataset di Google Drive**

Setiap responden yang diproses akan menghasilkan struktur folder luaran berikut:

```text
Outputs/
 └── [Nama_Responden]/
      ├── 1_Raw_Frames_SOP01&02/       # 1.500 Bingkai PNG Lossless (Segmen Optimal 30 Detik)
      ├── 2_Grayscale_ROI_SOP03/       # Potongan Area Mata ROI 800x800 px Stabilized
      ├── 3_Mask_Pupil_SOP04/          # Folder 1_Mask_Biner PNG & Video Terpadu Realtime MP4
      └── 4_Hasil_Analisis_SOP05_06/   # Berkas Spreadsheet CSV & Laporan PDF Ringkas
```

---

## **Informasi Hibah Penelitian**

* **Judul Hibah**: *Pengembangan Dataset Video Pupil dan Analisis Awal Dinamika Diameter Pupil Menggunakan Visi Komputer*
* **Tahun Pelaksanaan**: 2026
* **Lisensi Repositori**: Akademis / Hibah Penelitian (Restricted Use)
