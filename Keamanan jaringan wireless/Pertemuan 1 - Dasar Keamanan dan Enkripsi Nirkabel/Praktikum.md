# MODUL PRAKTIKUM: MODE INTERFACE, AUDIT RECONNAISSANCE, & ANALISIS 4-WAY HANDSHAKE
**Mata Kuliah:** Sistem Komunikasi Nirkabel  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Pertemuan:** Minggu IX (Pertemuan 1 Modul Keamanan)  
**Alokasi Waktu:** 210 Menit (3 x 70 menit)

---

## 1. ALOKASI WAKTU PRAKTIKUM (TOTAL: 210 MENIT)

| Tahap | Durasi | Deskripsi Aktivitas Praktikan |
| :---: | :---: | :--- |
| **I** | 15 Menit | **Briefing K3, Etika Laboratorium, & Pengenalan Instrumen RF**<br>- Penegasan batasan hukum (UU ITE): Larangan sniffing/penyerangan di luar BSSID lab terisolasi.<br>- Distribusi USB Wireless Adapter berspesifikasi *Monitor Mode & Packet Injection*. |
| **II** | 45 Menit | **Tahap 1: Eksplorasi Mode Interface Kartu Jaringan Nirkabel**<br>- Pengecekan antarmuka bawaan dalam mode **Managed** menggunakan `iwconfig` dan `ip link`.<br>- Pembersihan proses sistem pengganggu: `sudo airmon-ng check kill`.<br>- Transisi antarmuka ke mode **Monitor**: `sudo airmon-ng start wlan0`.<br>- Verifikasi status promiscuous RF sniffing. |
| **III** | 45 Menit | **Tahap 2: Reconnaissance Spektrum Nirkabel & Simulasi Wardriving**<br>- Pemindaian pasif seluruh Access Point sekitar lab menggunakan `airodump-ng`.<br>- Pemetaan kolom parameter: BSSID, Power (RSSI dBm), Beacon, Data, Kanal (CH), Cipher (CCMP/TKIP/WEP), dan Auth (PSK/MGT).<br>- Pengamatan deteksi Hidden SSID (`<length:  0>`) saat klien melakukan asosiasi. |
| **IV** | 20 Menit | *Istirahat & Pengecekan Data Tangkapan Pemindaian* |
| **V** | 55 Menit | **Tahap 3: Perekaman & Dekonstruksi Paket 4-Way Handshake**<br>- Isolasi penangkapan paket pada satu kanal dan target BSSID lab: `airodump-ng -c <CH> --bssid <MAC> -w lab_handshake wlan0mon`.<br>- Menghubungkan smartphone klien lab untuk memicu proses asosiasi 4-Way Handshake.<br>- Verifikasi kemunculan notifikasi: `[ WPA handshake: XX:XX:XX:XX:XX:XX ]`.<br>- Membuka file `.cap` di Wireshark: Analisis RSN Info pada Beacon, serta bedah field EAPOL Message 1 (ANonce), Message 2 (SNonce + MIC), Message 3 (GTK), dan Message 4 (ACK). |
| **VI** | 30 Menit | **Tahap 4: Uji Pembuktian Mitos Keamanan (MAC Spoofing)**<br>- Identifikasi MAC address smartphone klien resmi yang sedang aktif.<br>- Meniru identitas klien menggunakan perintah `macchanger` pada kartu jaringan penyerang.<br>- Pembuktian bahwa MAC Filtering dapat ditembus dalam hitungan detik.<br>- Pengisian lembar kerja dan verifikasi data oleh dosen/asisten lab. |

---

## 2. K3 & STANDAR OPERASIONAL LABORATORIUM
> [!CAUTION]
> **Kebijakan Etika & Hukum (Ethical Hacking Policy):**
> Aktivitas Monitor Mode dan perekaman paket radio nirkabel pada praktikum ini **HANYA DIIZINKAN** pada Access Point khusus laboratorium TRK Politani. Menangkap traffic atau mencoba memecahkan kata sandi jaringan kampus umum atau pihak ketiga tanpa izin merupakan tindak pidana pelanggaran hukum (UU ITE).

---

## 3. ALAT DAN BAHAN

