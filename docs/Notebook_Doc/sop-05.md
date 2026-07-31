# 📋 SOP-05: Tracking Pupil & Analisis Sinyal Temporal Fluktuasi Hippus

### 🎯 Tujuan
Mengekstraksi deret waktu (*time-series*) diameter pupil, membersihkan kedipan (*blink filtering*), menghitung fitur medis **Frekuensi Osilasi ($Hz$)** dan **Persentase Fluktuasi ($\Delta D_{\%}$)**, serta mengekspor data CSV dan Grafik PNG.

### 📌 Langkah Operasional
1. Ekstraksi koordinat pusat $(X, Y)$ dan diameter $D$ per frame.
2. Lakukan interpolasi linier untuk menyaring kedipan mata (*blink filtering*).
3. Hitung tren baseline rolling mean (30 frame = 1 detik).
4. Ekstraksi sinyal osilasi Pupillary Hippus, hitung puncak osilasi (*find_peaks*), frekuensi $Hz$, dan amplitudo fluktuasi.
5. Simpan data per-frame ke CSV dan render grafik `chart_hippus_sop06.png`.

### 📤 Luaran (*Output*)
* Berkas `laporan_analisis_sop06.csv` dan berkas grafik `chart_hippus_sop06.png`.
