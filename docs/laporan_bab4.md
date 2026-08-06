### **4.5 Tahapan Eksperimen**

**4.5.1 Pendahuluan Tahapan Eksperimen**

*   **a. Tujuan tahapan eksperimen:** Tahapan eksperimen ini bertujuan untuk merancang, mengimplementasikan, dan menguji algoritma visi komputer (*Pupil Dataset Processor*) yang mampu mengekstraksi parameter dinamika fenomena *Pupillary Hippus* (Frekuensi dan Fluktuasi Amplitudo) secara otomatis dari rekaman video.
*   **b. Gambaran umum pipeline penelitian:** Penelitian ini dibagi menjadi tiga fase komputasi utama. Fase 1 berfokus pada persiapan data (*Data Preparation*) dan stabilisasi frame. Fase 2 merupakan *Pipeline* Otomasi utama yang menjalankan segmentasi, pelacakan koordinat, dan ekstraksi parameter dinamika pupil. Fase 3 adalah tahap validasi model (SOP-07) dengan mengkomparasikan hasil prediksi program terhadap *Ground Truth*.
*   **c. Keterkaitan antar tahapan:** Setiap tahapan bersifat linear dan saling bergantung. Hasil pemotongan koordinat mata (*ROI Crop*) dari tahap prapemrosesan menjadi masukan mutlak bagi modul segmentasi biner. Hasil dari segmentasi tersebut kemudian digunakan oleh modul pelacakan (*tracking*) untuk membentuk data deret waktu (*time series*), yang pada akhirnya diolah menjadi Laporan Analisis (PDF).

---

**4.5.2 Input Video**

1.  **Tujuan:** Memasukkan dataset video mata mentah ke dalam lingkungan komputasi (*workspace*) agar dapat diakses oleh algoritma pra-pemrosesan.
2.  **Dasar teori singkat:** Video digital adalah sekumpulan frame (*frames*) yang diputar secara sekuensial pada kecepatan tertentu (*Frame Rate*). Semakin tinggi *frame rate*, semakin detail pergerakan mikroskopis mata (Hippus) yang dapat direkam.
3.  **Spesifikasi data/video:** Penelitian ini menggunakan **Dataset Primer berisikan 70 responden**. Video direkam secara stabil menggunakan tripod dengan posisi responden duduk nyaman dan menatap lurus ke arah kamera (*steady*).
4.  **Implementasi:** Proses ini diimplementasikan dalam **SOP-01 (Inisialisasi Environment)**. Sistem melakukan pemasangan (*mounting*) pada Google Drive dan menginisialisasi jalur direktori untuk membaca folder dataset dari 70 responden tersebut.
5.  **Hasil implementasi:** Direktori kerja terhubung secara sukses dengan sumber dataset primer, ditandai dengan ditemukannya berkas video rekaman dari masing-masing target responden.

---

**4.5.3 Pre-processing**

1.  **Tujuan:** Menyeragamkan format frame, menghilangkan warna (mengubah ke keabuan), dan melakukan ekstraksi seluruh *frame* tanpa kompresi (*lossless*).
2.  **Dasar teori:** *Grayscale conversion* mengubah frame berwarna (RGB) menjadi satu saluran intensitas cahaya (0-255) yang lebih ringan diproses. Ekstraksi *lossless* memastikan tidak ada piksel yang terdegradasi kualitasnya akibat proses kompresi video.
3.  **Algoritma:** Algoritma membaca video dari awal hingga durasi 30 detik, mengekstraksi 1500 *frame* (asumsi minimum 50 FPS), dan membuang informasi warna kromatik.
4.  **Implementasi:** Berjalan pada tahap **SOP-02 (Ekstraksi Lossless Frames)** dan paruh awal **SOP-03 (Pra-Pemrosesan Grayscale)** menggunakan pustaka *OpenCV* di lingkungan Python.
5.  **Hasil:** Kumpulan 1500 berkas gambar berekstensi `.png` berwarna keabuan dengan kualitas piksel yang presisi, siap untuk diisolasi.

---

**4.5.4 Eye Detection**

1.  **Tujuan:** Memotong frame penuh menjadi *Region of Interest* (ROI) yang hanya memuat area mata target, sekaligus menstabilkan pergerakan kepala responden.
2.  **Dasar teori:** Meskipun pengambilan video telah dilakukan secara stabil menggunakan tripod, pergerakan alami dari kepala responden (seperti tarikan napas atau pergeseran postur) tetap menyebabkan posisi bola mata sedikit berpindah-pindah antar *frame*. Pemotongan ROI harus bersifat dinamis namun tetap stabil (*Motion-Stabilized Crop*) agar pupil senantiasa terkunci di tengah *frame*.
3.  **Algoritma:** Sistem menggunakan fungsi matematika penyeimbang *Exponential Moving Average* (EMA) untuk meredam pergeseran titik koordinat mata yang diakibatkan oleh pergerakan minor kepala tersebut, tanpa sedikitpun menghilangkan getaran asli denyut pupil.
4.  **Parameter:** Parameter penstabil gerakan diatur untuk menoleransi pergeseran pelan (kepala), dan ukuran *frame* hasil pemotongan dikunci secara mutlak pada resolusi **800x800 piksel**.
5.  **Hasil deteksi:** Rangkaian frame *grayscale* berukuran 800x800 piksel yang terpusat secara konsisten dan stabil pada bola mata. Ini mengakhiri fase eksekusi **SOP-03**.

