# MATERI KULIAH: TEKNOLOGI LINK POINT TO POINT & ANTENA GRID
**Mata Kuliah:** Sistem Komunikasi Nirkabel (3 SKS)  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Pertemuan:** Minggu XII  
**Alokasi Waktu:** 210 Menit (3 x 70 menit)  
**Pendekatan:** Aplikatif & Praktis (Network Engineer / Systems Deployment)

---

## RUNDOWN & RENCANA WAKTU PEMBELAJARAN (TOTAL: 210 MENIT)

| Sesi | Waktu | Aktivitas Pembelajaran | Fokus Praktisi / Engineer |
| :--- | :---: | :--- | :--- |
| **Sesi 1** | 00:00 - 00:35 (35m) | **Konsep Dasar Link Point to Point (PTP) Jarak Jauh**<br>- Fungsi PTP sebagai tulang punggung (*wireless backhaul*) antar-gedung/kampus.<br>- Perbedaan PTP (titik-ke-titik) vs PTMP (titik-ke-banyak stasiun).<br>- Syarat kelayakan jalur nirkabel: Visual Line of Sight (LOS) dan bebas halangan pohon/gedung (*Fresnel clearance*). | Pemahaman topologi jaringan transmisi nirkabel tanpa teori propagasi rumit. |
| **Sesi 2** | 00:35 - 01:25 (50m) | **Anatomi & Karakteristik Fisik Antena Grid**<br>- Mengapa memilih antena grid di tower? (Kisi-kisi aluminium meloloskan terpaan angin / *low wind load*).<br>- Elemen reflektor kisi parabola, tiang penyangga, dan *feed horn* (titik fokus).<br>- Cara praktis menentukan polarisasi antena grid: Cukup memutar posisi *feed horn* $90^\circ$ (Vertikal vs Horizontal). | Panduan mekanis perakitan dan penanganan antena di menara/tiang. |
| **Sesi 3** | 01:25 - 01:45 (20m) | *Istirahat & Tanya Jawab Sesi Pertama* | Diskusi kendala teknis instalasi tiang dan kabel outdoor. |
| **Sesi 4** | 01:45 - 02:35 (50m) | **Konfigurasi Radio Outdoor & Penyesuaian Parameter Jarak Jauh**<br>- Mode Operasi: `ap-bridge` (Pemancar Master) vs `station-bridge` (Penerima Client transparan Layer 2).<br>- Mengapa Wi-Fi rumahan lambat di outdoor? Masalah *Hidden Node* dan pentingnya setting parameter **`Distance / ACK Timeout`** pada RouterOS.<br>- Protokol TDMA Khusus Outdoor: MikroTik **NV2** vs Ubiquiti **airMAX** (meniadakan tabrakan paket data di udara).<br>- Memilih Channel Width: $20\text{ MHz}$ (stabil dan tahan gangguan noise) vs $40\text{ MHz}$ (kecepatan tinggi pada frekuensi bersih). | Panduan konfigurasi Winbox RouterOS / AirOS yang biasa dihadapi teknisi. |
| **Sesi 5** | 02:35 - 03:10 (35m) | **Prosedur Pointing Sistematis & Indikator Kualitas Link**<br>- Tahapan sweeping arah: Mengatur Azimuth (kiri-kanan) dan Elevasi (atas-bawah) bertahap $1^\circ - 2^\circ$.<br>- Menghindari jebakan daun samping (**Side Lobe Trap**): Mengapa sinyal semu bisa menipu teknisi pemula.<br>- Membaca indikator status di Winbox: Target RSSI ($-50\text{ s/d } -65\text{ dBm}$), Noise Floor, SNR ($> 25\text{ dB}$), dan CCQ ($> 90\%$). | Simulasi troubleshooting link sinyal drop atau throughput rendah. |
| **Sesi 6** | 03:10 - 03:30 (20m) | **Kesimpulan, Rangkuman, & Pengarahan Praktikum Lapangan** | Review SOP keselamatan kerja menara (K3), briefing pembagian tim stasiun A & B. |

---

## 1. PENDAHULUAN: TOPOLOGI POINT TO POINT (PTP) UNTUK NETWORK ENGINEER

