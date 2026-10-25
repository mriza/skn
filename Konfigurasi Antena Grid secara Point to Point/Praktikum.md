# MODUL PRAKTIKUM: PERAKITAN, KONFIGURASI RADIO, & POINTING ANTENA GRID POINT TO POINT
**Mata Kuliah:** Sistem Komunikasi Nirkabel  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Alokasi Waktu:** 210 Menit (3 x 70 menit)

---

## 1. ALOKASI WAKTU PRAKTIKUM (TOTAL: 210 MENIT)

| Tahap | Durasi | Deskripsi Aktivitas Praktikan |
| :---: | :---: | :--- |
| **I** | 15 Menit | **Briefing K3 Lapangan & Prosedur Praktikum Tower/PTP**<br>- Keselamatan kerja mekanik: Kunci pas, obeng, baut U-bolt, handling pigtail RF.<br>- Pembagian 2 tim kerja per stasiun: **Tim Stasiun A (Master / AP)** dan **Tim Stasiun B (Slave / Station)**. |
| **II** | 45 Menit | **Tahap 1: Perakitan Fisik Antena Grid & Feed Horn**<br>- Pemasangan rangka reflektor kisi aluminium (*mesh reflector*).<br>- Pemasangan bracket sub-reflector & feed horn pada titik fokus parabola.<br>- Penyelarasan orientasi polarisasi (kedua tim wajib sepakat: **Polarisasi Vertikal** atau **Horizontal**).<br>- Pemasangan bracket U-Bolt ke pipa rigging tiang penyangga. |
| **III** | 40 Menit | **Tahap 2: Pengkabelan PoE & Konfigurasi Parameter Radio di Lab**<br>- Koneksi jumper pigtail N-Male ke RP-SMA dengan benar.<br>- Pengkabelan kabel UTP outdoor ke port PoE radio dan adaptor 24V.<br>- Konfigurasi software (RouterOS / AirOS): Mode `ap-bridge` pada Stasiun A dan `station-bridge` pada Stasiun B.<br>- Konfigurasi SSID khusus, frekuensi kanal, lebar pita (20 MHz), dan keamanan (WPA2-AES). |
| **IV** | 20 Menit | *Istirahat & Mobilisasi Tim ke Posisi Uji Outdoor* |
| **V** | 55 Menit | **Tahap 3: Prosedur Pointing Antena & Penyelarasan Sudut Sinyal**<br>- Penggunaan kompas/inclinometer untuk penentuan azimuth kasar.<br>- Sweeping horizontal (Azimuth) bertahap $1^\circ - 2^\circ$ secara bergantian antara Stasiun A dan B.<br>- Sweeping vertikal (Elevasi) untuk optimasi puncak sinyal (*Main Lobe*).<br>- Penguncian baut bracket secara simetris saat sinyal mencapai nilai optimal ($-50\text{ s/d } -65\text{ dBm}$). |
| **VI** | 35 Menit | **Tahap 4: Pengujian Throughput, Latency, & Analisis Stabilitas Link**<br>- Uji Ping test (100 paket ICMP: latency rata-rata & jitter).<br>- Uji Bandwidth Test (BTest TCP & UDP: Tx/Rx Throughput).<br>- Pencatatan data metrik (RSSI, CCQ, SNR, Noise Floor) ke lembar kerja.<br>- Pembongkaran alat (*teardown*) dan evaluasi instruktur. |

---

## 2. K3 & KESELAMATAN KERJA INSTALASI OUTDOOR
> [!CAUTION]
> 1. Gunakan sarung tangan kerja mekanik saat merakit reflektor kisi aluminium untuk menghindari luka akibat tepi logam kisi.
> 2. Pastikan baut U-Bolt pada tiang dikencangkan secara merata kiri dan kanan; pengencangan yang tidak seimbang dapat merusak drat baut atau pipa tiang penyangga.
> 3. Jangan pernah menghubungkan kabel LAN ke port PoE saat adaptor listrik telah tercolok untuk menghindari lonjakan arus (*arcing*). Pasang kabel LAN terlebih dahulu, baru nyalakan adaptor ke stopkontak PLN.

---

## 3. ALAT DAN BAHAN (PER KELOMPOK KERJA)

| No | Komponen | Spesifikasi / Keterangan | Jumlah |
| :---: | :--- | :--- | :---: |
| 1 | Antena Grid 2.4 GHz / 5 GHz | Reflektor Parabola Kisi Aluminium + Feed Horn Gain 24 - 27 dBi | 2 Set (Stasiun A & B) |
| 2 | Radio Wireless Outdoor | MikroTik Groove 52HPn / BaseBox atau Ubiquiti Bullet / Rocket | 2 Unit |
| 3 | Pipa Tiang Rigging Mini | Pipa besi/galvanis $\phi\ 1.5 - 2\text{ inch}$ panjang 1.5 - 2 meter + Tripod | 2 Unit |
| 4 | Kabel UTP Outdoor STP/FTP | Cat5e shielded dengan konektor RJ-45 metal grounding | 2 Roll (@ 10 meter) |
| 5 | Passive PoE Injector & Adaptor | 24V DC 0.8A / 1A | 2 Set |
| 6 | Kunci Pas / Kunci Ring | Ukuran 10 mm, 12 mm, dan 14 mm | 2 Set |
| 7 | Laptop Teknisi | Dilengkapi software Winbox (MikroTik) / Web Browser | 2 Unit |
| 8 | Kompas Bidik / GPS App | Penentu arah azimuth koordinat stasiun lawan | 1 Unit |

