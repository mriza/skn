# Konfigurasi Antena Grid secara Point to Point (Minggu XII)

**Mata Kuliah:** Sistem Komunikasi Nirkabel  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Alokasi Waktu:** 3 x 70 menit (210 menit)  

---

## DAFTAR DOKUMEN PEMBELAJARAN TERPISAH

Modul pembelajaran untuk topik Konfigurasi Antena Grid Point to Point telah dipisahkan menjadi file-file dokumen komprehensif berikut:

1. 🖥️ **[Slide_Pertemuan_4_Konfigurasi_Antena_Grid_PTP.pptx](Slide_Pertemuan_4_Konfigurasi_Antena_Grid_PTP.pptx)** *(Slide Presentasi Perkuliahan 20 Slides - Format 16:9 Widescreen)*
   - Slide berdesain modern dengan Reload terpadu P1-P3, arsitektur PTP backhaul, kalkulasi zona Fresnel & kelengkungan bumi, anatomi kisi grid, polarisasi V/H, setting Distance & TDMA NV2 RouterOS, SOP pointing presisi, dan mitigasi Side Lobe Trap.

2. 📖 **[Materi.md](Materi.md)**
   - Rencana perkuliahan teori 210 menit.
   - Uraian materi mendalam: Arsitektur wireless backhaul PTP, anatomi reflektor parabola kisi aluminium (ketahanan wind load, focal point, pengaturan polarisasi $90^\circ$ feed horn), limitasi CSMA/CA pada link jauh (masalah Hidden Node & ACK Timeout), protokol TDMA proprietary (MikroTik NV2 / Ubiquiti airMAX), trade-off channel width (10/20/40 MHz), parameter kualitas link (RSSI, SNR, CCQ, MCS), dan teknik menghindari jebakan Side Lobe (*Side Lobe Trap*).

2. 🔬 **[Praktikum.md](Praktikum.md)**
   - Modul eksperimen laboratorium & lapangan 210 menit.
   - Panduan kerja step-by-step: Pembagian tim Stasiun A (Master AP) & Stasiun B (Slave Client), perakitan fisik antena grid & feed horn, pengkabelan PoE & pigtail RF, konfigurasi RouterOS MikroTik (ap-bridge & station-bridge), metodologi fine-pointing (azimuth & elevasi), pengujian performa link (Ping test latency & BTest UDP/TCP throughput), lembar pengamatan lapangan, dan format laporan.

3. 📝 **[Kuis_Tugas.md](Kuis_Tugas.md)**
   - Instrumen evaluasi pembelajaran.
   - 10 Soal Pilihan Ganda berbobot + 2 Soal Analisis Kasus Lapangan Troubleshooting Link PTP Fluktuatif & Interferensi Spektrum (lengkap dengan Kunci Jawaban & Pembahasan Solutif).
   - Tugas Terstruktur (Proposal Desain Teknis): Perencanaan Link Point to Point Antena Grid 5 KM Menara-ke-Menara lengkap dengan estimasi link budget dan Bill of Materials (BOM).
