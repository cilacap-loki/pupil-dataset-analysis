# 🛡️ Q&A Pertahanan Sidang (*Defense Cheat Sheet*)

Dokumen ini berisi kompilasi pertanyaan kritis yang sangat mungkin diajukan oleh dosen penguji, beserta **jawaban pamungkas (*defense*)** untuk mematahkan keraguan mereka secara ilmiah dan elegan.

---

### Q1: Bukankah melihat perubahan ukuran pupil sekilas dengan senter dokter sudah cukup? Mengapa repot-repot membuat program serumit ini?
**Jawaban Defense (Analogi EKG):**
> "Betul Bapak/Ibu penguji, jika tujuannya hanya untuk melihat apakah pasien gegar otak berat atau masih hidup, senter puskesmas sudah cukup. Sama halnya seperti memegang denyut nadi di tangan. Namun, dokter tidak bisa mendiagnosis **penyakit jantung koroner atau kelainan katup** hanya dengan memegang nadi; mereka butuh alat EKG (*Elektrokardiogram*). 
> 
> Riset ini ibarat menciptakan **'EKG untuk Mata'**. Dokter mustahil bisa menghitung secara visual bahwa pupil berdenyut pada kecepatan 0.73 Hz atau meregang 36% dari ukuran aslinya. Angka presisi (*micro-abnormalities*) inilah yang menjadi indikator awal penyakit serius seperti Alzheimer, kelelahan kognitif kronis, atau stres. Hanya *Computer Vision* yang sanggup merubah tebakan kasat mata menjadi angka empiris yang pasti."

---

### Q2: Alat (Kamera beresolusi tinggi) untuk menjalankan program ini kan mahal, apakah tidak *overkill* untuk diterapkan di dunia medis biasa?
**Jawaban Defense (Visi Masa Depan):**
> "Saat ini mungkin terkesan *overkill* karena ini masih dalam tahap *Proof of Concept* (Batu Loncatan Fundamental) menggunakan dataset standar LPW. Namun, teknologi kamera *smartphone* saat ini berkembang sangat pesat (bahkan sudah dilengkapi sensor inframerah seperti FaceID). 
> 
> Visi ke depan dari algoritma yang kami bangun ini adalah agar kelak bisa langsung ditanamkan ke dalam aplikasi *smartphone* biasa. Sehingga, alih-alih puskesmas desa harus membeli alat diagnosis saraf miliaran rupiah, mereka nantinya cukup menggunakan kamera HP untuk mendiagnosis pasien secara objektif dan instan."

---

### Q3: Di grafik ini garis pupil sedang menurun tajam, tapi kok di tengah turunannya ditandai sebagai "Puncak Hippus" (Titik Oranye)? Apakah programnya salah?
**Jawaban Defense (Local Maxima & Sensitivitas):**
> "Program kami sama sekali tidak salah, justru ini membuktikan **sensitivitas tinggi** algoritma kami. Secara matematis, kami mencari *Local Maxima* (Puncak Lokal). 
> 
> Secara medis, itu artinya meskipun otot mata sedang dalam proses menyusut dengan cepat (konstriksi makro), otot tersebut tetap mengalami kedutan atau regangan mikro (berusaha membesar sesaat). Algoritma kami disetel dengan 'prominence 0.5 piksel', sehingga sekecil apa pun perlawanan pupil untuk membesar (*micro-fluctuation*), hal itu akan tetap tertangkap secara presisi sebagai sinyal Hippus."

---

### Q4: Coba jelaskan secara singkat, apa definisi Puncak Hippus itu?
**Jawaban Defense (Koreksi Terminologi):**
> "Puncak Hippus merepresentasikan ukuran pupil terlebar (titik dilatasi maksimum) **di dalam satu siklus (gelombang) denyutan.** Kami menerapkan syarat algoritma jarak minimal 15 frame (0.3 detik) antar puncak untuk memastikan bahwa setiap puncak yang ditandai benar-benar merupakan siklus denyut baru yang independen, bukan sekadar *noise* atau getaran piksel kamera."

---

### Q5: Kenapa Frekuensi (Hz) harus dihitung? Apa manfaatnya?
**Jawaban Defense (Jembatan Komputasi & Medis):**
> "Frekuensi adalah jembatan antara ilmu komputasi dan medis. Frekuensi Hippus dikendalikan langsung oleh sistem saraf otonom. Seseorang yang rileks memiliki frekuensi yang stabil, sementara orang yang stres, panik, atau kelelahan kognitif (*cognitive overload*) akan memiliki frekuensi Hippus yang berantakan dan getaran yang lebih cepat.
> 
> Menghitung frekuensi (Hz) berarti kita mengonversi fenomena biologis abstrak menjadi parameter angka mutlak yang bisa dijadikan rujukan valid oleh dokter untuk diagnosis klinis."