```
[ GEDUNG REKTORAT / SERVER ]                               [ KAMPUS CABANG / KEBUN PERCOBAAN ]
+--------------------------+                               +--------------------------+
| Switch Core / Gateway    |                               | Switch Distribusi LAN    |
+-------------+------------+                               +-------------+------------+
              | (Kabel LAN PoE)                                           | (Kabel LAN PoE)
+-------------v------------+                               +-------------v------------+
| Radio Master (AP-Bridge) |                               | Radio Slave (Station)    |
|   (MikroTik / Bullet)    |                               |   (MikroTik / Bullet)    |
+-------------+------------+                               +-------------+------------+
              | (Jumper RF)                                               | (Jumper RF)
     +========v========+       ((( BERKAS NARROW BEAM )))         +========v========+
     |   ANTENA GRID   | ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~|   ANTENA GRID   |
     | (Pengarah Sinyal)                 Jarak: 2 - 15 KM         | (Pengarah Sinyal)|
     +=================+                                          +=================+
```

### 1.1 Fungsi PTP di Dunia Kerja
Bagi seorang engineer komputer/jaringan, sambungan Point to Point (PTP) adalah **kabel virtual transparan di udara** pengganti penarikan kabel fiber optik yang mahal:
- Menghubungkan dua lokasi gedung terpisah (misal Kampus Pusat Politani ke Kebun Praktik) tanpa biaya langganan bulanan provider pihak ketiga.
- Mengalirkan seluruh segmen VLAN, IP subnet, dan akses internet secara langsung (*Layer 2 Bridge*).

---

## 2. ANATOMI & KARAKTERISTIK FISIK ANTENA GRID

```
          /|=================================|\
         / |         Reflektor Kisi          | \
        /  |          (Aluminium Grid)       |  \
       |   |                                 |   |
       |   |             [ Feed Horn ]       |   |  <--- Titik Fokus Parabola
       |   |           (Stik Pencatu Daya    |   |       (Putar 90° ubah Polarisasi V/H)
        \  |            ke Kabel Radio)      |  /
         \ |                                 | /
          \|=================================|/
                           |  |
                 [ Bracket U-Bolt Mounting ]  <--- Pengatur Sudut Arah (Azimuth & Elevasi)
                           |  |
                      [ Tiang / Mast ]
```

### 2.1 Keunggulan Desain Antena Grid di Lapangan:
1. **Lolos Terpaan Angin Kencang (*Low Wind Load*):**
   Di atas menara tower setinggi 20 - 40 meter, hembusan angin sangat kuat. Jika menggunakan piringan solid utuh (*solid dish*), tiang tower rawan terpuntir dan arah bidikan meleset. Rangka jaring kisi (*mesh grid*) meloloskan terpaan angin hingga $80\%$, menjaga arah bidikan tetap stabil.
2. **Fokus Berkas Sangat Sempit (*Narrow Pencil Beam*):**
   Sudut pancaran hanya sekitar $4^\circ - 8^\circ$. Seluruh energi dipadatkan lurus ke depan, menjamin sinyal tetap kuat sampai di seberang dan kebal dari polusi interferensi AP tetangga di samping.
3. **Kemudahan Mengubah Polarisasi:**
   Teknisi cukup memutar modul *feed horn* sebesar $90^\circ$ pada saat perakitan baut untuk memilih **Polarisasi Vertikal** atau **Polarisasi Horizontal**.

---

## 3. PENGATURAN PARAMETER RADIO WIRELESS OUTDOOR

### 3.1 Mode Wireless pada RouterOS (MikroTik):
- **Sisi Master (Pemancar):** Diset ke mode **`ap-bridge`** (berfungsi sebagai pemancar utama penyedia SSID dan pengatur kanal frekuensi).
- **Sisi Slave (Penerima):** Diset ke mode **`station-bridge`** (mode khusus MikroTik yang memungkinkan transfer paket data Layer 2 transparan sehingga IP klien di seberang langsung terhubung ke switch server).