| No | Komponen | Spesifikasi / Keterangan | Jumlah |
| :---: | :--- | :--- | :---: |
| 1 | Laptop Praktikan | Terinstal OS Kali Linux / Debian dengan software Wireshark & Aircrack-ng | 1 unit/kelompok |
| 2 | USB Wi-Fi Adapter Eksternal | Chipset Atheros AR9271 / Ralink RT3070 / RTL8812AU (Support Monitor Mode) | 1 unit/kelompok |
| 3 | Access Point Lab Khusus | MikroTik hAP mini / TP-Link Router dengan konfigurasi WPA2-PSK | 1 unit/kelompok |
| 4 | Smartphone Klien | Perangkat mobile untuk simulasi koneksi stasiun klien | 1 unit/kelompok |

---

## 4. LANGKAH KERJA STEP-BY-STEP

### Langkah 1: Eksplorasi Mode Interface Nirkabel
1. Pasang USB Wi-Fi adapter ke port USB laptop Anda.
2. Buka Terminal Linux, periksa antarmuka nirkabel bawaan:
   ```bash
   iwconfig
   ```
   *Amati:* Interface (misal: `wlan0`) berada pada `Mode:Managed` (hanya bisa mendengar paket untuk dirinya sendiri).
3. Matikan service background yang berpotensi mengganggu stabilitas monitor mode:
   ```bash
   sudo airmon-ng check kill
   ```
4. Ubah mode kartu nirkabel menjadi mode **Monitor**:
   ```bash
   sudo airmon-ng start wlan0
   ```
5. Periksa kembali nama antarmuka monitor yang terbentuk (biasanya `wlan0mon`):
   ```bash
   iwconfig wlan0mon
   # Pastikan parameter menampilkan: Mode:Monitor
   ```

---

### Langkah 2: Audit Reconnaissance & Pemetaan Spektrum
1. Jalankan pemindaian seluruh gelombang radio di sekitar laboratorium:
   ```bash
   sudo airodump-ng wlan0mon
   ```
2. **Analisis Kolom `airodump-ng`:**
   - **BSSID:** MAC Address perangkat pemancar Access Point.
   - **PWR:** Kekuatan sinyal (RSSI dalam -dBm). Semakin mendekati 0, sinyal semakin kuat.
   - **Beacons:** Jumlah frame pemberitahuan keberadaan AP yang berhasil ditangkap.
   - **#Data:** Jumlah frame data payload yang melintas di udara.
   - **CH:** Kanal frekuensi operasional (1 s/d 14 pada 2.4 GHz).
   - **ENC & CIPHER:** Tipe enkripsi (WEP, WPA, WPA2, WPA3) dan cipher (CCMP, TKIP).
   - **ESSID:** Nama jaringan nirkabel.
3. Catat 3 Access Point terkuat di lingkungan lab Anda ke dalam **Tabel Pengamatan 1**.

---

### Langkah 3: Perekaman 4-Way Handshake pada AP Target Lab
1. Tentukan BSSID dan Kanal AP Lab khusus milik kelompok Anda (misal BSSID: `00:11:22:33:44:55` pada Kanal `6`).
2. Kunci antena monitor hanya pada kanal dan BSSID target tersebut, lalu simpan hasil capture ke file `audit_lab`:
   ```bash
   sudo airodump-ng -c 6 --bssid 00:11:22:33:44:55 -w audit_lab wlan0mon
   ```
3. Hubungkan smartphone praktikan ke SSID AP target lab dengan memasukkan kata sandi yang telah ditentukan.
4. Perhatikan pojok kanan atas layar `airodump-ng`. Tunggu hingga muncul tulisan:
   ```
   [ WPA handshake: 00:11:22:33:44:55 ]
   ```
5. Tekan `Ctrl + C` untuk menghentikan proses perekaman. File berekstensi `.cap` telah tersimpan di direktori kerja Anda.

---

### Langkah 4: Dekonstruksi Kriptografi Paket pada Wireshark
1. Buka file hasil rekaman capture di Wireshark:
   ```bash
   wireshark audit_lab-01.cap &
   ```
2. **Analisis RSN Information pada Beacon Frame:**
   - Masukkan display filter: `wlan.fc.type_subtype == 8`
   - Buka layer **IEEE 802.11 Wireless Management** $\rightarrow$ **Tagged parameters** $\rightarrow$ **RSN Information**.
   - Catat: Versi RSN, Group Cipher Suite (AES/CCMP), dan Pairwise Cipher Suite.
