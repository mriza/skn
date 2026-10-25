# MATERI KULIAH: PANDUAN PRAKTIS ANTENA WIRELESS UNTUK NETWORK ENGINEER
**Mata Kuliah:** Sistem Komunikasi Nirkabel (3 SKS)  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Pertemuan:** Minggu XI  
**Alokasi Waktu:** 210 Menit (3 x 70 menit)  
**Pendekatan:** Aplikatif & Praktis (Applied Computer/Network Engineering)

---

## RUNDOWN & RENCANA WAKTU PEMBELAJARAN (TOTAL: 210 MENIT)

| Sesi | Waktu | Aktivitas Pembelajaran | Fokus Praktisi / Engineer |
| :--- | :---: | :--- | :--- |
| **Sesi 1** | 00:00 - 00:35 (35m) | **Pengantar Antena: Analogi & Prinsip Kerja Praktis**<br>- Mengapa engineer jaringan butuh memahami antena?<br>- Konsep dasar: Antena sebagai "pengarah energi", bukan "penghasil energi" (Analogi Balon Air & Lampu Senter vs Bohlam).<br>- Memahami satuan desibel praktis: dB, dBm (daya), dBi, dan dBd (gain). | Pemahaman intuitif konsep penguatan sinyal tanpa rumus fisika rumit. |
| **Sesi 2** | 00:35 - 01:25 (50m) | **Jenis & Bentuk Fisik Antena di Dunia Industri Jaringan**<br>- **Omnidirectional (Stick/Rubber Duck):** Jangkauan melingkar $360^\circ$ untuk hotspot ruangan/kafe.<br>- **Directional Patch/Panel (Kotak Datar):** Untuk klien outdoor (CPE) atau lorong gedung.<br>- **Sectoral (Persegi Panjang Tegak):** Untuk Base Station (BTS WISP / RT-RW Net).<br>- **Parabolic Grid / Dish (Jaring Kisi Cekung):** Untuk link Point to Point jarak jauh (tahan terpaan angin).<br>- **Yagi-Uda (Tulang Ikan):** Untuk penembak sinyal jarak menengah. | Membedah bentuk fisik, konektor RF (SMA, RP-SMA, N-Type), dan peruntukan skenario riil di lapangan. |
| **Sesi 3** | 01:25 - 01:45 (20m) | *Istirahat & Diskusi Interaktif Sesi 1* | Tanya jawab pemilihan antena di lapangan. |
| **Sesi 4** | 01:45 - 02:30 (45m) | **Memahami Karakteristik Beam (Sudut Pancar) Tanpa Rumus Rumit**<br>- **Beamwidth (Sudut Berkas):** Sudut Horizontal (Azimuth) vs Sudut Vertikal (Elevasi).<br>- Trade-off: Makin besar Gain (dBi) $\rightarrow$ Sudut Berkas makin sempit $\rightarrow$ Butuh bidikan lebih presisi.<br>- Bentuk Berkas: *Donut* (Omni), *Fan/Kipas* (Sectoral), dan *Pencil/Sorot* (Grid).<br>- Mengapa ada *Blind Spot* di bawah tower? Solusi: *Downtilt* (Kemiringan Antena). | Analisis grafik sudut pancar pada datasheet komersial (MikroTik, Ubiquiti, TP-Link). |
| **Sesi 5** | 02:30 - 03:10 (40m) | **Power Distribution, Sinyal Terima, & Regulasi**<br>- Daya Pemancar ($P_{Tx}$ dalam dBm/mW) vs Gain Antena (dBi).<br>- **EIRP (Aturan Kominfo):** Menghitung total daya pancar legal ($EIRP = P_{Tx} - \text{Kabel} + Gain$).<br>- **Front-to-Back (F/B) Ratio Praktis:** Mengapa antena tidak boleh "bocor sinyal ke belakang" saat dipasang berjejer di satu tower.<br>- Metrik Lapangan: RSSI target ($-50\text{ s/d } -65\text{ dBm}$), Noise Floor, SNR, dan Throughput riil. | Praktik membaca datasheet vendor dan kalkulasi link budget praktis (rule of thumb). |
| **Sesi 6** | 03:10 - 03:30 (20m) | **Rangkuman, Studi Kasus Singkat, & Pengantar Praktikum** | Review ringkas, tips memilih antena belanja perangkat, briefing lab. |

