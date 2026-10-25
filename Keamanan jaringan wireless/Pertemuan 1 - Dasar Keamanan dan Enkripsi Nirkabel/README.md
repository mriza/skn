# Pertemuan 1 (Minggu IX): Dasar Keamanan, Protokol Enkripsi, & Autentikasi Nirkabel

**Mata Kuliah:** Sistem Komunikasi Nirkabel  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Alokasi Waktu:** 3 x 70 menit (210 menit)  
**Dokumen Referensi Guru & Mahasiswa:** `Bacaan_Mahasiswa_Keamanan_Nirkabel.docx`, `Catatan_Dosen_Keamanan_Nirkabel.docx`, `Slide_Keamanan_Nirkabel.pptx`

---

## DAFTAR DOKUMEN PEMBELAJARAN LENGKAP

1. 📖 **[Materi.md](Materi.md)** *(Kuliah Teori 210 Menit)*
   - **Mode Interface Nirkabel:** Karakteristik dan fungsi Managed (Station), Master (AP), Monitor (Promiscuous RF Sniffing), Ad-Hoc, dan Mesh.
   - **Konsep Wardriving:** Metodologi pemetaan jaringan nirkabel mobile berbasis perangkat GPS dan aplikasi WiGLE.
   - **Apa itu IV & Mengapa Ruang Gerak IV Kecil Sangat Berisiko:** Fungsi Initialization Vector pada RC4 stream cipher, kalkulasi habisnya ruang $2^{24}$ (16,7 juta paket) dalam hitungan jam di jaringan sibuk, pembuktian matematis $C_1 \oplus C_2 = P_1 \oplus P_2$ (kebocoran keystream saat terjadi IV collision), serta prinsip serangan FMS dan PTW.
   - **WPA & TKIP (Solusi Stopgap):** Tiga lapis penambal (IV 48-bit, Per-Packet Key Mixing Phase 1 & 2, Michael MIC 64-bit), serta alasan deprecation akibat *Beck-Tews attack*.
   - **WPA2 & AES-CCMP:** Mengapa block cipher 128-bit AES menggantikan stream cipher RC4, serta fungsi mode CCMP (CTR untuk Confidentiality + CBC-MAC untuk Integrity).
   - **Arsitektur Derivasi Kunci (PMK vs PTK):** Pembentukan PMK 256-bit via PBKDF2 (mengapa SSID menjadi salt), mekanisme pertukaran 4-Way Handshake (pesan M1 s/d M4), derivasi PTK 512-bit via PRF-512, serta fungsi 4 sub-kunci (KCK, KEK, TK, MIC Key).
   - **Celah Offline Dictionary Attack:** Mengapa penangkapan frame M1 dan M2 memungkinkan penyerang melakukan brute force lokal via Hashcat/Aircrack-ng tanpa menyentuh AP target.
   - **Standar Baru WPA3-SAE & Mitos:** Pertukaran kunci Dragonfly berbasis Zero-Knowledge Proof (ZKP), Forward Secrecy, serta pembongkaran mitos Hide SSID dan MAC Filtering.

2. 🔬 **[Praktikum.md](Praktikum.md)** *(Eksperimen Lab 210 Menit)*
   - **Tahap 1:** Eksplorasi mode interface wireless (mengubah kartu jaringan dari Managed ke Monitor mode via `airmon-ng`).
   - **Tahap 2:** Reconnaissance pasif spektrum RF dan simulasi wardriving (`airodump-ng`).
   - **Tahap 3:** Perekaman frame asosiasi 4-Way Handshake pada target lab ke file `.cap`.
   - **Tahap 4:** Dekonstruksi struktur paket di Wireshark (analisis RSN Info pada Beacon, pelacakan field ANonce pada M1, serta SNonce dan MIC pada M2).
   - **Tahap 5:** Pembuktian ketidakefektifan MAC Filtering melalui teknik MAC spoofing (`macchanger`).

3. 📝 **[Kuis_Tugas.md](Kuis_Tugas.md)** *(Instrumen Evaluasi Pembelajaran)*
   - **Kuis 45 Menit:** 10 Soal Pilihan Ganda berbobot mengenai IV, IV Collision, Wardriving, TKIP, AES, PMK, PTK, dan Mode Interface + 2 Soal Analisis Kritis (Hitungan habisnya IV collision dan arsitektur 4 subkunci PTK) lengkap dengan kunci jawaban.
   - **Tugas Terstruktur:** Laporan analisis paket capture Wireshark dan tabel komparasi teknis 4 generasi protokol enkripsi.