3. **Dekonstruksi 4-Way Handshake (EAPOL):**
   - Hapus filter sebelumnya, ganti dengan display filter: `eapol`
   - Amati 4 frame berurutan:
     - **Message 1 (Frame 1):** Buka *802.1X Authentication* $\rightarrow$ *WPA Key Data*. Temukan field **WPA Key Nonce (ANonce)**. Perhatikan bahwa MIC masih bernilai nol.
     - **Message 2 (Frame 2):** Dikirim oleh stasiun klien. Temukan field **WPA Key Nonce (SNonce)** dan perhatikan field **WPA Key MIC** yang telah terisi tanda tangan hash pembuktian PMK!
     - **Message 3 (Frame 3):** Dikirim oleh AP. Amati field **WPA Key Data** yang berisi kunci GTK terenkripsi.
     - **Message 4 (Frame 4):** Frame konfirmasi penutupan proses handshake (ACK).

---

### Langkah 5: Pembuktian Ketidakefektifan MAC Filtering (MAC Spoofing)
1. Pada `airodump-ng`, periksa bagian bawah (tabel klien) untuk melihat MAC address smartphone resmi yang sedang terhubung ke AP lab (misal: `AA:BB:CC:DD:EE:FF`).
2. Buka terminal baru di Kali Linux, ubah MAC address kartu nirkabel penyerang menjadi sama persis dengan klien resmi tersebut:
   ```bash
   sudo ip link set dev wlan0mon down
   sudo macchanger -m AA:BB:CC:DD:EE:FF wlan0mon
   sudo ip link set dev wlan0mon up
   ```
3. Verifikasi dengan perintah `macchanger -s wlan0mon` bahwa MAC telah berubah.
4. Diskusikan bersama kelompok: Mengapa fitur MAC Filtering router tidak memiliki nilai perlindungan terhadap penyerang yang menggunakan Linux?

---

## 5. LEMBAR DATA PENGAMATAN PRAKTIKAN

### Tabel 1: Hasil Reconnaissance Spektrum Nirkabel di Area Lab

| No | Nama Jaringan (ESSID) | BSSID (MAC AP) | Sinyal (PWR dBm) | Kanal (CH) | Enkripsi (ENC) | Cipher Suite |
| :---: | :--- | :--- | :---: | :---: | :---: | :---: |
| 1 | AP Lab Kelompok | ........................ | ........... dBm | ...... | WPA2 | CCMP |
| 2 | ........................ | ........................ | ........... dBm | ...... | ............ | ............ |
| 3 | ........................ | ........................ | ........... dBm | ...... | ............ | ............ |

---

### Tabel 2: Bedah Komponen Kriptografi 4-Way Handshake di Wireshark

| Nomor Pesan | Arah Pengiriman | Field Kriptografi Kunci yang Dibawa | Fungsi Teknis dalam Pembentukan PTK |
| :---: | :---: | :--- | :--- |
| **Message 1** | AP $\rightarrow$ Klien | Nilai **ANonce**: `........................................` | Memberikan nomor acak AP kepada klien. |
| **Message 2** | Klien $\rightarrow$ AP | Nilai **SNonce**: `........................................`<br>Nilai **MIC**: `................................................` | Mengirim nomor acak klien + membuktikan kepemilikan PMK melalui MIC. |
| **Message 3** | AP $\rightarrow$ Klien | Perintah **Install PTK** + Kunci **GTK** Terenkripsi | Memerintahkan aktivasi kunci unicast dan membagikan kunci multicast. |
| **Message 4** | Klien $\rightarrow$ AP | Nilai **Replay Counter** + Konfirmasi ACK | Mengonfirmasi instalasi kunci selesai, port 802.1X dibuka. |

---

## 6. SISTEMATIKA LAPORAN PRAKTIKUM
Laporan disusun dalam format PDF dengan memuat:
1. **Identitas Kelompok & Resume Tujuan Praktikum**
2. **Screenshot Terminal `airodump-ng` (Reconnaissance Spektrum Nirkabel)**
3. **Screenshot Wireshark:**
   - Bukti pembacaan RSN Information pada Beacon frame.
   - Bukti 4 baris frame EAPOL (Message 1 s/d 4).
   - Detail tampilan field ANonce (Message 1) dan SNonce + MIC (Message 2).
4. **Analisis Teknis Mahasiswa:**
   - Mengapa seorang penyerang yang berhasil merekam frame Message 1 dan Message 2 dapat melakukan pemecahan kata sandi secara *offline* di laptopnya sendiri tanpa perlu menyentuh AP target lagi?
   - Mengapa pergantian mode kartu jaringan dari *Managed* ke *Monitor* menjadi syarat wajib dalam audit keamanan nirkabel?
5. **Kesimpulan Praktikum.**
