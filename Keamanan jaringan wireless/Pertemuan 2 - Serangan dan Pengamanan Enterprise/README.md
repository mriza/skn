# Pertemuan 2 (Minggu X): Serangan Nirkabel Modern & Arsitektur Keamanan Enterprise

**Mata Kuliah:** Sistem Komunikasi Nirkabel  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Alokasi Waktu:** 3 x 70 menit (210 menit)  

---

## DAFTAR DOKUMEN PEMBELAJARAN PERTEMUAN 2

1. 📖 **[Materi.md](Materi.md)** *(Kuliah Teori 210 Menit)*
   - Taksonomi serangan wireless: Eavesdropping, Man-in-the-Middle (MitM), DoS.
   - Serangan Deauthentication Flooding (eksploitasi frame manajemen 802.11 unencrypted).
   - Rogue Access Point vs Evil Twin Attack & captive portal phishing.
   - Serangan lanjutan: PMKID Attack (clientless), KRACK Attack, dan kelemahan WPS.
   - Arsitektur WPA-Enterprise (IEEE 802.1X): Supplicant, Authenticator, dan RADIUS Server.
   - Sistem Pertahanan: Protected Management Frames (PMF / IEEE 802.11w), WIDS/WIPS, dan segmentasi VLAN.

2. 🔬 **[Praktikum.md](Praktikum.md)** *(Eksperimen Lab 210 Menit)*
   - Simulasi audit serangan deautentikasi terarah (`aireplay-ng`).
   - Implementasi hardening pada Access Point MikroTik: Mengaktifkan PMF 802.11w required, mematikan WPS.
   - Konfigurasi Client Isolation (`default-forwarding=no`) dan segmentasi Guest VLAN.
   - Validasi ulang resistensi serangan: Pembuktian koneksi klien tetap stabil dari serangan deauth setelah PMF aktif.
   - Lembar data pengamatan dan sistematika laporan.

3. 📝 **[Kuis_Tugas.md](Kuis_Tugas.md)** *(Evaluasi Pembelajaran)*
   - Kuis 45 Menit: 10 Soal Pilihan Ganda + 2 Studi Kasus Troubleshooting Lapangan (Evil Twin di kantin & migrasi ke 802.1X).
   - Tugas Terstruktur (Capstone Project): Perancangan Blueprint Keamanan Jaringan Wireless Enterprise Kampus Politani.
