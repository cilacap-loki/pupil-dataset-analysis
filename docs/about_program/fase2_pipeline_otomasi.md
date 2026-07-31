# **FASE 2: PIPELINE OTOMASI & SEGMENTASI**
## **Dokumentasi Standar Operasional Prosedur (SOP-04, SOP-05, SOP-06)**

---

### **1. RINGKASAN FASE 2**
Fase 2 merupakan inti dari platform komputasi **Pupil Dataset Processor (PDP)**. Fase ini melakukan segmentasi biner pupil adaptif berpresisi tinggi, menghasilkan dataset masker biner, merekayasa sinyal temporal osilasi *Pupillary Hippus*, serta merender video verifikasi terpadu dan laporan PDF diagnostik klinis.

---

### **2. DETAIL STANDAR OPERASIONAL PROSEDUR (SOP)**

#### **SOP-04: Segmentasi Masker Biner Pupil & Render Video Terpadu Realtime MP4**
* **Tujuan**: Menghasilkan 1.500 file PNG masker biner pupil murni (`1_Mask_Biner/`) dan 1 Berkas Video Terpadu MP4.
* **Logika Kerja**:
  1. **Core Engine (`detect_pupil_opencv_sop05`)**:
     - *Eyeball Closure Check*: Jika `min_val > 175`, mata teridentifikasi tertutup (`"BLINK"`), mengembalikan masker serba hitam ($0$) dan label teks merah.
     - *Adaptive Thresholding*: Memotong piksel pupil secara dinamis berbasis kegelapan lokal ($T = V_{\text{min}} + 25$).
     - *Glint Removal*: Terapkan Morphological Closing ($7 \times 7$) untuk menutup bintik pantulan LED putih.
  2. **Area-Equivalent Isotropic Geometry ($D = 2\sqrt{\text{Area}/\pi}$)**:
     - Mengukur diameter pupil simetris dari luas kontur $A$, menghasilkan lingkaran overlay hijau yang presisi dan kebal potongan bulu mata.
  3. **Penyimpanan Output**:
     - **Folder `3_Mask_Pupil_SOP04/1_Mask_Biner/`**: Simpan 1.500 PNG masker biner.
     - **Berkas `[Nama_Responden]_Video_Tracking_dan_Grafik_Realtime.mp4`**: Render 1 video terpadu 3-panel (Tracking + Masker Biner + Grafik Realtime).

#### **SOP-05: Tracking Pupil, Filter Outlier Moving Median, & Sinyal Temporal Hippus**
* **Tujuan**: Mengekstrak sinyal deret-waktu (*time-series*) diameter pupil, menyaring kedipan/outlier, dan menghitung biomarker osilasi.
* **Logika Kerja**:
  1. **Outlier & Blink Suppression**:
     - Frame kedipan diubah menjadi `NaN`.
     - Terapkan *Moving Median Baseline Filter* dengan ukuran jendela $W = 150\text{ frame}$.
     - Sinyal kedipan dipotong bersih dan didilasi 11 frame untuk menghapus loncatan *spike* liar.
  2. **Ekstraksi Biomarker Hippus**:
     - Menghitung **Frekuensi Osilasi (Hz)**: $f = \frac{|\text{Peaks}|}{\text{Durasi Total (s)}}$.
     - Menghitung **Persentase Fluktuasi ($\Delta D_{\%}$)**: $\Delta D_{\%} = \frac{D_{\text{maks}} - D_{\text{min}}}{\bar{D}} \times 100\%$.
  3. **Ekspor CSV Tabular**: Menyimpan berkas spreadsheet `[Nama_Responden]_laporan_analisis_sop06.csv` di folder `4_Hasil_Analisis_SOP05_06/`.

#### **SOP-06: Generator Laporan PDF Diagnostik Klinis Individual**
* **Tujuan**: Menghasilkan dokumen PDF laporan akademis resmi per responden menggunakan pemustakaan ReportLab (dilengkapi *Failsafe Anti-Crash*).
* **Logika Kerja**:
  1. Memuat parameter medis (Frekuensi Hz, Fluktuasi %, Rata-rata Diameter, Blink Rate %).
  2. Menyusun tabel kuantitatif dan menyematkan grafik sinyal temporal PNG.
  3. Menyimpan berkas `[Nama_Responden]_Laporan_Klinis_SOP06.pdf` ke folder `4_Hasil_Analisis_SOP05_06/`.
