# **FASE 1: DATA PREPARATION & CLEANING**
## **Dokumentasi Standar Operasional Prosedur (SOP-01, SOP-02, SOP-03)**

---

### **1. RINGKASAN FASE 1**
Fase 1 berfokus pada tahap penyiapan data awal dari video mentah original hingga menjadi kepingan gambar *PNG Lossless* yang terisolasi pada jendela **Segmen Optimal 30 Detik** (1.500 Bingkai @ 50 FPS), serta pra-pemrosesan pemotongan area mata (*Region of Interest / ROI*) 800x800 piksel yang terstabilisasi tanpa distorsi pergerakan kepala.

---

### **2. DETAIL STANDAR OPERASIONAL PROSEDUR (SOP)**

#### **SOP-01: Inisialisasi Environment & Konfigurasi Workspace**
* **Tujuan**: Membangun lingkungan komputasi yang terisolasi di Google Colab dan memetakan struktur direktori output di Google Drive.
* **Logika Kerja**:
  1. Komputer melakukan mounting Google Drive (`/content/drive`).
  2. Memindai folder `Hibah Penelitian` untuk mendeteksi berkas video mentah (`.mp4`, `.avi`, `.mkv`) dan menyediakan antarmuka *Dropdown Interactive* untuk memilih responden.
  3. Membangun 4 subfolder output standar per responden secara otomatis:
     - `1_Raw_Frames_SOP01&02/` : Folder penyimpanan bingkai PNG mentah.
     - `2_Grayscale_ROI_SOP03/` : Folder hasil potong ROI 800x800 px terstabilisasi.
     - `3_Mask_Pupil_SOP04/` : Folder hasil segmentasi biner pupil & overlay.
     - `4_Hasil_Analisis_SOP05_06/` : Folder laporan tabular CSV & visualisasi grafik.

#### **SOP-02: Ekstraksi Direct Frame PNG Lossless (Segmen Optimal 30 Detik)**
* **Tujuan**: Mengisolasi 30 detik durasi video terbaik (kedipan paling minimal) dan mengekstraknya menjadi 1.500 gambar PNG murni tanpa kompresi visual.
* **Logika Kerja**:
  1. **Fast Blink Heuristic Scan (`check_blink_fast`)**:
     - Komputer memindai bingkai setiap kelipatan 5 frame (`frame_idx % 5 == 0`).
     - Menggunakan pemprosesan cepat ambang batas adaptif ($T_{\text{thresh}} = \min(V_{\text{min}} + 28, 130)$) di area ROI tergelap. Jika diameter kontur pupil $< 5\text{ px}$, bingkai tersebut ditandai sebagai **frame kedipan**.
  2. **Sliding Window Selection**:
     - Memindai seluruh durasi video menggunakan *sliding window* berukuran 1.500 frame (30 Detik @ 50 FPS) dengan pergeseran *step* 50 frame.
     - Memilih jendela waktu dengan jumlah akumulasi kedipan terendah sebagai **Segmen Optimal 30 Detik**.
  3. **Direct Frame Extraction**:
     - Memotong 1.500 frame tepat pada jendela terpilih dan menyimpannya secara *lossless* (`.png`) langsung ke folder `1_Raw_Frames_SOP01&02/`.

#### **SOP-03: Pra-Pemrosesan Grayscale & EMA Motion-Stabilized Crop ROI (800x800 px)**
* **Tujuan**: Pemotongan area mata (*Region of Interest / ROI*) resolusi $800 \times 800\text{ px}$ yang terstabilisasi secara halus tanpa distorsi guncangan (*shaking*) pergerakan kepala.
* **Logika Kerja**:
  1. **15% Border Margin Gating**: Mengabaikan 15% area tepi terluar bingkai ($M_x = 0.15 \times W$, $M_y = 0.15 \times H$) untuk mencegah gangguan pakaian/hijab atau bayangan luar yang dapat mengacaukan pencarian titik pupil.
  2. **Grayscale & Median Blur MinLoc**: Mengonversi bingkai ke skala kelabu (*grayscale*) dan menerapkan *Median Blur* filter $25 \times 25$ untuk mendeteksi koordinat piksel tergelap pupil $(X_{\text{target}}, Y_{\text{target}})$ via `minMaxLoc`.
  3. **EMA Motion Stabilization**: Menghaluskan lintasan pergerakan titik pusat crop $(\hat{X}_c, \hat{Y}_c)$ menggunakan penapis *Exponential Moving Average* (EMA):
     $$\hat{X}_c^{(i)} = \alpha \cdot X_{\text{target}}^{(i)} + (1 - \alpha) \cdot \hat{X}_c^{(i-1)}, \quad \alpha = 0.08$$
     *(Penggunaan nilai $\alpha = 0.08$ memberikan efek peredaman guncangan yang sangat halus/smooth).*
  4. **Stabilized Boundary Crop & Padding**: Memotong sub-gambar $800 \times 800\text{ px}$ mengelilingi koordinat terstabilisasi. Jika batas pemotongan melebihi batas bingkai asli, sistem otomatis menerapkan padding batas `BORDER_REPLICATE`. Hasil potong disimpan ke folder `2_Grayscale_ROI_SOP03/`.
