# 📋 SOP-03: Pra-Pemrosesan Grayscale & EMA-Stabilized Crop ROI 800x800

### 🎯 Tujuan
Mengonversi warna citra ke Grayscale dan melakukan pemotongan area mata *Region of Interest (ROI)* $800 \times 800\text{ px}$ yang terstabilisasi *Exponential Moving Average (EMA)*.

### 📌 Langkah Operasional
1. Konversi citra BGR ke Grayscale.
2. Deteksi piksel tergelap menggunakan Multi-stage Median Blur & `minMaxLoc`.
3. Terapkan pemulusan posisi pusat ROI dengan formula EMA ($lpha = 0.05$).
4. Potong dan simpan ROI $800 \times 800\text{ px}$ ke folder `2_Grayscale_ROI_SOP04`.

### 📤 Luaran (*Output*)
* Berkas citra ROI Grayscale terstabilisasi tanpa *jitter* kepala pada folder `2_Grayscale_ROI_SOP04`.
