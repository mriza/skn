# INSTRUMEN EVALUASI: KUIS & TUGAS KONFIGURASI ANTENA GRID POINT TO POINT
**Mata Kuliah:** Sistem Komunikasi Nirkabel  
**Topik Khusus:** Konfigurasi Radio, Pointing Antena Grid, & Troubleshooting PTP  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Pertemuan:** Minggu XII  
**Pendekatan:** Aplikatif & Praktis (Network Engineer Oriented)

---

## BAGIAN 1: KUIS TEKNIS PTP & POINTING ANTENA GRID (DURASI: 45 MENIT)

### A. Soal Pilihan Ganda (Bobot: 50 Poin / @5 Poin)

1. Dalam topologi Point to Point (PTP) menggunakan MikroTik RouterOS, mode wireless interface yang tepat untuk radio pemancar utama (*Master*) dan radio penerima (*Slave*) agar dapat meneruskan frame Layer 2 transparan ke switch jaringan adalah:
   - A. `station` dan `station-pseudobridge`
   - B. `ap-bridge` dan `station-bridge`
   - C. `alignment-only` dan `nstreme-dual-slave`
   - D. `wds-slave` dan `station-wds`

2. Apa yang menjadi penyebab utama link outdoor jarak jauh (misal jarak 10 km) mengalami pengiriman ulang paket terus-menerus (*retransmit storm*) dan throughput lambat jika parameter radio dibiarkan default indoor?
   - A. Kabel LAN UTP otomatis putus akibat arus petir.
   - B. Parameter `Distance / ACK Timeout` belum disesuaikan dengan jarak riil sehingga radio buru-buru menganggap paket hilang sebelum konfirmasi sempat tiba.
   - C. Antena grid tidak mampu menangkap gelombang yang berjarak lebih dari 1 km.
   - D. Frekuensi 5 GHz otomatis disadap oleh satelit cuaca.

3. Untuk mengatasi masalah *Hidden Node* dan menghilangkan tabrakan paket data di udara pada link outdoor jarak jauh, protokol proprietary berbasis **TDMA (Time Division Multiple Access)** yang digunakan pada perangkat MikroTik adalah:
   - A. OSPF
   - B. NV2 (Nstreme version 2)
   - C. Spanning Tree Protocol (STP)
   - D. BGP

4. Nilai level daya sinyal terima (Signal Strength / RSSI) yang dianggap paling ideal dan optimal untuk link nirkabel outdoor Point to Point agar tidak terjadi *overdrive* maupun sinyal *drop* adalah:
   - A. $-20\text{ dBm s/d } -30\text{ dBm}$
   - B. $-50\text{ dBm s/d } -65\text{ dBm}$
   - C. $-85\text{ dBm s/d } -95\text{ dBm}$
   - D. $+10\text{ dBm s/d } +20\text{ dBm}$

5. Fenomena teknisi mengunci arah antena pada pancaran daun samping (*Side Lobe*) yang menghasilkan sinyal semu lebih lemah daripada pancaran berkas utama (*Main Lobe*) dikenal dengan istilah:
   - A. Multipath Fading
   - B. Side Lobe Trap
   - C. Thermal Noise
   - D. Doppler Shift

6. Parameter pada RouterOS MikroTik yang menunjukkan persentase paket data yang berhasil dikirimkan dan diterima dengan baik tanpa memerlukan pengiriman ulang (*retransmit*) adalah:
   - A. Modulation Coding Scheme (MCS)
   - B. Client Connection Quality (CCQ)
   - C. Noise Floor
   - D. Frequency Offset

7. Mengapa pemilihan lebar kanal (*Channel Width*) $20\text{ MHz}$ sering kali lebih direkomendasikan pada link PTP jarak jauh dibandingkan menggunakan $40\text{ MHz}$ atau $80\text{ MHz}$ pada area dengan banyak interferensi?
   - A. Karena $20\text{ MHz}$ memiliki noise floor lebih rendah ($3\text{ dB}$ lebih hening) sehingga memberikan SNR dan sensitivitas yang lebih tinggi.
   - B. Karena kanal $20\text{ MHz}$ tidak memerlukan antena grid.
   - C. Karena kanal $40\text{ MHz}$ dilarang secara mutlak oleh undang-undang di seluruh dunia.
   - D. Karena antena grid hanya dapat beresonansi pada frekuensi $20\text{ MHz}$.

