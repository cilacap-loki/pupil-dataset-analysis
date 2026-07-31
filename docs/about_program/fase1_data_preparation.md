# **FASE 1: DATA PREPARATION & CLEANING**
## **Dokumentasi Standar Operasional Prosedur (SOP-01, SOP-02, SOP-03)**

---

### **1. RINGKASAN FASE 1**
Fase 1 berfokus pada tahap penyiapan data awal dari video mentah original hingga menjadi kepingan gambar *PNG Lossless* yang terisolasi pada jendela **Segmen Optimal 30 Detik** (1.500 Bingkai @ 50 FPS), serta pra-pemrosesan pemotongan area mata (*Region of Interest / ROI*) 800x800 piksel yang terstabilisasi.

---

### **2. DETAIL STANDAR OPERASIONAL PROSEDUR (SOP)**

#### **SOP-01: Inisialisasi Environment & Konfigurasi Workspace**
* **Tujuan**: Membangun lingkungan komputasi yang terisolasi di Google Colab dan memetakan struktur direktori output di Google Drive.
* **Logika Kerja**:
  1. Komputer melakukan mounting Google Drive (`/content/drive`).
  2. Memindai folder `Hibah Penelitian` untuk mendeteksi berkas video mentah (`.mp4`, `.avi`, `.mkv`).
  3. Membangun 4 subfolder output standar per responden:
     - `1_Raw_Frames_SOP01&02/`
     - `2_Grayscale_ROI_SOP03/`
     - `3_Mask_Pupil_SOP04/`
     - `4_Hasil_Analisis_SOP05_06/`

#### **SOP-02: Ekstraksi Direct Frame PNG Lossless (Segmen Optimal 30 Detik)**
* **Tujuan**: Mengisolasi 30 detik durasi video terbaik (kedipan paling minimal) dan mengesktraknya menjadi 1.500 gambar PNG murni tanpa kompresi visual.
* **Logika Kerja**:
  1. **Fast Blink Scan**: Komputer menggunakan *sliding window* 1.500 frame untuk memindai seluruh durasi video.
  2. **Kriteria Pemilihan**: Menghitung jumlah frame kedipan pada tiap jendela dan memilih jendela waktu dengan frekuensi kedipan terendah sebagai **Segmen Optimal 30 Detik**.
  3. **Direct Frame Extraction**: Memotong 1.500 frame pada jendela terpilih dan menyimpannya secara *lossless* ke `1_Raw_Frames_SOP01&02/`.

#### **SOP-03: Pra-Pemrosesan Grayscale & EMA Motion-Stabilized Crop ROI (800x800 px)**
* **Tujuan**: Pemotongan area mata (*Region of Interest / ROI*) resolusi $800 \times 800\text{ px}$ yang stabil tanpa distorsi *shaking/guncangan* kepala.
* **Logika Kerja**:
  1. **Grayscale & Heavy Blur**: Mengonversi bingkai ke skala kelabu (*grayscale*) dan menerapkan Median Blur $25 \times 25$ untuk mendeteksi posisi tergelap pupil (`minLoc`).
  2. **EMA Stabilization**: Menghaluskan pergerakan titik pusat $(X_c, Y_c)$ menggunakan penapis *Exponential Moving Average*:
     $$\hat{X}_c^{(i)} = \alpha \cdot X_{\text{raw}}^{(i)} + (1 - \alpha) \cdot \hat{X}_c^{(i-1)}, \quad \alpha = 0.15$$
  3. **Stabilized Crop**: Memotong sub-gambar $800 \times 800\text{ px}$ di sekeliling titik pusat terstabilisasi dan menyimpannya ke `2_Grayscale_ROI_SOP03/`.
