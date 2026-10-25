# INSTRUMEN EVALUASI: KUIS & TUGAS MATERI ANTENA WIRELESS
**Mata Kuliah:** Sistem Komunikasi Nirkabel  
**Topik Khusus:** Pemilihan Antena, Karakteristik Beam, & Sinyal Lapangan  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Pertemuan:** Minggu XI  
**Pendekatan:** Aplikatif & Praktis (Network Engineer Oriented)

---

## BAGIAN 1: KUIS PRAKTIS PEMILIHAN & ANALISIS ANTENA (DURASI: 45 MENIT)

### A. Soal Pilihan Ganda (Bobot: 50 Poin / @5 Poin)

1. Anda diminta memasang hotspot Wi-Fi di tengah-tengah ruang perpustakaan kampus Politani agar mahasiswa dari segala sudut ruangan dapat terhubung dengan stabil. Jenis antena yang paling tepat digunakan adalah:
   - A. Antena Parabola Grid
   - B. Antena Omnidirectional
   - C. Antena Yagi-Uda
   - D. Antena Sectoral $60^\circ$

2. Seorang teknisi ingin menghubungkan jaringan internet dari Gedung TRK ke Asrama Mahasiswa yang berjarak 4 kilometer secara Point-to-Point (PTP). Jenis antena yang paling direkomendasikan adalah:
   - A. Antena Rubber Duck 2 dBi
   - B. Antena Parabola Grid (Gain 24 dBi)
   - C. Antena Biquad kaleng
   - D. Antena Omni outdoor 8 dBi

3. Mengapa antena dengan nilai Gain (dBi) yang sangat besar membutuhkan bidikan (*pointing*) yang jauh lebih teliti dan presisi dibandingkan antena dengan Gain kecil?
   - A. Karena antena Gain besar otomatis mengubah frekuensi.
   - B. Karena semakin besar nilai Gain, sudut berkas pancarannya (*beamwidth*) menjadi semakin sempit dan runcing.
   - C. Karena antena Gain besar memerlukan arus listrik PLN langsung.
   - D. Karena antena Gain besar menghasilkan panas tinggi.

4. Sebuah Base Station WISP di pedesaan menggunakan 3 buah antena Sectoral untuk membagi area pancaran ke seluruh pelanggan di sekitarnya. Berapakah lebar sudut horizontal (*azimuth beamwidth*) yang ideal untuk masing-masing antena tersebut agar dapat menutup sudut $360^\circ$ secara merata?
   - A. $10^\circ$
   - B. $45^\circ$
   - C. $120^\circ$
   - D. $360^\circ$

5. Pengguna yang berdiri tepat di bawah menara Base Station (jarak 10 meter dari kaki tower) mengeluhkan sinyal Wi-Fi di ponselnya sangat lemah atau hilang sama sekali (*dead zone*), padahal antena di atas tower menyala normal. Penyebab utama fenomena ini adalah:
   - A. Antena sectoral rusak tersambar petir.
   - B. Sudut vertikal (*elevation beamwidth*) antena sangat tipis sehingga berkas sinyal memancar lurus ke kejauhan di atas kepala pengguna.
   - C. Smartphone tidak kompatibel dengan kabel fiber optik tower.
   - D. Frekuensi Wi-Fi terserap oleh tanah.

6. Solusi mekanis yang tepat untuk mengatasi masalah "dead zone" pada soal nomor 5 di atas adalah:
   - A. Mengganti seluruh kabel UTP dengan kabel coaxial.
   - B. Melakukan *Downtilt* (memiringkan moncong antena sedikit menunduk ke bawah) agar berkas sinyal mengenai area sekitar tower.
   - C. Menambah daya radio pemancar hingga 100 Watt.
   - D. Mengecat tiang menara dengan warna merah.

7. Mengapa antena Grid parabola didesain dalam bentuk kisi-kisi/jaring aluminium berlubang, bukan pelat solid utuh seperti wajan penggorengan?
   - A. Agar bobotnya lebih ringan dan terpaan angin kencang di atas menara dapat lolos menembus kisi-kisi (*low wind load*).
   - B. Agar harga tembaga lebih murah.
   - C. Agar air hujan bisa tertampung di dalam kisi.
   - D. Agar sinyal nirkabel dapat disaring menjadi lebih jernih.