8. Cara mengubah polarisasi pada antena grid dari Vertikal menjadi Horizontal adalah:
   - A. Mengganti radio outdoor dengan merk lain.
   - B. Memutar modul stik feed horn sebesar $90^\circ$ saat perakitan baut mekanis.
   - C. Mengubah konfigurasi IP address dari statik menjadi DHCP.
   - D. Memperpanjang kabel pigtail RF.

9. Jika noise floor pada suatu lokasi menara terukur sebesar $-98\text{ dBm}$ dan sinyal terima (RSSI) terukur $-68\text{ dBm}$, berapakah nilai **Signal-to-Noise Ratio (SNR)** dari link tersebut?
   - A. $-166\text{ dB}$
   - B. $30\text{ dB}$
   - C. $68\text{ dB}$
   - D. $98\text{ dB}$

10. Langkah pertama yang paling krusial sebelum melakukan prosedur pointing antena di atas menara adalah:
    - A. Memutar antena secara acak secepat mungkin.
    - B. Menentukan arah sudut perkiraan kasar menggunakan kompas bidik / GPS dan memastikan Line of Sight (LOS) visual bebas halangan.
    - C. Mengganti kata sandi router setiap 5 menit.
    - D. Menurunkan daya pemancar (*Tx Power*) menjadi 0 dBm.

---

### B. Soal Studi Kasus Troubleshooting Lapangan (Bobot: 50 Poin / @25 Poin)

**Kasus 1 (Diagnostik Link Fluktuatif & Tiang Goyang):**  
Sebuah link Point to Point Antena Grid 5.8 GHz berjarak 8 km yang menghubungkan Gedung Rektorat Politani dengan Kampus B dilaporkan mengalami gangguan:
- Pada siang hari yang cerah, sinyal berada pada $-60\text{ dBm}$ dan throughput mencapai 60 Mbps stabil.
- Namun saat terjadi angin kencang atau hujan gerimis, sinyal anjlok ke $-82\text{ dBm}$, nilai CCQ drop dari $98\%$ menjadi $40\%$, dan sering terjadi *link disconnected*.
- Teknisi memeriksa tiang antena dan mendapati tiang pipa galvanis bergoyang cukup kuat saat terpaan angin.

*Pertanyaan:*
1. Mengapa tiang yang bergoyang akibat angin dapat menyebabkan sinyal antena grid anjlok drastis padahal antena tidak rusak? Kaitkan dengan karakteristik *beamwidth* antena grid!
2. Rekomendasikan 3 tindakan teknis terperinci di lapangan untuk mengatasi masalah tersebut agar link kembali stabil permanen!

**Kasus 2 (Analisis Throughput Rendah & Interferensi Spektrum):**  
Dua radio outdoor dikonfigurasi pada mode `ap-bridge` dan `station-bridge` dengan lebar kanal $40\text{ MHz}$. Hasil pembacaan status pada Winbox menunjukkan:
- Signal Strength: $-58\text{ dBm}$ (Sangat kuat)
- Noise Floor: $-82\text{ dBm}$ (Tinggi / kotor)
- SNR: $24\text{ dB}$
- Tx/Rx CCQ: $45\% / 50\%$
- Bandwidth Test TCP hanya menghasilkan throughput 4 Mbps padahal kapasitas link teoritis $150\text{ Mbps}$.

*Pertanyaan:*
1. Mengapa nilai sinyal yang kuat ($-58\text{ dBm}$) tetap menghasilkan throughput sangat kecil dan nilai CCQ yang buruk?
2. Berikan langkah-langkah optimasi step-by-step pada konfigurasi radio (frekuensi kanal, channel width, protokol TDMA) untuk mendongkrak performa throughput link tersebut!

---

## BAGIAN 2: TUGAS TERSTRUKTUR (PROPOSAL PERENCANAAN LINK PTP 5 KM KAMPUS POLITANI)

### Judul Tugas:
**"Perencanaan Teknis & Desain Implementasi Link Wireless Point to Point 5 KM Menggunakan Antena Grid untuk Interkoneksi Jaringan Politani"**

