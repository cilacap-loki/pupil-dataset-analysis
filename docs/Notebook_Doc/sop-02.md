# 📋 SOP-02: Akuisisi Data Video Mentah & Ekstraksi Frame PNG Responden

### 🎯 Tujuan
Mengumpulkan data rekaman video pupil mata responden mentah (MP4/AVI) dan mengekstraksi menjadi citra PNG frame-by-frame *lossless* tanpa kompresi.

### 📌 Langkah Operasional
1. Memasukkan berkas video mentah ke folder `1_Raw_Frames_SOP01&02/<ID_Responden>/`.
2. Menjalankan ekstraktor OpenCV `cv2.VideoCapture`.
3. Menyimpan setiap frame citra sebagai `frame_XXXX.png`.

### 📤 Luaran (*Output*)
* Ribuan frame citra PNG resolusi tinggi siap diproses pada folder `1_Raw_Frames_SOP01&02`.
