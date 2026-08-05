# 🏥 Matriks Kasar Diagnosis Medis Berdasarkan Parameter Pupil

Dokumen ini berisi rangkuman hipotesis klinis (*Medical Assumptions*) yang bisa ditarik dari dua parameter utama program (*Frekuensi Hippus* dan *Fluktuasi Amplitudo*). Kesimpulan ini didasarkan pada literatur medis, terutama metrik yang disebut **Pupillary Unrest Index (PUI)**.

> **Peringatan untuk Presentasi:** Riset utama hibah ini murni berfokus pada ranah Ilmu Komputer (Metodologi Pengolahan Citra). Matriks medis ini disediakan secara eksklusif sebagai wawasan tambahan (*Future Work / Trivia*) untuk menjawab pertanyaan penguji mengenai potensi nyata penerapan aplikasi ini di masa depan.

---

### 1. Kondisi Rileks & Sehat (Sistem Saraf Seimbang)
*   **Pola Pupil:** Frekuensi Sedang, Fluktuasi Sedang (Stabil).
*   **Penjelasan:** Saraf simpatik (gas) dan parasimpatik (rem) bekerja seimbang. Pupil merespons lingkungan dengan tenang tanpa regangan ekstrem.
*   **Bukti Ilmiah:** Pada subjek yang sadar penuh dan sehat, pupil tetap relatif stabil dengan fluktuasi amplitudo minimum (sekitar 0.3–0.5 mm) saat beristirahat tanpa beban pikiran. *(Referensi 1)*

### 2. Kondisi Mengantuk Berat & Kelelahan (*Drowsiness / Fatigue*)
*   **Pola Pupil:** Frekuensi Lambat (< 0.8 Hz), Fluktuasi Sangat Tinggi (*Fatigue Waves*).
*   **Penjelasan:** Di luar dugaan banyak orang, saat otak kelelahan menahan kantuk, kendali saraf otonom akan goyah. Ini memicu munculnya "Gelombang Kelelahan" (*Fatigue Waves*). Pupil tidak lagi bergetar cepat, melainkan perlahan-lahan merenggang lebar dan menyusut secara ekstrem di luar kendali sadar pasien.
*   **Bukti Ilmiah:** *Pupillary Unrest Index* (PUI) terbukti meningkat tajam pada supir atau pekerja shift yang kelelahan. Jurnal medis mencatat bahwa saat individu mulai mengantuk, amplitudo osilasi pupil yang berfrekuensi rendah (< 0.8 Hz) akan membesar secara signifikan hingga beberapa milimeter. *(Referensi 1 & 2)*

### 3. Kondisi Stres Berat, Beban Kognitif Tinggi, atau Panik (*Hyper-Arousal*)
*   **Pola Pupil:** Frekuensi Tinggi (Bergetar Cepat), Fluktuasi Bervariasi.
*   **Penjelasan:** Saat pasien dihadapkan pada masalah yang rumit (ujian matematika) atau situasi menegangkan (*Fight or Flight*), sistem saraf simpatik yang ditenagai adrenalin akan mendominasi otak. Hal ini memaksa otot mata untuk siaga tinggi dan bergetar (*twitching*) dengan frekuensi tinggi.
*   **Bukti Ilmiah:** *Task-evoked pupillary response* (TEPR) mengonfirmasi bahwa peningkatan beban kognitif berbanding lurus dengan ketidakstabilan frekuensi pupil akibat intervensi kuat dari saraf simpatik. *(Referensi 3)*

### 4. Kondisi Kerusakan Saraf, Koma, atau Pengaruh Obat Depresan
*   **Pola Pupil:** Frekuensi Nyaris Nol, Fluktuasi Sangat Rendah (*Stiff Pupil*).
*   **Penjelasan:** Sistem saraf gagal memberikan sinyal listrik ke otot *sphincter pupillae*. Pupil terlihat diam membatu (kaku) dan menolak untuk merenggang.
*   **Bukti Ilmiah:** Hilangnya refleks alami dan fluktuasi dinamis pupil adalah indikator klinis darurat utama pada diagnosis cedera otak traumatis (*Traumatic Brain Injury*), koma, atau keracunan zat sedatif saraf (narkotika/alkohol berat). *(Referensi 4)*

---

### 📚 Referensi Jurnal Ilmiah Tertaut:
Kutip jurnal-jurnal kedokteran ini jika penguji meragukan validitas hipotesis di atas:

1. **Wilhelm, B., et al. (1998).** *"Pupillary unrest changes with sleepiness"*. (Jurnal ini adalah pondasi penemuan *Pupillary Unrest Index* / PUI sebagai penanda objektif untuk mendeteksi rasa kantuk yang memicu bahaya mikrosleep).
2. **Lüdtke, H., et al. (1998).** *"Mathematical procedures in data recording and processing of pupillary fatigue waves"*. (Menyebutkan bukti nyata gelombang lambat frekuensi < 0.8 Hz dengan amplitudo tinggi saat pasien mulai tertidur).
3. **Beatty, J. (1982).** *"Task-evoked pupillary responses, processing load, and the structure of information processing"*. (Membahas kaitan dilatasi dan getaran pupil saat otak diberikan beban pikiran berat / stres kognitif).
4. **Ritter, A. M., et al. (1999).** *"Pupillary light reflex in traumatic brain injury"*. (Membahas kakunya pupil pada pasien gegar otak).
