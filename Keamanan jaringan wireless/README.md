# Keamanan Jaringan Wireless (Minggu IX & X)

**Mata Kuliah:** Sistem Komunikasi Nirkabel  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Total Alokasi Waktu:** 2 Pertemuan x 210 Menit (Total 420 Menit / 6 Jam Pembelajaran)  

---

## DOKUMEN SUMBER & PENDAMPING DOSEN/MAHASISWA

Modul perkuliahan ini terintegrasi penuh dengan dokumen acuan pengajaran berikut di direktori ini:
1. 📄 **[Bacaan_Mahasiswa_Keamanan_Nirkabel.docx](Bacaan_Mahasiswa_Keamanan_Nirkabel.docx)** — Diktat bacaan komprehensif mahasiswa mencakup 8 bab teori dan latihan.
2. 📄 **[Catatan_Dosen_Keamanan_Nirkabel.docx](Catatan_Dosen_Keamanan_Nirkabel.docx)** — Buku panduan dosen pengampu (skenario ceramah per sesi, tanya-jawab antisipatif, rubrik penilaian).
3. 📊 **[Slide Pertemuan 1](Pertemuan%201%20-%20Dasar%20Keamanan%20dan%20Enkripsi%20Nirkabel/Slide_Pertemuan_1_Dasar_Keamanan_Enkripsi.pptx)** & **[Slide Pertemuan 2](Pertemuan%202%20-%20Serangan%20dan%20Pengamanan%20Enterprise/Slide_Pertemuan_2_Serangan_Pengamanan_Enterprise.pptx)** — Presentasi slide 16:9 widescreen masing-masing 20 slides terstruktur untuk 6 sesi perkuliahan.

---

## PEMBAGIAN 2 PERTEMUAN KULIAH & PRAKTIKUM

Sesuai silabus distribusi tugas TRK Politani, topik Keamanan Jaringan Wireless dibagi menjadi **2 pertemuan perkuliahan & praktikum mandiri**:

### 📁 [Pertemuan 1 - Dasar Keamanan dan Enkripsi Nirkabel](Pertemuan%201%20-%20Dasar%20Keamanan%20dan%20Enkripsi%20Nirkabel/) *(Minggu IX)*
Fokus pada pemahaman fundamental kerentanan media RF, mode interface, evolusi protokol enkripsi (WEP $\rightarrow$ TKIP $\rightarrow$ AES-CCMP $\rightarrow$ WPA3), dan derivasi kunci:
* 📖 **[Materi.md](Pertemuan%201%20-%20Dasar%20Keamanan%20dan%20Enkripsi%20Nirkabel/Materi.md)** *(Kuliah Teori 210 Menit)*:
  * **Mode Interface Nirkabel:** Managed (Station), Master (AP), Monitor (Promiscuous RF Sniffing), Ad-Hoc, dan Mesh.
  * **Konsep Wardriving:** Pemetaan sinyal nirkabel mobile dengan adapter high-gain, GPS, dan database WiGLE.
  * **Apa itu IV & Bahaya Ruang Gerak IV Kecil:** Fungsi Initialization Vector pada RC4 stream cipher, kalkulasi habisnya ruang $2^{24}$ (16,7 juta paket) dalam hitungan jam di jaringan sibuk, pembuktian matematis $C_1 \oplus C_2 = P_1 \oplus P_2$ (bocoran keystream saat IV collision), serta serangan FMS dan PTW.
  * **WPA-TKIP (Stopgap):** 3 lapis perbaikan (IV 48-bit, Per-Packet Key Mixing Phase 1 & 2, Michael MIC), dan keruntuhannya via *Beck-Tews attack*.
  * **WPA2 & AES-CCMP:** Mengapa block cipher 128-bit menggantikan stream cipher, serta peran CCMP (CTR untuk Confidentiality + CBC-MAC untuk Integrity).
  * **Derivasi Kunci PMK vs PTK:** Pembentukan PMK 256-bit via PBKDF2 (mengapa SSID menjadi salt penting), pertukaran 4-Way Handshake (M1 s/d M4), derivasi PTK 512-bit via PRF-512, serta fungsi 4 sub-kunci (KCK, KEK, TK, MIC Key).
  * **Celah Offline Dictionary Attack:** Mengapa rekaman M1 dan M2 memungkinkan penyerang melakukan brute-force lokal via Hashcat tanpa menyentuh AP target.
  * **WPA3-SAE & Mitos Keamanan:** Dragonfly handshake berbasis Zero-Knowledge Proof (ZKP), Forward Secrecy, serta pembongkaran mitos Hide SSID dan MAC Filtering.