---

## 4. TOPOLOGI & DIAGRAM PENGKABELAN

```
[ STASIUN A: MASTER (AP-BRIDGE) ]                       [ STASIUN B: SLAVE (STATION-BRIDGE) ]
  Laptop A (192.168.88.2/24)                              Laptop B (192.168.88.3/24)
         |                                                       |
   (LAN Port)                                              (LAN Port)
         v                                                       v
  [ PoE Injector ]                                        [ PoE Injector ]
    [LAN]  [PoE]                                            [LAN]  [PoE]
             | (Kabel UTP Outdoor)                                   | (Kabel UTP Outdoor)
             v                                                       v
     [ Radio MikroTik A ]                                    [ Radio MikroTik B ]
     IP: 192.168.88.1/24                                     IP: 192.168.88.254/24
     Mode: AP-Bridge                                         Mode: Station-Bridge
             | (Pigtail RF N-Male)                                   | (Pigtail RF N-Male)
             v                                                       v
      [ ANTENA GRID A ]           ((( POINT TO POINT )))      [ ANTENA GRID B ]
      Polarisasi: Vertikal     ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~    Polarisasi: Vertikal
```

---

## 5. LANGKAH KERJA STEP-BY-STEP

### Langkah 1: Perakitan Fisik Antena Grid
1. Pasang dua belahan reflektor kisi aluminium (*grid*) menjadi satu kesatuan menggunakan baut pengunci tengah.
2. Pasang bracket penyangga *feed horn* pada lubang pusat reflektor.
3. Pasang sub-reflector *feed horn*.
   > [!IMPORTANT]
   > **Perhatian Polarisasi:** Perhatikan orientasi elemen di dalam *feed horn*. Jika dipasang sejajar dengan kisi-kisi vertikal, antena berada dalam **Polarisasi Vertikal**. Pastikan kedua antena (Stasiun A dan Stasiun B) dirakit dengan orientasi polarisasi yang persis sama!
4. Pasang bracket U-Bolt di bagian belakang kisi antena, lalu kencangkan pada pipa tiang penyangga.

### Langkah 2: Pengkabelan & Setting Radio Wireless
1. Hubungkan port RF radio outdoor ke konektor N-Type antena menggunakan kabel jumper/pigtail low-loss.
2. Hubungkan kabel UTP outdoor dari port radio ke port **PoE** pada adaptor PoE injector.
3. Hubungkan port **LAN** pada PoE injector ke port ethernet laptop teknisi.
4. Buka aplikasi **Winbox** (untuk MikroTik):
   - **Konfigurasi Stasiun A (Master / AP):**
     1. Masuk menu `Wireless` -> tab `Security Profiles` -> buat profil baru dengan mode `WPA2-PSK`, unicast/group ciphers `aes ccm`, masukkan kata sandi (misal: `PTP-Grid-TRK2026`).
     2. Masuk tab `WiFi Interfaces` -> buka interface `wlan1`.
     3. Set parameter berikut:
        - `Mode`: **ap bridge**
        - `Band`: **5GHz-A/N** (atau 2GHz-B/G/N)
        - `Channel Width`: **20MHz**
        - `Frequency`: Pilih frekuensi yang bersih (misal: **5200 MHz** atau kanal 6 pada 2.4 GHz)
        - `SSID`: **PTP-POLITANI-LINK**
        - `Wireless Protocol`: **any** atau **nv2**
        - `Security Profile`: pilih profil yang baru dibuat.
     4. Masuk menu `IP` -> `Addresses` -> tambahkan IP: `192.168.88.1/24` pada interface `bridge1` (atau `wlan1`).

   - **Konfigurasi Stasiun B (Slave / Client):**
     1. Buat `Security Profile` yang identik dengan Stasiun A.
     2. Buka interface `wlan1`:
        - `Mode`: **station bridge**
        - `Band`: Identik dengan Stasiun A
        - `Channel Width`: **20MHz**
        - `SSID`: **PTP-POLITANI-LINK**
        - `Security Profile`: profil WPA2 yang identik.
     3. Masuk menu `IP` -> `Addresses` -> tambahkan IP: `192.168.88.254/24`.