---

## 1. PENDAHULUAN: MEMAHAMI ANTENA SECARA INTUITIF

Bagi seorang **Network Engineer / Teknisi Komputer**, antena bukanlah persamaan gelombang elektromagnetik Maxwell, melainkan **komponen pasif pengarah sinyal** yang menentukan:
1. Seberapa jauh jangkauan jaringan nirkabel kita.
2. Ke arah mana saja pengguna dapat menangkap sinyal Wi-Fi.
3. Seberapa tahan jaringan terhadap interferensi dari tetangga.

### 1.1 Analogi "Balon Karet Berisi Air"
Bayangkan Anda memiliki sebuah balon karet bulat berisi air dengan volume tetap (volume air mengibaratkan **daya pemancar radio / Transmit Power**):

```
       ANTENA OMNIDIRECTIONAL (Gain Rendah)            ANTENA DIRECTIONAL (Gain Tinggi)
             (Balon Bulat Mengembang)                     (Balon Ditekan/Dilonjongkan)

                       ^                                               ^
                       |                                               |
                  +---------+                                          | (Jangkauan Jauh)
             <--- |  RADIO  | --->                                     |
                  +---------+                                     +---------+
                       |                                          |  RADIO  | ===>
                       v                                          +---------+
            Jangkauan Menyebar Rata $360^\circ$                    Fokus Kuat ke Satu Arah,
               (Dekat ke Semua Sisi)                             Sisi Lain Menjadi Sangat Tipis
```

- **Antena tidak menambah daya listrik!** Antena hanya memampatkan dan memfokuskan energi ke arah tertentu.
- Jika energi difokuskan ke satu arah sempit (Directional), jangkauannya menjadi sangat jauh.
- Jika energi disebar ke segala arah (Omnidirectional), jangkauannya menjadi lebih pendek di setiap sisi.

### 1.2 Memahami Satuan Praktis di Lapangan
- **dBm (Daya Nyata):** Menyatakan kekuatan daya pemancar radio.
  - $0\text{ dBm} = 1\text{ mW}$
  - $20\text{ dBm} = 100\text{ mW}$ (Daya standar Access Point rumahan / laptop)
  - $27\text{ dBm} = 500\text{ mW}$ (Daya radio outdoor komersial)
  - $30\text{ dBm} = 1000\text{ mW} = 1\text{ Watt}$
- **dBi (Gain Antena):** Nilai penguatan fokus antena dibandingkan antena isotropis (bola teoritis).
  - Gain makin tinggi = Berkas makin sempit dan tajam.
  - Tambahan $+3\text{ dB}$ artinya melipatgandakan kekuatan sinyal $2\times$ lipat.

---

## 2. PANDUAN MEMILIH BENTUK & JENIS ANTENA (ENGINEER FIELD GUIDE)

Berikut adalah panduan praktis memilih jenis antena berdasarkan kebutuhan nyata di lapangan:

```
+---------------------------------------------------------------------------------------------------------+
|                                    PANDUAN PEMILIHAN ANTENA LAPANGAN                                    |
+-------------------+----------------------+--------------------+------------------+----------------------+
| Jenis Antena      | Bentuk Fisik         | Sudut Pancar       | Jangkauan        | Skenario Penggunaan  |
+-------------------+----------------------+--------------------+------------------+----------------------+
| 1. OMNI           | Batang lurus / stick | $360^\circ$        | Pendek - Sedang  | Hotspot kafe, kantor,|
|                   | silinder vertikal    | Horizontal         | (100 m - 1 km)   | ruang kelas, taman.  |
+-------------------+----------------------+--------------------+------------------+----------------------+
| 2. PATCH / PANEL  | Kotak persegi tipis  | Sedang             | Sedang           | Klien outdoor (CPE), |
|                   | datar (flat panel)   | ($30^\circ-60^\circ$)| (500 m - 3 km) | lorong hotel/gedung. |
+-------------------+----------------------+--------------------+------------------+----------------------+
| 3. SECTORAL       | Persegi panjang      | Melebar horizontal | Sedang - Jauh    | Base Station (BTS)   |
|                   | tegak memanjang      | ($60^\circ-120^\circ$)| (1 km - 10 km)| WISP / RT-RW Net.    |
+-------------------+----------------------+--------------------+------------------+----------------------+
| 4. GRID           | Rangka cekung kisi-  | Sangat sempit      | Jauh - Sangat    | Link PTP antar-gedung|
|                   | kisi aluminium       | ($4^\circ - 9^\circ$)| Jauh (5 - 30 km)| atau menara tower.   |
+-------------------+----------------------+--------------------+------------------+----------------------+
| 5. YAGI-UDA       | Rangka pipa dengan   | Cukup sempit       | Menengah         | Penembak sinyal jarak|
|                   | sirip sirip melintang| ($25^\circ-40^\circ$)| (1 km - 5 km)  | menengah / pedesaan. |
+-------------------+----------------------+--------------------+------------------+----------------------+
```