* 🔬 **[Praktikum.md](Pertemuan%201%20-%20Dasar%20Keamanan%20dan%20Enkripsi%20Nirkabel/Praktikum.md)** *(Eksperimen Lab 210 Menit)*:
  * Setup monitor mode (`airmon-ng`), reconnaissance spektrum pasif (`airodump-ng`), capture 4-Way Handshake pada target lab, bedah field ANonce/SNonce/MIC di Wireshark, dan uji bypass MAC Filtering (`macchanger`).
* 📝 **[Kuis_Tugas.md](Pertemuan%201%20-%20Dasar%20Keamanan%20dan%20Enkripsi%20Nirkabel/Kuis_Tugas.md)** *(Evaluasi Pembelajaran)*:
  * Kuis 45 menit (10 PG + 2 Soal Hitungan Analisis IV Collision & 4 Sub-kunci PTK) serta tugas laporan bedah paket Wireshark.

---

### 📁 [Pertemuan 2 - Serangan dan Pengamanan Enterprise](Pertemuan%202%20-%20Serangan%20dan%20Pengamanan%20Enterprise/) *(Minggu X)*
Fokus pada audit kerentanan serangan aktif nirkabel, mitigasi DoS, dan arsitektur pengamanan WLAN enterprise:
* 📖 **[Materi.md](Pertemuan%202%20-%20Serangan%20dan%20Pengamanan%20Enterprise/Materi.md)** *(Kuliah Teori 210 Menit)*:
  * Mengapa enkripsi AES saja tidak cukup? (Kriptografi kuat gagal jika protokol di sekitarnya cacat).
  * Taksonomi serangan aktif: Deauthentication Flooding (eksploitasi frame 802.11 unencrypted), Rogue AP internal, dan Evil Twin Attack (Master mode + Captive Portal Phishing).
  * Serangan lanjutan: KRACK (Key Reinstallation pada Message 3) dan PMKID Attack (clientless hash capture via 802.11r).
  * Arsitektur WPA-Enterprise (IEEE 802.1X): Supplicant, Authenticator, dan FreeRADIUS server. Komparasi EAP-TLS (sertifikat) vs PEAP-MSCHAPv2 (username/password).
  * Pertahanan Enterprise: Protected Management Frames (PMF / IEEE 802.11w), WIDS/WIPS, Client Isolation (`default-forwarding=no`), dan segmentasi Guest VLAN.
* 🔬 **[Praktikum.md](Pertemuan%202%20-%20Serangan%20dan%20Pengamanan%20Enterprise/Praktikum.md)** *(Eksperimen Lab 210 Menit)*:
  * Simulasi serangan deauth (`aireplay-ng`), hardening Access Point MikroTik (PMF 802.11w required, nonaktifkan WPS, Client Isolation), validasi mitigasi pasca-hardening, dan segmentasi Guest VLAN.
* 📝 **[Kuis_Tugas.md](Pertemuan%202%20-%20Serangan%20dan%20Pengamanan%20Enterprise/Kuis_Tugas.md)** *(Evaluasi Pembelajaran)*:
  * Kuis 45 menit (10 PG + 2 Kasus Lapangan) dan Tugas Besar (Capstone Project) Blueprint Keamanan WLAN Kampus Politani.