### Langkah 3: Prosedur Pointing Antena Grid (Penyelarasan Sinyal)
1. Aktifkan fitur *Alignment Beeper* atau buka jendela `Status` pada antarmuka wireless di kedua laptop teknisi.
2. Gunakan kompas bidik untuk mengarahkan kedua antena saling berhadapan secara visual.
3. **Penyelarasan Azimuth (Horizontal):**
   - Kunci antena Stasiun B dalam posisi diam.
   - Longgarkan sedikit baut U-bolt Stasiun A. Putar antena Stasiun A perlahan ke kiri dan ke kanan dalam rentang gerak $1^\circ - 2^\circ$.
   - Amati grafik sinyal pada Winbox Stasiun B (`Signal Strength`). Cari titik puncaknya (sinyal paling mendekati angka $0\text{ dBm}$, misal naik dari $-78\text{ dBm}$ ke $-58\text{ dBm}$).
   - Kencangkan baut horizontal Stasiun A sementara.
   - Sekarang gantian putar horizontal antena Stasiun B untuk menyempurnakan sinyal.
4. **Penyelarasan Elevasi (Vertikal):**
   - Kendurkan baut pengatur kemiringan (*tilt*). Naikkan atau turunkan sudut antena Stasiun A dan B hingga didapatkan nilai RSSI terbaik.
5. **Kunci Seluruh Baut:**
   - Kencangkan seluruh mur dan baut secara diagonal bergantian agar arah antena tidak bergeser saat dikunci kencang.

### Langkah 4: Pengujian & Stress Test Performa Link
1. Periksa parameter link pada menu `Wireless` -> `Registration` di Winbox:
   - Catat: **Signal Strength**, **Tx/Rx Signal Strength Ch0**, **Signal to Noise (SNR)**, **Tx/Rx CCQ**, dan **Tx/Rx Rate**.
2. **Uji Latency (Ping Test):**
   - Buka Terminal di Laptop A:
     ```bash
     ping 192.168.88.254 -c 100
     ```
   - Catat nilai *Packet Loss*, *Minimum*, *Average*, dan *Maximum Latency*.
3. **Uji Throughput (Bandwidth Test):**
   - Pada Winbox, buka menu `Tools` -> `Bandwidth Test`.
   - Masukkan IP target `192.168.88.254`.
   - Pilih protokol `UDP`, arah `both` (send & receive). Jalankan selama 30 detik.
   - Ulangi untuk protokol `TCP`.
   - Catat throughput stabil yang dicapai.

---

## 6. LEMBAR KERJA EVALUASI PRAKTIKAN

### Tabel 1: Log Metrik Sinyal Sebelum & Sesudah Pointing Halus

| Parameter Kualitas Link | Nilai Awal (Pointing Kasar) | Nilai Akhir (Setelah Optimasi) | Keterangan Standar Kelayakan |
| :--- | :---: | :---: | :--- |
| **Signal Strength (RSSI)** | ............... dBm | ............... dBm | Target: $-50\text{ s/d } -65\text{ dBm}$ |
| **Noise Floor** | ............... dBm | ............... dBm | Typical: $-95\text{ s/d } -105\text{ dBm}$ |
| **Signal to Noise (SNR)** | ............... dB | ............... dB | Syarat Minimal: $\ge 25 - 30\text{ dB}$ |
| **Tx / Rx CCQ** | ......... / ......... % | ......... / ......... % | Target Stabil: $> 90 - 100\%$ |
| **Terkoneksi pada Data Rate (MCS)** | .................... | .................... | Contoh: MCS 7 (65/72.2 Mbps) |

### Tabel 2: Hasil Pengujian Throughput & Latency

| Parameter Pengujian | Protokol UDP | Protokol TCP | Analisis Perbedaan Kinerja |
| :--- | :---: | :---: | :--- |
| **Tx Throughput (Upload)** | ............ Mbps | ............ Mbps | .................................................... |
| **Rx Throughput (Download)** | ............ Mbps | ............ Mbps | .................................................... |
| **Rata-rata Ping Latency** | ............ ms | ............ ms | .................................................... |
| **Packet Loss (%)** | ............ % | ............ % | .................................................... |

---

## 7. FORMAT SISTEMATIKA LAPORAN PRAKTIKUM
Laporan disusun oleh masing-masing pasangan tim kerja (Stasiun A & B) dengan sistematika:
1. **Identitas Anggota Tim (Stasiun A & B) & Tanggal Pengujian**
2. **Spesifikasi Hardware (Model Antena Grid, Model Radio, Frekuensi Kerja, Polarisasi)**
3. **Screenshot Konfigurasi Winbox:**
   - Halaman wireless interface Stasiun A & B.
   - Halaman status registration table (RSSI, CCQ, MCS).
4. **Data Tabel 1 dan Tabel 2 yang telah terisi lengkap.**
5. **Analisis Masalah:**
   - Jelaskan kendala saat proses pointing (apakah sempat terjebak pada *Side Lobe*?).
   - Analisis perbedaan throughput antara pengujian UDP vs TCP.
6. **Kesimpulan & Rekomendasi Instalasi Tower PTP di Lapangan.**
