# 📈 Panduan Membaca Grafik Laporan Klinis (SOP-06)

Dokumen ini adalah "contekan" (*cheat sheet*) untuk membantu Anda mempresentasikan dan mempertahankan hasil akhir (Laporan PDF Klinis) dari program analisis pupil Anda di depan dewan penguji. 

---

### 1. Membedah Visual Grafik (Garis & Titik)
Jika Anda ditanya, *"Apa maksud dari garis biru, garis merah putus-putus, dan titik oranye pada grafik ini?"*, berikut jawabannya:

*   **Garis Biru (Diameter Pupil px):**
    Ini adalah sinyal mentah pergerakan ukuran pupil dari *frame* ke *frame* (sebanyak 50 *frame* per detik) yang **sudah dibersihkan dari *noise* kedipan mata (Blinks)** menggunakan metode Interpolasi Linear dan penapisan data pencilan (*Outlier Filter*).
*   **Garis Merah Putus-putus (Trend Baseline):**
    Garis ini adalah **nilai tengah/rata-rata bergerak (*Moving Average/Median*)** dari garis biru. Pupil tidak pernah diam, tetapi ia memiliki ukuran dasar (*baseline*) di sekeliling area mana ia berdenyut. Garis merah melambangkan ukuran dasar tersebut.
*   **Titik Oranye (Puncak Hippus):**
    Setiap titik oranye merepresentasikan satu denyutan maksimum (*local maxima*). Algoritma (*SciPy find_peaks*) menempatkan titik ini setiap kali pupil mencapai regangan terbesar sebelum akhirnya mengecil kembali.

---

### 2. Membedah Rumus Parameter Medis
Di atas grafik, terdapat dua angka penting: **Frekuensi (Hz)** dan **Fluktuasi (%)**. Berikut adalah asal-usul (rumus matematis) dari angka-angka tersebut yang digunakan di dalam *V3 Engine* Anda:

#### A. Frekuensi Hippus (Hz)
Frekuensi mengukur "Seberapa cepat denyutan pupil terjadi dalam satu detik".
*   **Formula / Rumus:** 
    `Frekuensi (Hz) = Total Jumlah Puncak (Titik Oranye) / Total Durasi Video (Detik)`
*   **Logika Program:** Algoritma menghitung ada berapa titik oranye di sepanjang grafik, lalu membaginya dengan panjang waktu (misalnya 1500 *frame* pada 50 FPS = 30 detik).
*   **Contoh:** Jika ada 22 puncak oranye dalam 30 detik, maka Frekuensi = `22 / 30 = 0.73 Hz`.

#### B. Fluktuasi Amplitudo (%)
Fluktuasi mengukur "Seberapa ekstrem regangan elastisitas pupil saat ia membesar dan mengecil secara tak sadar".
*   **Formula / Rumus:**
    `Fluktuasi (%) = ((Diameter Maksimum - Diameter Minimum) / Rata-rata Baseline) * 100%`
*   **Logika Program:** Program mencari titik tertinggi (*max*) dan titik terendah (*min*) dari garis biru, menghitung selisih jarak regangannya, lalu mengonversinya menjadi persentase (%) terhadap rata-rata ukuran pupil responden tersebut.
*   **Contoh Makna Klinis:** Fluktuasi 36% artinya ukuran pupil penderita bisa merenggang membesar/mengecil hingga 36% dari ukuran aslinya secara tak sadar (sangat dinamis).

---

### 💡 Kalimat Pertahanan (*Defense*) Saat Presentasi:
Jika penguji menanyakan validitas perhitungan algoritma Anda, gunakan argumen ini:
> *"Pencarian denyut pupil (puncak oranye) tidak dilakukan secara sembarangan. Algoritma kami menggunakan fungsi matematis pencarian puncak dengan ambang batas jarak (distance) minimal 15 frame dan prominensi khusus, sehingga riak-riak kecil yang diakibatkan oleh noise atau bayangan kamera tidak akan dihitung secara keliru sebagai denyut Hippus medis."*