### Ketentuan Tugas:
1. Sifat: Tugas Berkelompok (2 Mahasiswa).
2. Waktu Pengerjaan: 1 Minggu setelah praktikum lapangan.
3. Luaran: Dokumen Proposal Teknis (PDF, 6 - 8 Halaman).

### Struktur Isi Dokumen Proposal:
1. **Peta Topografi & Profil Jalur (airLink / ISP Design Center):**
   - Gunakan software planner gratis (Ubiquiti ISP Design Center / airLink) untuk menentukan koordinat Titik A (Kampus Utama) dan Titik B (Lokasi Praktik).
   - Lampirkan screenshot grafik profil kontur tanah dan garis bebas halangan (*Fresnel clearance*).
2. **Ketinggian Tiang/Menara yang Dibutuhkan:**
   - Tentukan tinggi tower di kedua sisi berdasarkan simulasi agar berkas tidak terpotong tajuk pohon sawit atau bukit.
3. **Bill of Materials (BOM) & Perangkat yang Dipilih:**
   - Rekomendasi tipe antena grid (Gain dBi), model radio outdoor (RouterBOARD / Bullet), tipe kabel LAN outdoor FTP Cat5e/6, grounding penangkal petir, dan power supply PoE.
4. **SOP Prosedur Instalasi & Pointing di Lapangan:**
   - Panduan praktis perakitan antena, pengaturan polarisasi, dan tahapan fine-pointing mencari nilai RSSI $-50\text{ s/d } -65\text{ dBm}$.

---

## BAGIAN 3: KUNCI JAWABAN KUIS & PEMBAHASAN KASUS

### Kunci Jawaban Pilihan Ganda:
1. **B** | 2. **B** | 3. **B** | 4. **B** | 5. **B** | 6. **B** | 7. **A** | 8. **B** | 9. **B** ($SNR = -68 - (-98) = 30\text{ dB}$) | 10. **B**

### Pembahasan Kasus Lapangan:

**Kasus 1:**
1. *Akar Masalah:* Antena grid dengan gain tinggi memiliki sudut pancar (*beamwidth*) yang sangat sempit ($4^\circ - 6^\circ$). Ketika tiang bergoyang ditiup angin, arah berkas utama (*main lobe*) bergeser keluar dari fokus sasaran, menyebabkan sinyal drop drastis ke arah *side lobe* atau redaman luar berkas. Nilai CCQ drop karena stasiun harus mengirim ulang paket data berkali-kali.
2. *Rekomendasi:*
   - Pasang kawat seling penarik (*guyed wire*) minimal 3 atau 4 arah pada tiang dengan span turnbuckle pengencang untuk mengunci goyangan angin.
   - Ganti tiang pipa lentur dengan pipa galvanis tebal $\ge 2\text{ inch}$ atau tiang menara triangle.
   - Lakukan pointing ulang dan kencangkan baut U-bolt menggunakan mur ganda (*double nut*) dan ring per (*spring washer*) agar tidak mudah kendor akibat getaran.

**Kasus 2:**
1. *Penyebab:* Terjadi interferensi frekuensi radio yang sangat parah (*high RF noise*) di sekitar lokasi, dibuktikan oleh Noise Floor yang sangat tinggi ($-82\text{ dBm}$). Kanal lebar $40\text{ MHz}$ menangkap spektrum yang terlalu luas sehingga rentan terpapar polusi frekuensi tetangga, mengakibatkan tabrakan paket tinggi dan CCQ anjlok ke $< 50\%$.
2. *Solusi Optimasi:*
   - Buka menu `Wireless` -> `Snooper` atau `Frequency Usage` untuk memindai kanal frekuensi yang paling bersih dari interferensi AP lain.
   - Turunkan lebar pita kanal (*Channel Width*) dari $40\text{ MHz}$ ke $20\text{ MHz}$. Ini akan menurunkan noise floor sebesar $3\text{ dB}$ dan meningkatkan nilai SNR serta stabilitas link secara drastis.
   - Aktifkan protokol TDMA proprietary (ganti `Wireless Protocol` menjadi **`nv2`** pada MikroTik) untuk mengeliminasi tabrakan paket data di udara.