8. Sebuah radio outdoor memiliki daya pancar $P_{Tx} = 20\text{ dBm}$ ($100\text{ mW}$), dihubungkan ke antena Patch dengan Gain $14\text{ dBi}$ menggunakan kabel jumper dengan redaman $1\text{ dB}$. Berapakah nilai **EIRP** pemancar tersebut?
   - A. $7\text{ dBm}$
   - B. $20\text{ dBm}$
   - C. $33\text{ dBm}$
   - D. $35\text{ dBm}$

9. Pada datasheet antena directional, spesifikasi **Front-to-Back (F/B) Ratio** sebesar $28\text{ dB}$ memiliki arti praktis:
   - A. Antena memerlukan waktu 28 detik untuk booting.
   - B. Pancaran daya ke arah depan lebih kuat $28\text{ dB}$ dibandingkan kebocoran sinyal ke arah belakangnya sendiri, sehingga aman dari interferensi perangkat lain di tiang yang sama.
   - C. Antena dapat menampung maksimal 28 klien.
   - D. Antena dapat berputar $28^\circ$ secara otomatis.

10. Indikator sinyal pada router MikroTik di sisi penerima menunjukkan angka RSSI sebesar **$-86\text{ dBm}$**. Sebagai engineer jaringan, tindakan apa yang harus Anda simpulkan?
    - A. Sinyal sangat bagus dan kecepatan internet akan maksimal.
    - B. Sinyal terlalu lemah (kritis), berisiko tinggi putus-nyambung (*drop*), dan perlu dilakukan pointing ulang atau penggantian antena yang memiliki gain lebih besar.
    - C. Router mengalami konsleting listrik.
    - D. Frekuensi radio harus diubah ke 50 GHz.

---

### B. Soal Studi Kasus Lapangan Network Engineer (Bobot: 50 Poin / @25 Poin)

**Kasus 1 (Pemilihan Perangkat & Desain Jaringan Nirkabel Kampus):**  
Pihak pengelola kampus Politeknik Pertanian Negeri memberikan proyek interkoneksi jaringan kepada tim TRK untuk 2 kebutuhan berikut:
1. **Lokasi A:** Area kafe/taman terbuka mahasiswa di depan rektorat (luas $40 \times 40\text{ meter}$) dengan target 80 pengguna smartphone yang tersebar di sekeliling taman.
2. **Lokasi B:** Interkoneksi internet dari Gedung Server Utama ke Laboratorium Kandang Ternak Terpadu yang berjarak $1.5\text{ kilometer}$ melintasi area perkebunan sawit.

*Pertanyaan:*
- Untuk **Lokasi A**, jenis antena apa yang Anda rekomendasikan dan mengapa?
- Untuk **Lokasi B**, jenis antena apa yang Anda pilih? Mengapa Anda tidak boleh menggunakan antena Omni untuk kebutuhan Lokasi B?
- Jelaskan faktor halangan (pohon sawit) terhadap syarat *Line of Sight (LOS)* pada Lokasi B!

**Kasus 2 (Troubleshooting Sinyal & Interferensi Antar Antena):**  
Seorang teknisi WISP memasang 2 unit antena directional di satu tiang pipa yang sama. Antena 1 menghadap ke arah Barat, sedangkan Antena 2 dipasang membelakangi Antena 1 menghadap ke arah Timur. Setelah dipasang, kedua sambungan internet sering mengalami kelambatan parah (*packet loss tinggi* dan throughput anjlok) setiap kali kedua antena aktif bersamaan.  
*Pertanyaan:*
1. Mengapa kedua antena tersebut dapat saling mengganggu padahal arah bidikannya berlawanan arah ($180^\circ$)? Kaitkan penjelasan Anda dengan parameter **Front-to-Back (F/B) Ratio** dan kebocoran *Back Lobe*!
2. Berikan 2 solusi praktis di lapangan untuk mengatasi masalah interferensi tersebut tanpa harus merobohkan tiang menara!

