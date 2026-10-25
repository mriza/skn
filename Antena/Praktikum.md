# MODUL PRAKTIKUM: IDENTIFIKASI ANTENA, PENGUKURAN SEBARAN SINYAL, & SIMULASI LINK BUDGET
**Mata Kuliah:** Sistem Komunikasi Nirkabel  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Pertemuan:** Minggu XI  
**Alokasi Waktu:** 210 Menit (3 x 70 menit)  
**Pendekatan:** Aplikatif & Praktis (Network Engineer Oriented)

---

## 1. ALOKASI WAKTU PRAKTIKUM (TOTAL: 210 MENIT)

| Tahap | Durasi | Deskripsi Aktivitas Praktikan |
| :---: | :---: | :--- |
| **I** | 15 Menit | **Briefing K3 & Standar Kerja Praktisi Nirkabel**<br>- Penanganan fisik antena, kabel pigtail, dan konektor RF (N-Type, RP-SMA).<br>- Aturan keselamatan kerja listrik outdoor & grounding tiang penangkal petir. |
| **II** | 45 Menit | **Eksperimen 1: Bedah Fisik & Membaca Datasheet Antena Komersial**<br>- Pengamatan langsung bentuk fisik antena: Omni (Stick), Panel (Kotak), Sectoral (Panjang), dan Grid (Jaring).<br>- Latihan membaca spesifikasi penting di datasheet vendor (Gain dBi, HPBW Azimuth/Elevasi, Polarisasi, F/B ratio, Connector type, Wind survivability). |
| **III** | 50 Menit | **Eksperimen 2: Uji Sebaran Sinyal (Coverage Mapping) Omni vs Directional**<br>- Menyalakan AP pemancar dengan antena Omni, lalu mengukur level sinyal (RSSI dalam -dBm) di 4 sisi ruangan (Depan, Kanan, Kiri, Belakang).<br>- Mengganti antena AP dengan tipe Directional (Patch Panel), lalu mengulang pengukuran di titik yang sama.<br>- Menganalisis perbedaan sebaran sinyal dan konsep pengarahan energi. |
| **IV** | 20 Menit | *Istirahat & Review Data Pengukuran Lapangan* |
| **V** | 50 Menit | **Eksperimen 3: Simulasi Desain Link Jarak Jauh (Kalkulator Online)**<br>- Menggunakan software perencana wireless online (Ubiquiti airLink / ISP Design Center).<br>- Simulasi pemasangan link interkoneksi Kampus Politani ke Kebun Percobaan (jarak 2 - 5 km).<br>- Menentukan tinggi tower yang diperlukan agar bebas halangan (*Fresnel clearance*), memilih jenis antena yang cocok, dan melihat estimasi kapasitas throughput yang didapat. |
| **VI** | 30 Menit | **Pembersihan Alat, Analisis Diskusi, & Pengisian Lembar Kerja**<br>- Penyusunan rekomendasi antena untuk studi kasus nyata di kampus.<br>- Pengesahan data oleh instruktur/dosen pengampu. |

---

## 2. K3 & STANDAR KESELAMATAN KERJA ENGINEER
> [!WARNING]
> 1. Jangan menyalakan radio pemancar dalam kondisi port antena terbuka tanpa beban karena dapat merusak power amplifier RF.
> 2. Jangan memelintir atau menekuk kabel koaksial RF (pigtail) hingga patah (*kinking*), karena redaman kabel akan melonjak drastis.
> 3. Kencangkan konektor RP-SMA cukup dengan kekuatan jari tangan (*finger tight*).

---

## 3. ALAT DAN BAHAN

| No | Komponen | Spesifikasi / Keterangan | Jumlah |
| :---: | :--- | :--- | :---: |
| 1 | Antena Omnidirectional | 2.4 GHz Rubber Duck 5 dBi / Omni Outdoor | 1 unit/kelompok |
| 2 | Antena Patch / Panel | 2.4 GHz Gain 12 - 14 dBi | 1 unit/kelompok |
| 3 | Antena Grid (Fisik) | Antena Parabola Grid 2.4 GHz / 5 GHz (untuk demonstrasi bentuk) | 1 unit lab |
| 4 | Radio Access Point Uji | MikroTik hAP mini / TP-Link Router dengan antena lepas-pasang (*detachable*) | 1 unit/kelompok |
| 5 | Laptop / Smartphone Tester | Terinstal aplikasi Wi-Fi Analyzer / InSSIDer / NetSpot | 1 unit/kelompok |
| 6 | Akses Internet | Untuk membuka software web planner (Ubiquiti airLink / UI ISP Design Center) | 1 unit/kelompok |

---

## 4. LANGKAH KERJA STEP-BY-STEP

### Eksperimen 1: Membaca Datasheet Antena Komersial
1. Buka lembar spesifikasi (*datasheet*) antena komersial yang dibagikan dosen (misal: *Ubiquiti airMAX Sector 2G15-120* dan *MikroTik mANT 19s*).
2. Temukan dan catat parameter-parameter berikut ke **Tabel 1**:
   - **Frekuensi Operasional:** (misal $2.3 - 2.7\text{ GHz}$)
   - **Gain:** (misal $15\text{ dBi}$)
   - **HPBW Horizontal (Azimuth):** (misal $120^\circ$)
   - **HPBW Vertikal (Elevasi):** (misal $8^\circ$)
   - **Front-to-Back Ratio:** (misal $28\text{ dB}$)
   - **Tipe Konektor:** (misal RP-SMA Female atau N-Type)
   - **Ketahanan Terpaan Angin (*Wind Survivability*):** (misal $200\text{ km/jam}$)

