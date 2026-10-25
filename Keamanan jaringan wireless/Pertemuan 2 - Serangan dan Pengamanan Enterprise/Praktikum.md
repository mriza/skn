# MODUL PRAKTIKUM: AUDIT KERENTANAN DEAUTENTIKASI & HARDENING WLAN ENTERPRISE
**Mata Kuliah:** Sistem Komunikasi Nirkabel  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Pertemuan:** Minggu X (Pertemuan 2)  
**Alokasi Waktu:** 210 Menit (3 x 70 menit)

---

## 1. ALOKASI WAKTU PRAKTIKUM (TOTAL: 210 MENIT)

| Tahap | Durasi | Deskripsi Aktivitas Praktikan |
| :---: | :---: | :--- |
| **I** | 15 Menit | **Briefing K3, Pembagian Skenario Audit, & Etika Lab**<br>- Penegasan batasan pengujian hanya pada BSSID lab.<br>- Pembagian peran dalam kelompok: Penguji Penetrasi (*Auditor*) vs Administrator Jaringan (*Defender*). |
| **II** | 35 Menit | **Tahap 1: Setup Lingkungan Uji & Verifikasi Koneksi Klien**<br>- Booting Kali Linux dan konfigurasi interface monitor mode.<br>- Koneksi smartphone klien ke Access Point Lab target default (WPA2-PSK tanpa PMF).<br>- Pengujian ping continuous untuk memantau stabilitas koneksi sebelum pengujian serangan. |
| **III** | 45 Menit | **Tahap 2: Simulasi Serangan Deautentikasi & Analisis Dampak**<br>- Pengiriman frame deauth terarah (`aireplay-ng --deauth`) dari MAC AP palsu ke MAC smartphone klien.<br>- Pengamatan reaksi stasiun klien (koneksi terputus dan status reconnect loop).<br>- Perekaman traffic frame deauth pada Wireshark untuk menganalisis header Reason Code (`Reason code: 7 / Class 3 frame received from nonassociated STA`). |
| **IV** | 20 Menit | *Istirahat & Review Data Log Penyerangan* |
| **V** | 60 Menit | **Tahap 3: Implementasi Hardening pada Access Point Lab**<br>- Login ke manajemen router/AP (Winbox RouterOS / WebGUI).<br>- Penerapan **Protected Management Frames (PMF / 802.11w)**: set `management-protection=required`.<br>- Nonaktifkan protokol usang: WEP, WPA1, TKIP, dan fitur **WPS (Wi-Fi Protected Setup)**.<br>- Konfigurasi **Client Isolation** (`default-forwarding=no`) untuk mencegah serangan antar-klien di SSID yang sama.<br>- Konfigurasi Virtual AP dengan segmentasi **VLAN 30 (Guest Network)**. |
| **VI** | 35 Menit | **Tahap 4: Validasi Ulang Pertahanan & Penyusunan Laporan**<br>- Pengulangan injeksi frame deauth terhadap klien yang terhubung ke AP pasca-hardening.<br>- Verifikasi stasiun klien tetap terhubung tanpa terganggu (*Drop attack berhasil dimitigasi*).<br>- Pemeriksaan isolasi klien (uji ping antar dua smartphone klien menghasilkan *Destination Host Unreachable*).<br>- Verifikasi lembar pengamatan oleh dosen/asisten lab. |

---

## 2. K3 & TATA TERTIB LABORATORIUM
> [!CAUTION]
> Injeksi frame deautentikasi radio memancar secara terbuka di udara. Setiap kelompok **HANYA BOLEH** menembakkan paket secara spesifik ke alamat MAC stasiun smartphone kelompoknya sendiri (`-c <MAC_KLIEN_SENDIRI>`). Dilarang keras melakukan broadcast deauth (`-c FF:FF:FF:FF:FF:FF`) yang dapat mengganggu perkuliahan di ruangan lain!

---

## 3. ALAT DAN BAHAN

| No | Komponen | Spesifikasi / Keterangan | Jumlah |
| :---: | :--- | :--- | :---: |
| 1 | Laptop Auditor (Kali Linux) | USB Wi-Fi Adapter chipset Alfa AWUS036NHA / TP-Link WN722N v1 | 1 unit/kelompok |
| 2 | Router Access Point Lab | MikroTik RouterBOARD (hAP mini/hAP ac/RouterOS v7) | 1 unit/kelompok |
| 3 | Perangkat Klien Target | 2 Unit Smartphone (Android/iOS) atau Laptop Klien Uji | 2 unit/kelompok |
| 4 | Kabel Patch UTP Cat6 | Kabel LAN koneksi manajemen router ke laptop teknisi | 1 unit |

---

## 4. TOPOLOGI & SKENARIO PENGUJIAN

```
               +---------------------------------------------+
               |        ACCESS POINT LAB (MIKROTIK)          |
               |  SSID: LAB-TRK-SECURE                       |
               |  Fitur: PMF (802.11w) + Client Isolation ON |
               +----------------------+----------------------+
                                      |
              ((( RF 2.4 GHz )))      |      ((( RF 2.4 GHz )))
                     |                |              |
                     v                |              v
       +----------------------------+ | +----------------------------+
       |   SMARTPHONE KLIEN 1       | | |    SMARTPHONE KLIEN 2      |
       | IP: 192.168.88.10          | | | IP: 192.168.88.11          |
       | (Target Deauth & Isolation)| | | (Uji Client Isolation)     |
       +----------------------------+ | +----------------------------+
                     ^                |
                     | Injeksi Palsu  |
                     | (Deauth Frame) |
       +-------------+--------------+ |
       |     LAPTOP AUDITOR KALI    | |
       | Alfa USB (Monitor Mode)    | |
       +----------------------------+ |
```

