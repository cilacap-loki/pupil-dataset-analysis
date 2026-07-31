# 📑 Dokumentasi Standard Operating Procedure (SOP-01 s/d SOP-09)
### Pipeline Riset: Pupil Dataset Processor & Hippus Analysis Engine

Dokumentasi ini berisi panduan teknis operasional 9 SOP yang selaras 1-to-1 dengan proposal hibah riset **Pengembangan Dataset Video Pupil dan Analisis Awal Dinamika Diameter Pupil Menggunakan Visi Komputer**.

---

### 🗺️ Peta Alur SOP Riset:

| Nomor SOP | Nama SOP | Fase | Output Utama |
| :---: | :--- | :---: | :--- |
| **[SOP-01](sop-01.md)** | Inisialisasi Environment & Workspace | FASE 1 | Mount Drive & Setup Environment |
| **[SOP-02](sop-02.md)** | Akuisisi Data Video Mentah & Frame PNG | FASE 1 | Ekstraksi Frame PNG Responden Lossless |
| **[SOP-03](sop-03.md)** | Pra-Pemrosesan Grayscale & Eye Crop ROI | FASE 1 | Crop ROI 800x800 EMA-Stabilized |
| **[SOP-04](sop-04.md)** | Segmentasi Mask Pupil & Video Verifikasi | FASE 2 | Masker Biner PNG & 2 Video Verifikasi |
| **[SOP-05](sop-05.md)** | Tracking Pupil & Analisis Sinyal Hippus | FASE 2 | Fitur Medis ($Hz$, $\Delta D_{\%}$) & CSV/PNG Chart |
| **[SOP-06](sop-06.md)** | Generator Laporan PDF Diagnostik Klinis | FASE 2 | Sertifikat PDF Diagnostik Klinis Resmi |
| **[SOP-07](sop-07.md)** | **Validasi Benchmark Ground Truth LPW** | FASE 3 | **Video Super-Komparasi & PDF Evaluasi GT** |
| **[SOP-08](sop-08.md)** | Tata Kelola Storage Privat & Backup | FASE 3 | Struktur Folder Drive & Backup Privat |
| **[SOP-09](sop-09.md)** | Diseminasi & Manuskrip Scientific | FASE 3 | Manuskrip Jurnal & Laporan Akhir Hibah |
