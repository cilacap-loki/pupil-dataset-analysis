# 📋 SOP-07: Validasi Benchmark Ground Truth LPW (Labeled Pupils in the Wild)

### 🎯 Tujuan
Mengevaluasi presisi, akurasi, dan keandalan algoritma pelacak OpenCV SOP-04 terhadap koordinat acuan **Ground Truth (GT)** publik acuan internasional **LPW (Labeled Pupils in the Wild)**.

### 📌 Langkah Operasional
* **Langkah 1:** Form Pemilihan Target Dataset Ground Truth LPW & Subfolder (contoh: `001`, `002`, `ALL`).
* **Langkah 2:** Parsing & Verifikasi Berkas Koordinat Ground Truth LPW (`1.txt` 2-kolom $X, Y$).
* **Langkah 3:** Rendering Video MP4 Super-Komparasi Realtime (*Split-Screen GT vs Prediksi OpenCV + Trajectory Chart 2D*).
* **Langkah 4:** Penghitungan statistik kuantitatif Ground Truth Error (**Detection Rate %**, **Mean Center Error px**, **Median Center Error px**), ekspor CSV per-frame, dan terbit **PDF Laporan Evaluasi Ground Truth LPW**.

### 📤 Luaran (*Output*)
* Video MP4 Super-Komparasi Realtime, Berkas CSV Evaluasi GT, dan Dokumen PDF Laporan Evaluasi Resmi Ground Truth LPW.
