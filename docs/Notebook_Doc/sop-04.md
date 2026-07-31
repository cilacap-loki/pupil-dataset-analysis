# 📋 SOP-04: Segmentasi Mask Pupil Otomatis & Video Verifikasi Realtime

### 🎯 Tujuan
Mengekstraksi area pupil mata menggunakan algoritma OpenCV teroptimasi, menyimpan masker biner PNG, dan merender 2 berkas video verifikasi realtime.

### 📌 Langkah Operasional
* **Langkah 1:** Definisi *Core Engine OpenCV* `detect_pupil_opencv_sop05(gray_frame, ...)` (Multi-stage blur, adaptive thresholding, contour circularity, ellipse fitting).
* **Langkah 2:** Eksekusi segmentasi masker biner PNG ke folder `3_Mask_Pupil_SOP05`.
* **Langkah 3:** Render 2 berkas video MP4 verifikasi (`Video2_Overlay_Tracking.mp4` & `Video3_Komparasi_SplitScreen.mp4`).

### 📤 Luaran (*Output*)
* Berkas masker biner PNG pupil dan 2 video MP4 verifikasi realtime.