---

## BAGIAN 2: TUGAS TERSTRUKTUR (PANDUAN PEMILIHAN ANTENA DAN BILL OF MATERIALS)

### Judul Tugas:
**"Perancangan Rekomendasi Pemilihan Antena & Aksesoris RF untuk Infrastruktur Jaringan Nirkabel Politani"**

### Ketentuan Tugas:
1. Sifat: Tugas Kelompok (2 Mahasiswa).
2. Waktu Pengumpulan: 1 Minggu ke depan.
3. Luaran: Dokumen Rekomendasi Teknis (PDF, 4 - 6 Halaman).

### Isi Laporan:
1. **Pencarian Datasheet Produk:**
   - Cari 3 produk antena komersial di toko daring / website resmi vendor (MikroTik, Ubiquiti, atau TP-Link Pharos) untuk kategori: 1 Antena Omni, 1 Antena Panel/CPE, dan 1 Antena Grid/Dish.
2. **Tabel Ringkasan Spesifikasi Lapangan:**
   - Masukkan ke dalam tabel: Model perangkat, Frekuensi, Gain (dBi), Sudut Horizontal & Vertikal, Jenis Konektor, dan Perkiraan Harga.
3. **Justifikasi Penerapan di Kampus:**
   - Jelaskan skenario penempatan yang paling tepat untuk masing-masing antena di lingkungan Politeknik Pertanian Negeri (misal: di gedung jurusan, hotspot kantin, atau link ke kebun).

---

## BAGIAN 3: KUNCI JAWABAN KUIS & PEMBAHASAN KASUS

### Kunci Jawaban Pilihan Ganda:
1. **B** | 2. **B** | 3. **B** | 4. **C** | 5. **B** | 6. **B** | 7. **A** | 8. **C** ($20 - 1 + 14 = 33\text{ dBm}$) | 9. **B** | 10. **B**

### Pembahasan Kasus Lapangan:

**Kasus 1:**
- **Lokasi A:** Menggunakan antena **Omnidirectional** (atau AP Outdoor Omni). Alasan: Pengguna berada menyebar $360^\circ$ di sekeliling taman dalam jarak dekat ($< 50\text{ meter}$).
- **Lokasi B:** Menggunakan antena **Directional (Grid atau High-Gain Panel)**. Alasan: Jarak $1.5\text{ km}$ membutuhkan pemusatan berkas energi yang sempit agar sinyal sampai dengan kuat. Antena Omni tidak boleh digunakan karena energinya terbuang menyebar ke arah lain sehingga sinyal di titik tujuan akan sangat lemah di bawah batas sensitivitas ($< -85\text{ dBm}$).
- **Faktor Halangan Sawit:** Pohon sawit menyerap dan menghamburkan gelombang radio (terutama 2.4/5 GHz yang mudah teredam molekul air daun). Oleh karena itu, tower di kedua sisi harus cukup tinggi agar berkas Line of Sight dan area Zona Fresnel bebas dari puncak tajuk pohon sawit.

**Kasus 2:**
1. *Penyebab:* Antena memiliki pancaran bocoran ke arah belakang (*Back Lobe*). Jika antena yang digunakan memiliki nilai F/B ratio yang rendah ($< 20\text{ dB}$), sinyal dari Antena 1 akan bocor ke belakang dan langsung masuk ke mulut antena 2 di tiang yang sama, memicu *self-interference / co-channel interference*.
2. *Solusi Praktis:*
   - Beri jarak pemisahan fisik secara vertikal pada tiang (geser antena 1 lebih ke atas minimal $1 - 1.5\text{ meter}$ dari antena 2).
   - Pastikan kedua radio bekerja pada **kanal frekuensi yang berbeda dan tidak saling bertumpukan** (*non-overlapping channel*), misal Antena 1 di 5180 MHz dan Antena 2 di 5745 MHz.
   - Pasang perisai pelindung logam samping/belakang (*RF Armor / Shielding kit*) untuk meredam kebocoran back lobe.
