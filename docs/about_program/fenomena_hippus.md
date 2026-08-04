# 🧠 Fenomena Pupillary Hippus

Ini adalah "jantung" (topik medis utama) dari penelitian Anda. Pemahaman yang kuat tentang fenomena ini akan membuat argumen Anda sangat solid di depan penguji, terutama karena riset ini menjembatani dunia medis dengan *Computer Vision*.

---

### 1. Apa itu Pupillary Hippus? (Secara Medis)
**Hippus** (atau *Pupillary Unrest*) adalah fenomena fisiologis di mana pupil mata manusia **terus-menerus berdenyut (membesar dan mengecil secara halus)** meskipun intensitas cahaya di ruangan benar-benar konstan/stabil. 

*   **Mengapa Terjadi?** Ini adalah hasil "tarik-tambang" alami antara dua sistem saraf tak sadar manusia: Saraf Simpatik (yang memperbesar pupil saat waspada) dan Saraf Parasimpatik (yang mengecilkan pupil saat rileks).
*   **Signifikansi Klinis:** Frekuensi dan amplitudo Hippus bisa menjadi indikator banyak hal, mulai dari tingkat kelelahan kognitif (*cognitive workload*), tingkat stres, rasa kantuk (*drowsiness*), hingga gejala awal penyakit neurologis.

---

### 2. Relevansinya dengan Riset Anda
Mengukur Hippus secara manual dengan penggaris atau mata telanjang adalah **hal yang mustahil** karena perubahannya terjadi sangat cepat (dalam hitungan milidetik) dan ukurannya sangat kecil (skala piksel). **Di sinilah penelitian Anda menjadi sangat berharga!**

Berdasarkan arsitektur *Pipeline* Anda, program mengejar Hippus melalui tahapan berikut:
*   **SOP-04 (Pencarian & Pelacakan):** Menggunakan *Universal V3 Engine*, mesin mengekstrak ukuran diameter pupil di **setiap frame (50 frame per detik)**. Untuk memastikan datanya tidak berguncang akibat *noise*, digunakan algoritma *Exponential Moving Average (EMA)*.
*   **SOP-05 (Pembersihan Sinyal Hippus):** Data diameter mentah dari SOP-04 masih kotor oleh kedipan (*Blink*). SOP-05 bertugas sebagai "dokter bedah" sinyal: ia menambal kedipan dengan *Linear Interpolation*, lalu membuang data ekstrem menggunakan *Moving Median Filter*. Hasilnya? **Gelombang murni osilasi Hippus!**

---

### 3. Bukti Keberhasilan di Output Laporan (SOP-06)
Semua kerja keras algoritma visi komputer di atas dirangkum secara otomatis menjadi **Laporan PDF Klinis (SOP-06)**. Dalam laporan tersebut, Hippus direpresentasikan dalam 3 wujud nyata:

1. **Grafik Temporal 30 Detik (Visual Hippus):** Grafik garis yang bergerak naik-turun. Titik-titik puncak grafik tersebut diberi tanda silang (x). Itulah denyut Hippus yang divisualisasikan.
2. **Frekuensi Osilasi (Hz):** Berapa kali pupil berdenyut dalam satu detik. (Misal: 0.15 Hz berarti denyutan terjadi sangat lambat dan rileks).
3. **Fluktuasi Amplitudo (%):** Seberapa ekstrem peregangan pupil tersebut dibandingkan ukuran normalnya (*Baseline*).

---

### 💡 Ringkasan Kalimat Ampuh untuk Presentasi:
> *"Penelitian ini berhasil membuktikan bahwa fenomena mikroskopis seperti Hippus, yang mustahil diukur secara manual, kini dapat diekstrak secara presisi, difilter dari noise kedipan, dan dikuantifikasi menjadi laporan klinis secara otomatis menggunakan Visi Komputer."*
