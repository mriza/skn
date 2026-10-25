# INSTRUMEN EVALUASI: KUIS & TUGAS PERTEMUAN 2
**Mata Kuliah:** Sistem Komunikasi Nirkabel  
**Topik:** Serangan Nirkabel Modern & Arsitektur Keamanan Enterprise  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Pertemuan:** Minggu X  

---

## BAGIAN 1: KUIS TEKNIS AUDIT & HARDENING WIRELESS (DURASI: 45 MENIT)

### A. Soal Pilihan Ganda (Bobot: 50 Poin / @5 Poin)

1. Serangan Deauthentication Flooding dapat memutuskan stasiun dari Access Point secara instan karena pada standar 802.11 lama:
   - A. Sinyal radio otomatis mati saat menerima paket ping.
   - B. Frame manajemen 802.11 tidak dienkripsi dan tidak memiliki tanda tangan keaslian sumber sehingga mudah dipalsukan (*spoofed*).
   - C. Penyerang memotong kabel fiber optik backend.
   - D. Frekuensi microwave mengalami interferensi hujan.

2. Standar IEEE yang dirancang khusus untuk mengenkripsi dan melindungi integritas frame manajemen (*Protected Management Frames*) dari serangan deautentikasi palsu adalah:
   - A. IEEE 802.11b
   - B. IEEE 802.11w
   - C. IEEE 802.3u
   - D. IEEE 802.1Q

3. Seorang penyerang mendirikan Access Point tiruan dengan SSID dan MAC Address yang sama persis dengan Wi-Fi resmi kampus, lalu menyajikan halaman login Captive Portal palsu untuk mencuri username dan password mahasiswa. Teknik serangan ini dinamakan:
   - A. RF Jamming
   - B. Evil Twin Attack
   - C. Buffer Overflow
   - D. SYN Flood

4. Perangkat Access Point tidak sah yang dicolokkan secara diam-diam oleh oknum ke colokan dinding LAN kampus tanpa izin administrator sehingga membuka pintu belakang (*backdoor*) disebut:
   - A. Rogue Access Point
   - B. Repeater Resmi
   - C. Bridge Network
   - D. Core Switch

5. Serangan pencurian hash WPA2 tanpa memerlukan stasiun klien terhubung (*clientless attack*) yang memanfaatkan fitur roaming IEEE 802.11r disebut:
   - A. SQL Injection
   - B. PMKID Attack
   - C. Ping of Death
   - D. Cross-Site Scripting (XSS)

6. Pada arsitektur WPA-Enterprise (IEEE 802.1X), komponen yang bertindak sebagai pemutus kebijakan akses dan gerbang awal (*gatekeeper*) adalah:
   - A. Supplicant (Perangkat Klien)
   - B. Authenticator (Access Point / Wireless LAN Controller)
   - C. Database LDAP
   - D. Kabel Patch Cord

7. Metode EAP pada otentikasi 802.1X yang memberikan tingkat keamanan tertinggi dengan mewajibkan sertifikat digital terpasang baik di sisi server RADIUS maupun di sisi perangkat klien adalah:
   - A. EAP-MD5
   - B. EAP-TLS
   - C. PEAP-MSCHAPv2
   - D. PAP

8. Fitur pada Access Point yang menonaktifkan fungsi *forwarding* langsung antar-stasiun nirkabel sehingga sesama klien di SSID yang sama tidak dapat saling menyerang atau menyadap data dinamakan:
   - A. Client Isolation (Default Forwarding = No)
   - B. Transmit Power Control
   - C. Dynamic Frequency Selection (DFS)
   - D. SSID Broadcast

9. Sistem pemantauan jaringan nirkabel yang berfungsi mendeteksi keberadaan Rogue AP, jammer, dan serangan deauth secara otomatis selama 24 jam penuh disebut:
   - A. DNS Server
   - B. WIDS / WIPS (Wireless Intrusion Detection & Prevention System)
   - C. NTP Client
   - D. NAT Gateway

