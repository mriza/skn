# Antena (Minggu XI)

**Mata Kuliah:** Sistem Komunikasi Nirkabel  
**Topik Khusus:** Panduan Praktis Antena Wireless untuk Network Engineer  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Alokasi Waktu:** 3 x 70 menit (210 menit)  
**Pendekatan:** Aplikatif & Praktis (Applied Computer & Network Engineering)

---

## DAFTAR DOKUMEN PEMBELAJARAN TERAPAN

Modul pembelajaran topik Antena dirancang khusus untuk mahasiswa Teknologi Rekayasa Komputer (TRK) dengan menitikberatkan pada aspek **pemilihan perangkat, instalasi lapangan, pembacaan spesifikasi teknis (datasheet), pemahaman sudut pancar, dan analisis kualitas sinyal riil**, tanpa beban turunan rumus fisika teoretis yang rumit:

1. 🖥️ **[Slide_Pertemuan_3_Panduan_Praktis_Antena.pptx](Slide_Pertemuan_3_Panduan_Praktis_Antena.pptx)** *(Slide Presentasi Perkuliahan 20 Slides - Format 16:9 Widescreen)*
   - Slide berdesain modern dengan Reload materi keamanan P1-P2, bedah satuan dBm/dBi/EIRP, field guide 5 tipe antena, analisis beamwidth HPBW, polarisasi V/H, mitigasi dead zone via downtilt, checklist metrik sinyal, dan panduan membaca datasheet.

2. 📖 **[Materi.md](Materi.md)** *(Kuliah Teori Terapan 210 Menit)*
   - **Prinsip Intuitif:** Analogi balon air & lampu senter vs bohlam (antena sebagai pengarah energi, bukan penambah daya listrik).
   - **Field Guide Jenis Antena:** Kapan memilih antena Omni (hotspot $360^\circ$), Panel (CPE/lorong), Sectoral (Base Station WISP), dan Grid (PTP jarak jauh tahan angin).
   - **Karakteristik Beam Praktis:** Membaca sudut Horizontal (Azimuth) vs Vertikal (Elevasi) di datasheet, trade-off Gain vs Sudut Berkas, serta solusi blind spot di bawah tower via *Downtilt*.
   - **Power & Kualitas Sinyal:** Menghitung total daya pancar legal (EIRP sesuai regulasi Kominfo), fungsi Front-to-Back (F/B) ratio agar tidak saling ganggu di satu tiang, dan tabel indikator standar kelayakan engineer (RSSI, Noise Floor, SNR, CCQ).

2. 🔬 **[Praktikum.md](Praktikum.md)** *(Eksperimen Lab Terapan 210 Menit)*
   - **Eksperimen 1:** Bedah fisik antena dan latihan membaca lembar datasheet komersial (Gain dBi, HPBW, polarisasi, konektor RF, wind load).
   - **Eksperimen 2:** Uji sebaran sinyal nyata (Coverage Mapping) membandingkan antena Omni vs Directional Panel pada jarak 10 meter menggunakan aplikasi Wi-Fi Analyzer.
   - **Eksperimen 3:** Simulasi perencanaan link wireless jarak jauh (2 - 5 km) menggunakan software web planner praktis (*Ubiquiti ISP Design Center / airLink*) untuk menentukan tinggi tiang dan estimasi kapasitas throughput.
   - Lembar data pengamatan mahasiswa dan panduan checklist instalasi.

3. 📝 **[Kuis_Tugas.md](Kuis_Tugas.md)** *(Instrumen Evaluasi Terapan)*
   - **Kuis 45 Menit:** 10 Soal Pilihan Ganda praktis (pemilihan antena, beamwidth, mitigasi dead zone bawah menara, hitungan cepat EIRP, F/B ratio, interpretasi RSSI) + 2 Studi Kasus Riil Lapangan (Pemilihan antena kampus Politani vs troubleshooting interferensi back-lobe di tiang yang sama).
   - **Tugas Terstruktur:** Penyusunan panduan pemilihan antena dan Bill of Materials (BOM) komersial untuk kebutuhan jaringan nirkabel kampus.