### 3.2 Menghindari Retransmit Storm: Setting Parameter "Distance"
- Standar Wi-Fi rumahan berasumsi jarak perangkat hanya beberapa meter di dalam ruangan (*ACK Timeout default $25\ \mu\text{s}$*).
- Pada jarak outdoor $10\text{ km}$, gelombang membutuhkan waktu lebih lama untuk merambat bolak-balik di udara.
- **Trik Praktisi:** Pada RouterOS MikroTik (menu `Wireless` -> tab `Advanced`), ubah parameter **`Distance`** dari *indoors/dynamic* menjadi angka jarak riil lapangan (misal ketik **`10`** untuk jarak 10 km). Radio akan otomatis memperpanjang batas waktu tunggu konfirmasi paket (ACK), mencegah terjadinya pengiriman ulang paket terus-menerus (*retransmit storm*) yang membuat koneksi lemot.

### 3.3 Mengapa Menggunakan Protokol TDMA (MikroTik NV2 / Ubiquiti airMAX)?
Protokol bawaan Wi-Fi (CSMA/CA) sering gagal di link outdoor karena radio tidak bisa saling mendengar sinyal radio lain di kejauhan (*Hidden Node Problem*):
- **Protokol TDMA (Time Division Multiple Access):**
  - Radio AP membagi jadwal transmisi data menjadi petak-petak waktu berulang (*time slots*).
  - Masing-masing radio hanya mentransmisikan data pada gilirannya sendiri.
  - Hasil: Tidak ada paket data yang saling bertabrakan di udara (*zero collision*), throughput naik hingga $2 - 3\times$ lipat dan latency ping menjadi sangat stabil.

### 3.4 Pemilihan Lebar Pita (Channel Width)
- **$20\text{ MHz}$ (Rekomendasi Standar):** Spektrum sempit, noise floor rendah, sangat stabil, tahan gangguan interferensi di area perkotaan/kampus.
- **$40\text{ MHz}$:** Menghasilkan throughput lebih besar ($> 150\text{ Mbps}$), namun hanya disarankan jika kondisi spektrum nirkabel di sekitar lokasi bersih dari pemancar liar.

---

## 4. METODOLOGI POINTING ANTENA & MENGHINDARI JEBAKAN SIDE LOBE

```
               Pola Sebaran Sinyal Antena Grid (Tampak Atas)
                        Side Lobe     Main Lobe (-55 dBm)   Side Lobe
                          (-75 dBm)         / \            (-75 dBm)
                             _             /   \             _
                            / \           /     \           / \
             --------------/---\---------/-------\---------/---\------------
             -90 dBm       |   |        |    *    |        |   |
                                        | (TARGET)|
                                       Bidikan Tepat
```

> [!CAUTION]
> **Jebakan Daun Samping (Side Lobe Trap):**
> Antena grid memiliki satu berkas pancar utama yang sangat tajam (*Main Lobe*) yang diapit oleh daun samping (*Side Lobe*). Saat memutar antena, teknisi pemula sering buru-buru mengunci baut ketika sinyal pertama kali terdeteksi (misal $-75\text{ dBm}$), padahal yang terkunci adalah **Side Lobe**.
> **SOP Teknisi:** Terus putar antena perlahan melintasi titik sinyal drop (*null*) hingga menemukan puncak sinyal tertinggi sejati (*Main Lobe*, misal naik ke $-55\text{ dBm}$).

### Standar Checklist Kelayakan Link Nirkabel PTP:
1. **Signal Strength (RSSI):** Target ideal antara **$-50\text{ s/d } -65\text{ dBm}$**. (Jika lebih kuat dari $-45\text{ dBm}$, turunkan Tx Power radio agar tidak *overdrive*; jika lebih lemah dari $-75\text{ dBm}$, perbaiki bidikan pointing).
2. **Noise Floor:** Berkisar antara **$-95\text{ s/d } -105\text{ dBm}$**.
3. **Signal to Noise Ratio (SNR):** Selisih sinyal di atas noise minimal **$> 25\text{ dB}$**.
4. **Client Connection Quality (CCQ):** Persentase keutuhan paket data pada RouterOS harus stabil di atas **$> 90 - 100\%$**.