10. Fitur koneksi otomatis pada router rumahan yang memiliki kerentanan fatal terhadap serangan brute-force PIN menggunakan tools *Reaver* atau *Pixie Dust* adalah:
    - A. WPA3 Enterprise
    - B. WPS (Wi-Fi Protected Setup)
    - C. RADIUS Accounting
    - D. 802.11ac Beamforming

---

### B. Soal Studi Kasus Troubleshooting Lapangan (Bobot: 50 Poin / @25 Poin)

**Kasus 1 (Analisis Insiden Serangan Evil Twin di Kantin Kampus):**  
Di area kantin kampus Politani, sejumlah mahasiswa melaporkan bahwa akun Sistem Informasi Akademik (SIAKAD) mereka telah dibajak oleh pihak tidak dikenal setelah login ke Wi-Fi "POLITANI-FREE". Analisis awal tim IT menemukan adanya sinyal Wi-Fi dengan nama SSID yang sama persis memancar dari laptop penyerang yang berada di sudut kantin.  
*Pertanyaan:*
1. Jelaskan secara teknis skenario bagaimana penyerang mengeksekusi serangan Evil Twin ini hingga berhasil mencuri kredensial akun mahasiswa!
2. Sebagai teknisi jaringan nirkabel, berikan 3 langkah mitigasi konkret yang harus diterapkan oleh kampus untuk mencegah keberhasilan serangan serupa di masa depan!

**Kasus 2 (Perancangan Migrasi ke WPA-Enterprise):**  
Saat ini seluruh ruang dosen menggunakan satu kata sandi bersama (*Pre-Shared Key*). Ketika seorang staf atau asisten lab mengundurkan diri, kata sandi tersebut berisiko disalahgunakan dari area parkir luar gedung.  
*Pertanyaan:*
1. Mengapa implementasi WPA2/WPA3 Enterprise (802.1X / RADIUS) menjadi solusi paling tepat untuk mengatasi masalah tersebut?
2. Jelaskan alur proses yang terjadi di jaringan saat seorang dosen baru pertama kali melakukan login menggunakan akun pribadinya (Supplicant -> Authenticator -> RADIUS Server)!

---

## BAGIAN 2: TUGAS BESAR TERSTRUKTUR (TAKE-HOME CAPSTONE PROJECT)

### Judul Tugas:
**"Perancangan Blueprint Arsitektur Keamanan Jaringan Wireless Enterprise Tersegmentasi Berbasis 802.1X, VLAN, dan WIPS untuk Politeknik Pertanian Negeri"**

### Ketentuan Tugas:
1. Sifat: Tugas Kelompok (2 Mahasiswa per kelompok).
2. Waktu Pengerjaan: 1 Minggu setelah Pertemuan 2.
3. Luaran: Dokumen Desain Teknis (PDF, 8 - 12 Halaman) dan File Konfigurasi Backup RouterOS MikroTik / Packet Tracer.

### Muatan Wajib Laporan:
1. **Analisis Risiko & Kebutuhan Kampus:** Identifikasi potensi ancaman di lingkungan kampus Politeknik Pertanian Negeri.
2. **Desain Topologi Segmentasi Multi-SSID:**
   - SSID Dosen & Staf (`POLITANI-STAFF`): VLAN 10, WPA2/WPA3 Enterprise via RADIUS, PMF Required.
   - SSID Mahasiswa (`POLITANI-MAHASISWA`): VLAN 20, Otentikasi Akun SIAKAD, Bandwidth Limitation per user.
   - SSID Tamu (`POLITANI-GUEST`): VLAN 30, Captive Portal, Client Isolation Aktif, Firewall isolasi dari subnet internal.
3. **Mekanisme Deteksi Rogue AP (WIDS/WIPS):** Strategi pemindaian background scan AP untuk melacak pemancar tidak sah.
4. **Panduan Kebijakan Keamanan (Security Policy Document):** SOP manajemen akun, masa berlaku kata sandi, dan sertifikat digital.

---

## BAGIAN 3: KUNCI JAWABAN KUIS PILIHAN GANDA
1. **B** | 2. **B** | 3. **B** | 4. **A** | 5. **B** | 6. **B** | 7. **B** | 8. **A** | 9. **B** | 10. **B**