### 2.1 Bedah Karakteristik Antena:

#### A. Antena Omnidirectional
- **Bentuk:** Tongkat silinder putih/hitam (Rubber Duck indoor atau fiberglass outdoor).
- **Karakteristik:** Memancar ke segala arah secara horizontal ($360^\circ$). Pola pancarannya menyerupai kue donat.
- **Kelebihan:** Klien dari arah manapun bisa terhubung tanpa perlu mengarahkan antena.
- **Kekurangan:** Jangkauan terbatas, sangat mudah menangkap interferensi dari segala arah.

#### B. Antena Patch / Flat Panel
- **Bentuk:** Kotak plastik pipih tertutup.
- **Karakteristik:** Menembakkan sinyal ke satu arah depan dengan sudut berkas sedang ($30^\circ - 60^\circ$).
- **Kelebihan:** Kompak, rapi dipasang di dinding, tahan cuaca, estetis untuk gedung perkantoran.
- **Penggunaan:** Sering dijadikan antena stasiun klien (*Client Premises Equipment - CPE*) yang dipasang di atap rumah pelanggan menghadap ke tower WISP.

#### C. Antena Sectoral
- **Bentuk:** Kotak memanjang vertikal (tinggi $60\text{ cm} - 1.5\text{ meter}$).
- **Karakteristik:** Dirancang memancarkan sinyal melebar secara mendatar (*fan beam*, biasanya pilihan sudut $60^\circ, 90^\circ\text{, atau } 120^\circ$), namun sangat tipis secara vertikal ($4^\circ - 8^\circ$).
- **Kelebihan:** Ideal untuk membagi area menara menjadi 3 atau 4 sektor (*Base Station*) agar kapasitas bandwidth lebih besar dan tidak saling tumpang tindih.

#### D. Antena Parabola Grid
- **Bentuk:** Cekungan kisi-kisi kawat aluminium dengan stik pencatu (*feed horn*) di tengahnya.
- **Karakteristik:** Sudut berkas sangat sempit (*pencil beam*, sekitar $4^\circ - 9^\circ$), memusatkan seluruh daya ke satu target.
- **Mengapa berbentuk kisi/jaring?** Agar angin kencang di atas menara dapat berhembus menembus kisi-kisi tanpa mengguncang atau merobohkan tiang menara (*low wind load*).

---

## 3. KARAKTERISTIK BEAM (SUDUT PANCAR) UNTUK PRAKTISI

Saat engineer membuka lembar spesifikasi (*datasheet*) antena komersial, parameter berkas pancaran yang dicari adalah **HPBW (Half-Power Beamwidth)**:

```
                            SUDUT PANCAR BEAMWIDTH (-3 dB)
                                       0° (Puncak)
                                        /\
                                       /  \  <--- Sudut HPBW (-3 dB)
                                      /    \      Area jangkauan efektif sinyal
                                     /      \
                                    /________\
```

### 3.1 Sudut Horizontal vs Sudut Vertikal
Setiap antena memiliki 2 sudut berkas:
1. **Horizontal Beamwidth (H-Plane / Azimuth):** Lebar sebaran sinyal ke kiri dan ke kanan.
2. **Vertical Beamwidth (E-Plane / Elevasi):** Lebar sebaran sinyal ke atas dan ke bawah.