### Eksperimen 2: Menguji Perbedaan Sebaran Sinyal Omni vs Panel
1. Pasang antena **Omnidirectional (5 dBi)** pada Access Point lab. Letakkan AP di tengah ruangan/lapangan.
2. Bawa smartphone tester dengan aplikasi **Wi-Fi Analyzer** aktif ke 4 titik uji berjarak konstan $10\text{ meter}$ dari AP:
   - **Titik 1 (Depan):** Catat RSSI (-dBm).
   - **Titik 2 (Kanan):** Catat RSSI (-dBm).
   - **Titik 3 (Kiri):** Catat RSSI (-dBm).
   - **Titik 4 (Belakang):** Catat RSSI (-dBm).
3. Matikan AP. Ganti antena dengan tipe **Directional (Patch Panel)** yang dihadapkan ke arah Depan (Titik 1).
4. Nyalakan AP kembali. Tanpa mengubah jarak, ukur ulang RSSI di ke-4 titik yang sama.
5. Catat data hasil perbandingan ke **Tabel 2**. Amati bagaimana antena Directional melipatgandakan sinyal di depan namun melemah di samping dan belakang!

### Eksperimen 3: Simulasi Desain Link Jarak Jauh (Web Tool airLink)
1. Buka browser di laptop, akses: `https://ispdesign.ui.com/` (atau tool kalkulator wireless serupa).
2. Tentukan Titik A: **Gedung TRK Politani** dan Titik B: **Kebun Percobaan / Kampus B** (pilih jarak sekitar $2 - 4\text{ km}$).
3. Pilih perangkat antena:
   - Coba pasang antena Omnidirectional di kedua sisi. Amati apakah link terhubung? *(Hasil: Merah/Gagal karena gain omni terlalu kecil)*.
   - Ganti dengan antena Directional Parabola Grid / Dish. Amati perubahan indikator link!
4. Perhatikan parameter yang ditampilkan:
   - **Fresnel Zone Clearance:** Apakah garis hijau terpotong kontur bukit/pohon?
   - **Tinggi Tower:** Berapa meter tiang yang disarankan sistem agar link bebas halangan?
   - **Estimasi Signal Strength:** Berapa dBm sinyal yang diprediksi?
   - **Throughput:** Berapa kapasitas Mbps riil yang didapatkan?
5. Ambil screenshot hasil simulasi untuk dilampirkan pada laporan.

---

## 5. LEMBAR DATA PENGAMATAN MAHASISWA

### Tabel 1: Analisis Spesifikasi Teknis Antena pada Datasheet

| Parameter Kunci | Antena 1 (Omni Stick) | Antena 2 (Patch Panel) | Antena 3 (Sectoral BTS) | Antena 4 (Grid Parabola) |
| :--- | :--- | :--- | :--- | :--- |
| **Gain Nominal (dBi)** | ........................ | ........................ | ........................ | ........................ |
| **Lebar Sudut Horizontal** | ........................ | ........................ | ........................ | ........................ |
| **Lebar Sudut Vertikal** | ........................ | ........................ | ........................ | ........................ |
| **F/B Ratio (dB)** | (N/A) | ........................ | ........................ | ........................ |
| **Tipe Konektor RF** | ........................ | ........................ | ........................ | ........................ |
| **Rekomendasi Penempatan**| ........................ | ........................ | ........................ | ........................ |

### Tabel 2: Uji Perbandingan Sebaran Sinyal di Lapangan (Jarak 10 Meter)

| Titik Pengujian | Sinyal Antena Omni (-dBm) | Sinyal Antena Panel (-dBm) | Selisih Perbedaan (dB) | Analisis Praktis Engineer |
| :--- | :---: | :---: | :---: | :--- |
| **Titik 1 (Depan)** | ............... dBm | ............... dBm | + ......... dB | Fokus energi ke arah target |
| **Titik 2 (Kanan $90^\circ$)** | ............... dBm | ............... dBm | - ......... dB | Redaman samping |
| **Titik 3 (Kiri $270^\circ$)** | ............... dBm | ............... dBm | - ......... dB | Redaman samping |
| **Titik 4 (Belakang $180^\circ$)** | ............... dBm | ............... dBm | - ......... dB | Efek perlindungan back lobe |

---

## 6. FORMAT LAPORAN PRAKTIKUM
Laporan disusun ringkas dalam format PDF:
1. **Identitas Kelompok & Resume Tujuan Praktikum**
2. **Data Hasil Tabel 1 dan Tabel 2 yang telah terisi lengkap.**
3. **Screenshot Hasil Simulasi Web Planner (airLink) interkoneksi jarak jauh.**
4. **Studi Kasus Singkat:** Jika Anda diminta memasang Wi-Fi di area kantin terbuka vs menghubungkan kantor rektorat ke gedung bengkel mesin terpisah 800 meter, antena apa yang Anda pilih untuk masing-masing lokasi? Jelaskan alasannya secara singkat!