---

**4.5.5 Pupil Segmentation**

1.  **Tujuan:** Memisahkan secara tegas antara objek target hitam pekat (Pupil, direpresentasikan dengan nilai biner 1) dan latar belakang yang tidak relevan seperti iris, sklera, atau kulit mata (direpresentasikan dengan biner 0).
2.  **Dasar teori:** Segmentasi objek spesifik sangat bergantung pada pencarian nilai ambang batas (*threshold*). Algoritma morfologi sekunder juga diperlukan untuk menambal "lubang" kosong yang diakibatkan oleh pantulan cahaya putih kamera (*Glint*).
3.  **Algoritma:** Algoritma **V3 Engine (SOP-04)** menggunakan metode *Adaptive Thresholding*. Ia memindai area piksel tergelap dalam frame ($V_{\text{min}}$) dan menambahkan konstanta offset untuk membentuk batas pembelah biner.
4.  **Parameter:** Nilai ambang batas (*threshold*) didapatkan secara otomatis dengan mencari piksel tergelap di dalam mata, lalu ditambah dengan nilai toleransi kecerahan sebesar 25 tingkat warna.
5.  **Hasil segmentasi:** Rangkaian *Mask Biner* (frame hitam-putih mutlak). Area bola pupil tampak putih polos tanpa ada gangguan *glint*, berlatar belakang hitam pekat (*Binary Mask*).

---

**4.5.6 Pupil Tracking**

1.  **Tujuan:** Melacak perpindahan titik pusat (koordinat sentroid X dan Y) area pupil di setiap rentetan *frame* secara berkesinambungan.
2.  **Dasar teori:** Pergerakan pupil dalam format *time-series* sangat rentan terhadap *noise* ekstrem (misalnya saat kelopak mata menutup atau berkedip). Nilai koordinat saat berkedip tidak boleh dianggap sebagai data riil denyutan.
3.  **Algoritma:** Program menghitung letak sentroid (titik keseimbangan) dari kumpulan piksel putih di frame mask biner. Untuk membuang data kedipan (*outliers*), program mengaplikasikan filter perata pergerakan, yakni *Moving Median*, pada aliran koordinat yang berjalan.
4.  **Parameter:** Sistem menggunakan filter penstabil pergerakan yang menyaring dan meratakan data selama durasi tertentu (150 frame) untuk memastikan bahwa anomali seperti kedipan mata akan diabaikan oleh program.
5.  **Hasil tracking:** Perekaman rekam jejak koordinat Cartesian yang halus, mulus, dan bebas dari lonjakan ekstrem akibat gangguan kedipan mekanis.

---

**4.5.7 Estimasi Diameter Pupil**

1.  **Tujuan:** Mengonversi jumlah besaran total piksel di area putih pupil (Luas / Area 2D) menjadi satu nilai kuantitatif panjang garis tengah yang dapat ditarik vertikal maupun horizontal (Diameter 1D).
2.  **Dasar teori:** Dengan meletakkan asumsi dasar bahwa bola pupil manusia mendekati bentuk lingkaran sempurna yang simetris, maka total luas piksel lingkarannya dapat ditarik mundur (*square root*) untuk menemukan nilai garis diameternya.
3.  **Algoritma:** Menggunakan rumus perhitungan *Geometri Simetris Area-Equivalent*.
4.  **Parameter:** Dengan menghitung total jumlah piksel putih yang membentuk area pupil pada mask biner, program mengonversinya menjadi perkiraan ukuran garis tengah (diameter) pupil menggunakan logika geometri lingkaran dasar.
5.  **Hasil estimasi:** Satu nilai desimal metrik (*float*) bersatuan piksel (px) yang dihasilkan di setiap *frame* (misalnya: Frame ke-10 = 129.5 px, Frame ke-11 = 130.0 px).

---

**4.5.8 Pembentukan Time Series**

