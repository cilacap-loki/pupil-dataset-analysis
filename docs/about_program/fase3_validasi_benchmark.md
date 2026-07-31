# **FASE 3: VALIDASI BENCHMARK & PENYELESAIAN RISET**
## **Dokumentasi Standar Operasional Prosedur (SOP-07, SOP-08, SOP-09)**

---

### **1. RINGKASAN FASE 3**
Fase 3 berfokus pada tahap validasi kuantitatif mutlak (*cross-validation*) untuk mengukur seberapa akurat algoritma OpenCV kita jika disandingkan dengan label *Ground Truth* publik berstandar internasional (*Labeled Pupils in the Wild* / LPW & OpenEDS Meta), serta pengarsipan data dan finalisasi publikasi riset.

---

### **2. DETAIL STANDAR OPERASIONAL PROSEDUR (SOP)**

#### **SOP-07: Validasi Benchmark Ground Truth LPW & OpenEDS**
* **Tujuan**: Mengukur akurasi pelacakan algoritma pada video *benchmark* berkecepatan tinggi (95 FPS) dan sudut pandang samping (*off-axis side view*).
* **Logika Kerja**:
  1. **Parsing Ground Truth**: Membaca berkas kunci jawaban koordinat manual (`1.txt` / `9.txt`).
  2. **Perspective Ellipse Fitting**: Menggunakan `cv2.fitEllipse` untuk melacak bentuk pupil terdistorsi perspektif pada tampilan samping.
  3. **Evaluasi Metrik**: Menghitung *Detection Rate (%)* dan *Center Distance Error (px)*.

#### **SOP-08: Penyimpanan & Tata Kelola Dataset (Data Archiving)**
* **Tujuan**: Mengarsipkan seluruh luaran riset (1.500 PNG Lossless, ROI 800x800, Masker Biner, CSV, PDF) ke dalam basis data riset privat (*Google Drive / Harddisk*) yang aman.
* **Logika Kerja**:
  1. Memverifikasi kelengkapan 4 subfolder output per responden.
  2. Menerapkan aturan pengabaian berkas media besar di repositori Git (`.gitignore`).

#### **SOP-09: Dokumentasi Riset & Publikasi Jurnal (Final Reporting)**
* **Tujuan**: Mengompilasi luaran SOP 1 hingga 8 sebagai basis data empiris untuk penyusunan Laporan Akhir Hibah Penelitian dan Manuskrip Jurnal Ilmiah.
* **Logika Kerja**:
  1. Menyusun Technical Paper ([`Technical_Paper_Pupil_Processor.md`](../Technical_Paper_Pupil_Processor.md)).
  2. Menyiapkan draf naskah publikasi jurnal bereputasi (Sinta / Scopus).