> [!TIP]
> **Aturan Emas Pemilihan Antena:**
> - Makin **besar dBi** antena $\rightarrow$ Sudut berkasnya makin **sempit/tipis**.
> - Antena Grid 24 dBi memiliki sudut hanya $\sim 6^\circ$. Meleset sedikit saja saat mengarahkan (*pointing*), sinyal akan hilang total!
> - Antena Omni 5 dBi memiliki sudut horizontal $360^\circ$ penuh, sehingga tidak perlu pointing sama sekali.

### 3.2 Mengapa Ada "Dead Zone" di Bawah Tower? (Konsep Downtilt)
Banyak teknisi pemula heran: *"Mengapa smartphone yang berada tepat di bawah menara BTS justru sinyalnya lemah atau hilang?"*
- **Penyebab:** Sudut vertikal antena sectoral sangat tipis ($4^\circ - 8^\circ$). Sinyal memancar lurus ke kejauhan melewati atap rumah pengguna di bawah tower!
- **Solusi Engineer (Downtilting):**
  - Miringkan antena sedikit menunduk ke bawah ($2^\circ - 5^\circ$) menggunakan braket (*Mechanical Tilt*) atau pengaturan fasa antena (*Electrical Tilt*) agar berkas menyentuh permukaan tanah di area sasaran.

```
       Tower BTS
         [===] \ 
           |    \   Sudut Berkas Menunduk (Downtilt)
           |     \
           |      \===================> Menjangkau Klien
           |
       [Dead Zone] <--- Area tepat di bawah tower tidak terkena berkas sinyal!
```

---

## 4. POWER DISTRIBUTION & KUALITAS SINYAL LAPANGAN

### 4.1 Regulasi Kominfo & Konsep EIRP
Pemerintah (melalui Kominfo / SDPPI) membatasi daya pancar total nirkabel agar tidak mengacaukan frekuensi publik:
- **EIRP (Effective Isotropic Radiated Power):** Total daya kombinasi antara kekuatan radio pemancar dikurangi redaman kabel, ditambah penguatan antena:
  $$\text{EIRP (dBm)} = P_{Tx}\text{ (dBm)} - \text{Loss Kabel (dB)} + \text{Gain Antena (dBi)}$$
- *Contoh Kasus Lapangan:*
  - Radio diset daya: $20\text{ dBm}$ ($100\text{ mW}$)
  - Kabel pigtail loss: $1\text{ dB}$
  - Antena Grid: $24\text{ dBi}$
  - $\text{EIRP} = 20 - 1 + 24 = \mathbf{43\text{ dBm}}$ ($20\text{ Watt}$ daya efektif terpancar ke udara!).

### 4.2 Front-to-Back (F/B) Ratio: Mencegah Sinyal Bocor ke Belakang
Saat memasang beberapa antena pada satu tiang menara (misal 3 antena sectoral menghadap arah berbeda):
- **Front-to-Back (F/B) Ratio:** Menyatakan seberapa kuat antena memblokir sinyal agar tidak bocor ke arah belakangnya sendiri.
- Nilai F/B ideal adalah **$> 25\text{ dB}$**.
- Jika nilai F/B jelek (misal hanya $10\text{ dB}$), antena sektor 1 akan menembus dan menabrak radio antena sektor 2 di belakangnya, menyebabkan interferensi lokal dan koneksi menjadi lambat (*packet loss*).

### 4.3 Panduan Indikator Kualitas Sinyal (Checklist Engineer)

| Indikator | Nilai Sangat Bagus | Nilai Standar Layak | Nilai Buruk / Bermasalah |
| :--- | :---: | :---: | :---: |
| **Signal Strength (RSSI)** | $-50\text{ s/d } -60\text{ dBm}$ | $-65\text{ s/d } -72\text{ dBm}$ | $<-80\text{ dBm}$ *(Putus-nyambung)* |
| **Noise Floor** | $-95\text{ s/d } -105\text{ dBm}$ | $-90\text{ s/d } -94\text{ dBm}$ | $>-85\text{ dBm}$ *(Area penuh polusi RF)* |
| **Signal to Noise (SNR)** | $> 30\text{ dB}$ | $20 - 29\text{ dB}$ | $< 15\text{ dB}$ *(Throughput drop drastis)* |
| **CCQ (Client Connection Quality)**| $95\% - 100\%$ | $85\% - 94\%$ | $< 70\%$ *(Banyak paket retransmit)* |