1.  **Tujuan:** Memvisualisasikan pergerakan atau fluktuasi perubahan diameter pupil sepanjang 30 detik durasi rekaman ke dalam wujud diagram garis dua dimensi.
2.  **Dasar teori:** Deret data temporal akan sangat jauh lebih mudah dianalisis secara mendalam oleh peneliti apabila dipetakan pada sumbu kartesius dengan Waktu sebagai sumbu kontrol independen (Sumbu X) dan nilai pengukuran sebagai sumbu dependen (Sumbu Y).
3.  **Implementasi:** Modul pustaka `Matplotlib` mem-plot seluruh *array* hasil diameter pupil secara sekuensial. Garis biru solid menggambarkan kurva pergerakan ukuran *real-time* mata. Garis merah putus-putus (*Trend Baseline*) ditambahkan sebagai representasi matematis dari rata-rata diam (*Moving Average*) dari pupil.
4.  **Hasil Visual:** Menghasilkan kanvas grafik garis dengan Sumbu Y berupa ukuran Diameter (px) dan Sumbu X berupa Titik Waktu/Frame (*Frame Number*).

---

**4.5.9 Analisis Temporal Hippus**

1.  **Tujuan:** Mengekstraksi pola gelombang tak beraturan (*Pupillary Hippus*) dari grafik *time-series* menjadi angka ukur kuantitatif mutlak yang pasti, yakni **Frekuensi (Hz)** dan **Fluktuasi Amplitudo (%)**.
2.  **Dasar teori:** Fenomena Hippus dicirikan oleh hadirnya gelombang fluktuasi involunter dan regangan elastisitas pupil. Ekstraksi parameternya dapat membuka peluang riset lanjutan di berbagai disiplin ilmu.
3.  **Algoritma ekstraksi:**
    *   Sistem mencari seluruh puncak tertinggi lokal sementara (*Local Maxima*) di sepanjang kontur gelombang grafik garis biru.
    *   **Frekuensi:** Dihitung dengan membagi total kemunculan titik puncak dengan durasi rekaman keseluruhan.
        *(Rumus: Frekuensi (Hz) = Total Jumlah Puncak / Total Durasi Video)*
    *   **Fluktuasi:** Dihitung dengan mencari selisih antara bukaan mata terbesar dan terkecil, lalu menormalisasinya terhadap ukuran mata saat rileks.
        *(Rumus: Fluktuasi (%) = ((Diameter Maksimum - Diameter Minimum) / Rata-rata Baseline) x 100%)*
4.  **Parameter:** Untuk memastikan bahwa getaran yang dihitung adalah denyut pupil asli dan bukan gangguan (*noise*) kamera, sistem mewajibkan adanya jarak jeda minimal antar-denyutan sebesar **15 frame** (0.3 detik) dan wujud regangan yang cukup terlihat (minimal **0.5 piksel**). Proses pencetakan tertuang pada eksekusi **SOP-05 & SOP-06**.
5.  **Hasil analisis:** Teks luaran kuantitatif dalam berkas **Laporan Analisis PDF (SOP-06)** yang merumuskan dua indikator utama tersebut secara tegas untuk keperluan analisis lebih lanjut.

---

**4.5.10 Evaluasi Model**

1.  **Tujuan:** Mengukur dan memverifikasi seberapa akurat algoritma *V3 Engine (Machine Prediction)* dalam mendeteksi dan melacak letak koordinat sentroid pupil jika dibandingkan dan diadu dengan hasil anotasi kebenaran mutlak referensi ahli (*Ground Truth*).
2.  **Metrik evaluasi:** Menggunakan algoritma pengukur jarak standar internasional, **Mean Euclidean Error**. Algoritma ini menarik garis lurus terpendek antara titik potong (X, Y) tebakan program komputasi dengan titik (X, Y) referensi ahli pada potongan *frame* yang sama.
3.  **Implementasi:** Sepenuhnya diwujudkan secara tertutup dan otonom pada **SOP-07 (Validasi Benchmark LPW)**. Algoritma komparasi (*Benchmark Engine*) menyejajarkan secara sinkron matriks log `pred.txt` luaran program dengan matriks `[ID].txt` milik anotasi ahli dari dataset LPW.
4.  **Hasil pengujian:**
    *   Sistem mengeluarkan angka kuantitatif ilmiah berupa metrik akhir komparasi *Mean Euclidean Error*.
    *   Secara bersamaan, mesin *ffmpeg* mencetak luaran visual definitif berupa **Video 4-Panel** (Panel gabungan yang menjejalkan: Video Asli, Visualisasi Bounding Box Prediksi Mesin, Kotak Acuan Ground Truth Ahli, dan *Crosshair* Komparasi Sumbu X-Y).
5.  **Kesimpulan:** Memberikan legitimasi ilmiah mutlak atas hipotesis penelitian bahwa algoritma *Pupil Dataset Processor* PDP, tidak hanya sanggup memproses data secara mandiri untuk kepentingan ekstraksi fitur (Fase 1-2), tetapi juga teruji valid dan sanggup berkompetisi saat diadu akurasinya dengan basis anotasi standar penelitian di dunia (Fase 3).