---

## 5. LANGKAH KERJA STEP-BY-STEP

### Langkah 1: Persiapan Audit & Koneksi Awal (Baseline)
1. Nyalakan Access Point Lab. Konfigurasi SSID default `LAB-TRK-DEFAULT` dengan security profile `WPA2-PSK`, ciphers `aes ccm`, namun **PMF dalam kondisi disabled**.
2. Sambungkan Smartphone Klien 1 ke SSID tersebut. Pastikan klien mendapat IP (misal `192.168.88.10`).
3. Pada Smartphone 1, jalankan aplikasi Terminal atau Ping tool ke IP gateway `192.168.88.1` secara kontinu. Amati respons latency stabil $1 - 5\text{ ms}$.

### Langkah 2: Simulasi Serangan Deautentikasi (Evaluasi Kerentanan)
1. Pada laptop Kali Linux, aktifkan monitor mode pada interface Wi-Fi:
   ```bash
   sudo airmon-ng start wlan0
   ```
2. Tangkap lalu lintas AP lab:
   ```bash
   sudo airodump-ng -c <CH_LAB> --bssid <BSSID_LAB> wlan0mon
   ```
   *(Temukan MAC address Smartphone Klien 1 pada daftar Station).*
3. Buka terminal kedua, jalankan serangan deautentikasi terarah:
   ```bash
   sudo aireplay-ng --deauth 15 -a <BSSID_AP> -c <MAC_SMARTPHONE_1> wlan0mon
   ```
4. **Amati Layar Smartphone:**
   - Perhatikan aplikasi ping: respons seketika *Request Timed Out* atau *Network Unreachable*.
   - Ikon Wi-Fi di smartphone akan menghilang / putus dan berusaha mencari koneksi ulang.

### Langkah 3: Hardening Access Point pada RouterOS MikroTik
1. Buka aplikasi **Winbox** dan login ke MikroTik AP Lab.
2. Masuk menu `Wireless` -> tab `Security Profiles` -> edit profil keamanan yang digunakan:
   - Tab `General`: Pastikan hanya mencentang `WPA2 PSK` (atau `WPA3 SAE`). Hapus centang pada `WPA PSK`.
   - Pastikan Unicast Ciphers & Group Ciphers hanya memilih `aes ccm`.
   - Buka tab `Management Protection`:
     - Ubah `Management Protection`: dari `disabled` menjadi **`required`** (atau `allowed`).
     - Masukkan `Management Protection Key` (opsional jika menggunakan mode required standar).
3. Masuk tab `WiFi Interfaces` -> buka interface `wlan1`:
   - Buka tab `Wireless`:
     - Nonaktifkan opsi `Default Forwarding` (hapus tanda centang).
       *(Fungsi: Mengaktifkan **Client Isolation** sehingga Klien 1 dan Klien 2 tidak dapat saling memindai atau mengirim paket data).*
     - Nonaktifkan fitur WPS: Buka tab `WPS` -> set `WPS Mode: disabled`.
4. Klik `Apply` dan `OK`.

### Langkah 4: Validasi Ulang Resistensi & Keamanan
1. Hubungkan kembali Smartphone 1 dan Smartphone 2 ke AP yang telah di-hardening.
2. Jalankan kembali ping continuous dari Smartphone 1 ke Gateway AP.
3. Dari terminal Kali Linux auditor, ulangi perintah serangan deautentikasi:
   ```bash
   sudo aireplay-ng --deauth 20 -a <BSSID_AP> -c <MAC_SMARTPHONE_1> wlan0mon
   ```
4. **Amati Hasilnya:**
   - Apakah koneksi Smartphone 1 terputus? *(Klien tetap lancar terhubung dan ping tetap replay tanpa putus berkat proteksi 802.11w)*.
5. **Uji Client Isolation:**
   - Dari Smartphone 1 (`192.168.88.10`), lakukan ping ke Smartphone 2 (`192.168.88.11`).
   - Amati bahwa ping gagal / unreachable, membuktikan sesama pengguna terisolasi dari potensi serangan lokal.

---

## 6. LEMBAR PENGAMATAN MAHASISWA

| Parameter Audit Keamanan | Kondisi Sebelum Hardening | Kondisi Setelah Hardening | Kesimpulan Analisis |
| :--- | :--- | :--- | :--- |
| **Status PMF (802.11w)** | Disabled | Required | Proteksi terhadap pemalsuan frame manajemen |
| **Resistensi Serangan Deauth** | Terputus seketika (Drop) | Tetap terhubung (Kebal) | .................................................... |
| **Ping Antar Sesama Klien** | Berhasil Reply (Rawan) | Drop / Blocked | .................................................... |
| **Status Fitur WPS** | Enabled | Disabled | Mencegah brute force PIN Reaver |

---

## 7. FORMAT SISTEMATIKA LAPORAN PRAKTIKUM
Laporan praktikum disusun dalam format PDF dengan sistematika:
1. **Identitas Kelompok & Resume Tujuan Praktikum**
2. **Topologi Jaringan Lab & Peran Anggota (Auditor vs Defender)**
3. **Screenshot Hasil Pengujian Serangan Deautentikasi (Sebelum Hardening)**
4. **Screenshot Langkah-langkah Konfigurasi Hardening pada Winbox MikroTik (PMF, Client Isolation, WPS Disabled)**
5. **Screenshot Bukti Uji Resistensi Pasca Hardening (Ping tetap stabil saat diserang deauth)**
6. **Kesimpulan:** Rekomendasi teknis penerapan pengamanan Wi-Fi untuk gedung perkuliahan Politeknik Pertanian Negeri.
