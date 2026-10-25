# MATERI KULIAH: DASAR KEAMANAN, PROTOKOL ENKRIPSI, & AUTENTIKASI NIRKABEL
**Mata Kuliah:** Sistem Komunikasi Nirkabel (3 SKS)  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Pertemuan:** Minggu IX (Pertemuan 1 Modul Keamanan)  
**Alokasi Waktu:** 210 Menit (3 x 70 menit)  
**Dokumen Pendamping:** `Bacaan_Mahasiswa_Keamanan_Nirkabel.docx`, `Catatan_Dosen_Keamanan_Nirkabel.docx`, `Slide_Keamanan_Nirkabel.pptx`

---

## RUNDOWN & RENCANA WAKTU PEMBELAJARAN (TOTAL: 210 MENIT)

| Sesi | Waktu | Aktivitas Pembelajaran | Fokus & Output |
| :--- | :---: | :--- | :--- |
| **Sesi 1** | 00:00 - 00:35 (35m) | **Sifat Media Nirkabel, Model Ancaman, & Mode Interface**<br>- Perimeter fisik vs perimeter elektromagnetik (*RF signal leakage*).<br>- CIA Triad pada WLAN.<br>- **Mode Interface Kartu Wireless:** Managed (Station), Master (AP), Monitor (Promiscuous/Sniffing), Ad-Hoc, dan Mesh.<br>- **Konsep Wardriving:** Peta pemindaian sinyal mobile berbasis GPS & WiGLE. | Pemahaman arsitektur kartu nirkabel dan model ancaman media terbuka. |
| **Sesi 2** | 00:35 - 01:25 (50m) | **Bedah WEP & Mengapa Ruang Gerak IV Kecil Sangat Berisiko**<br>- Apa itu **IV (Initialization Vector)** pada kriptografi stream cipher RC4.<br>- **Matematika IV Collision:** Ruang $2^{24}$ (16,7 juta paket) habis dalam hitungan jam di jaringan sibuk.<br>- Konsekuensi matematis $C_1 \oplus C_2 = P_1 \oplus P_2$ (bocoran keystream).<br>- Serangan FMS (*Fluhrer-Mantin-Shamir*) & PTW (*Pyshkin-Tews-Weinmann*).<br>- **WPA-TKIP:** 3 lapis penambal darurat (IV 48-bit, per-packet key mixing Phase 1 & 2, Michael MIC) dan kelemahannya (*Beck-Tews attack*). | Bedah kelemahan struktural WEP dan alasan TKIP di-deprecate. |
| **Sesi 3** | 01:25 - 01:45 (20m) | *Istirahat & Kuis Interaktif Sesi 1 (Mentimeter / Form)* | Rehat sejenak dan evaluasi cepat pemahaman dasar. |
| **Sesi 4** | 01:45 - 02:35 (50m) | **Standar WPA2 (IEEE 802.11i), AES-CCMP, & Derivasi Kunci**<br>- Mengapa AES menggantikan RC4 (Block cipher 128-bit vs Stream cipher).<br>- CCMP: Menjawab *Confidentiality* (CTR mode) + *Integrity* (CBC-MAC).<br>- **Derivasi Kunci Master (PMK):** Algoritma PBKDF2 (Passphrase + SSID + 4096 iterasi HMAC-SHA1). Mengapa SSID menjadi salt?<br>- **Mekanisme 4-Way Handshake:** Bedah pesan M1, M2, M3, dan M4.<br>- **Derivasi Kunci Sesi (PTK):** Fungsi PRF-512 menghasilkan 4 sub-kunci (KCK, KEK, TK, MIC Key).<br>- Celah Struktural: Mengapa WPA2-PSK rentan terhadap **Offline Dictionary Attack**? | Pemahaman utuh alur pembentukan kunci dan celah handshake. |
| **Sesi 5** | 02:35 - 03:10 (35m) | **Standar Baru WPA3-SAE & Membongkar Mitos Keamanan**<br>- WPA3-SAE (*Simultaneous Authentication of Equals*) berbasis Dragonfly Handshake.<br>- Konsep *Zero-Knowledge Proof (ZKP)* dan *Forward Secrecy* (kebal offline attack).<br>- **Mitos #1:** Hide SSID (Mengapa SSID tetap terbaca di Probe Request/Response).<br>- **Mitos #2:** MAC Filtering (Kemudahan MAC spoofing via header plaintext 802.11). | Komparasi WPA2 vs WPA3 dan best practices praktis. |
| **Sesi 6** | 03:10 - 03:30 (20m) | **Rangkuman 4 Generasi, Refleksi Pembelajaran, & Arahan Praktikum** | Sintesis materi 4 generasi, tanya jawab refleksi, briefing lab Wireshark. |

---

## 1. PENDAHULUAN: SIFAT MEDIA NIRKABEL & MODE INTERFACE

### 1.1 Perimeter Fisik vs Perimeter Elektromagnetik
- **Jaringan Kabel (IEEE 802.3):** Memiliki batas perimeter fisik yang tegas. Penyerang harus terhubung secara fisik ke kabel UTP atau port switch (*guided media*).
- **Jaringan Nirkabel (IEEE 802.11):** Sinyal RF merambat bebas ke segala arah (*unguided broadcast medium*) melintasi tembok, kaca, dan batas properti gedung (*RF Signal Leakage*). Jarak jangkauan AP standar indoor adalah $\sim 30 - 50\text{ meter}$, namun dengan antena pengarah (*directional high-gain*), sinyal bocoran dapat ditangkap dari jarak ratusan meter di area parkir luar gedung.

```
+-----------------------------------------------------------------------------------+
| MODEL ANCAMAN:                                                                    |
| Kabel UTP  : Butuh akses fisik langsung / wiretapping di ruang server.            |
| Wi-Fi 802.11: Cukup kartu nirkabel mode monitor dari luar pagar properti!         |
+-----------------------------------------------------------------------------------+
```

### 1.2 Mode Operasi Antarmuka Nirkabel (Wireless Interface Modes)
Chipset kartu jaringan nirkabel (NIC) dapat dikonfigurasi dalam beberapa mode operasi:
1. **Managed Mode (Station / Client Mode):**
   - Mode default perangkat klien (laptop, smartphone).
   - Kartu hanya berkomunikasi dengan satu Access Point (BSSID) yang telah terasosiasi dan menyaring frame yang bukan miliknya.
2. **Master Mode (Access Point Mode):**
   - Kartu bertindak sebagai Access Point (AP), memancarkan frame Beacon secara periodik, menerima asosiasi klien, dan menjembatani lalu lintas data.
3. **Monitor Mode (Promiscuous RF Mode):**
   - Kartu melepaskan diri dari asosiasi AP manapun dan mendengarkan seluruh gelombang radio pada kanal frekuensi tertentu secara pasif.
   - Menangkap seluruh jenis frame 802.11 di udara (Management, Control, dan Data frame), baik yang ditujukan kepadanya maupun yang bukan.
   - **Mode wajib bagi auditor keamanan** (digunakan oleh tool seperti `airodump-ng`, `kismet`, dan `wireshark`).
4. **Ad-Hoc Mode (IBSS - Independent Basic Service Set):**
   - Komunikasi langsung *peer-to-peer* antar-perangkat nirkabel tanpa perantara Access Point.
5. **Mesh Mode (IEEE 802.11s):**
   - Kartu berpartisipasi dalam topologi jala dinamis untuk saling meneruskan paket (*multi-hop forwarding*).

### 1.3 Apa itu Wardriving?
- **Wardriving** adalah aktivitas mencari, memetakan, dan mencatat keberadaan jaringan nirkabel (Wi-Fi) yang rentan atau tidak berpengaman saat bergerak menggunakan kendaraan (mobil, sepeda motor, atau berjalan kaki).
- **Peralatan Standar Wardriving:**
  1. Laptop / Raspberry Pi dengan sistem operasi audit (Kali Linux).
  2. Adapter Wi-Fi eksternal berdaya tinggi (High-Gain Alfa Network) dalam **Monitor Mode**.
  3. Modul GPS Receiver USB untuk mencatat titik koordinat garis lintang dan bujur (Latitude/Longitude).
  4. Software pemetaan: `Kismet` atau aplikasi Android `WiGLE WiFi Wardriving`.
- **Dampak Bagi Keamanan Kampus/Industri:** Data yang dikumpulkan diunggah ke database publik seperti [WiGLE.net](https://wigle.net), memungkinkan siapapun melihat peta lokasi SSID, tipe enkripsi (WEP, WPA2, WPA3), MAC address AP, dan potensi celah keamanannya.

---

## 2. BEDAH WEP & MENGAPA RUANG GERAK IV KECIL SANGAT BERISIKO

```
                       STRUKTUR PAKET ENKRIPSI WEP
       +-------------+------------------+-----------------------+-------------+
       | 802.11 Hdr  |  IV (24-bit)     |  Encrypted Payload    |  ICV (CRC32)|
       | (Plaintext) |  (Plaintext!)    |  (RC4 Stream Cipher)  |  (Checksum) |
       +-------------+------------------+-----------------------+-------------+
```

### 2.1 Apa itu IV (Initialization Vector)?
- WEP menggunakan algoritma **RC4**, yaitu sebuah *stream cipher*. Stream cipher bekerja dengan cara menghasilkan deretan bit acak semu tak hingga yang disebut **Keystream**.
- Keystream ini kemudian dioperasikan menggunakan gerbang logika **XOR ($\oplus$)** dengan data asli (*Plaintext*) untuk menghasilkan teks tersandi (*Ciphertext*):
  $$\text{Ciphertext} = \text{Plaintext} \oplus \text{Keystream}$$
- **Masalah Kunci Statis:** Jika pemancar hanya menggunakan kunci rahasia statis yang sama untuk mengenkripsi setiap paket, maka Keystream yang dihasilkan akan selalu identik!
- **Fungsi IV:** Untuk mencegah Keystream berulang, ditambahkanlah **Initialization Vector (IV)**. Kunci yang diumpankan ke RC4 adalah gabungan dari IV dan Kunci Rahasia:
  $$\text{RC4 Seed} = \text{IV} \parallel \text{Shared Secret Key}$$
  Dengan mengganti nilai IV pada setiap paket, keystream yang dihasilkan menjadi bervariasi.

### 2.2 Mengapa Ruang Gerak IV Kecil (24-Bit) Sangat Berisiko?
Pada standar WEP, perancang protokol hanya mengalokasikan **24-bit** untuk ukuran IV.
1. **Total Kemungkinan Nilai IV:**
   $$2^{24} = 16.777.216\ \text{kemungkinan (sekitar 16,7 juta)}$$
2. **Kapan Terjadi IV Collision (Tabrakan IV)?**
   - Di jaringan kampus atau kantor yang sibuk dengan transfer data rata-rata 1.000 paket per detik:
     $$1.000\text{ paket/detik} \times 3.600\text{ detik} = 3.600.000\text{ paket/jam}$$
   - Dalam waktu kurang dari **4,6 jam**, ruang 16,7 juta IV akan habis terpakai dan pasti terjadi perulangan nilai IV (*IV Collision*).
   - Menurut teori probabilitas **Birthday Paradox**, tabrakan dua IV yang sama dengan peluang $> 50\%$ bahkan sudah terjadi setelah mengumpulkan sekitar **$\sqrt{2^{24}} \approx 4.096\text{ hingga } 5.000\text{ paket}$** saja jika generator IV bersifat pseudorandom!
3. **Bencana Kriptografi Akibat IV Collision:**
   - Karena IV dikirimkan dalam bentuk **plaintext tidak terenkripsi** di depan payload, penyerang dapat memantau udara dan mendeteksi secara pasti kapan dua paket menggunakan nilai IV yang persis sama.
   - Jika dua paket ($P_1$ dan $P_2$) dienkripsi dengan IV yang sama, maka keduanya menggunakan Keystream ($K$) yang sama persis:
     $$C_1 = P_1 \oplus K$$
     $$C_2 = P_2 \oplus K$$
   - Ketika penyerang melakukan operasi XOR antara kedua Ciphertext ($C_1 \oplus C_2$):
     $$C_1 \oplus C_2 = (P_1 \oplus K) \oplus (P_2 \oplus K) = P_1 \oplus P_2$$
   - **Keystream $K$ musnah dari persamaan!** Penyerang kini memegang hasil XOR dua data asli ($P_1 \oplus P_2$). Mengingat paket jaringan memiliki format header yang baku (seperti header TCP/IP atau SNAP yang mudah ditebak), penyerang dapat merekonstruksi isi pesan asli dan membongkar keystream secara instan.
4. **Serangan Praktis FMS & PTW:**
   - Pada tahun 2001, Scott Fluhrer, Itsik Mantin, dan Adi Shamir mempublikasikan celah penjadwalan kunci RC4 (*FMS Attack*). Terdapat nilai-nilai IV tertentu ("Weak IVs") yang membocorkan informasi byte kunci rahasia lapis demi lapis ke ciphertext.
   - Pada tahun 2007, serangan disempurnakan oleh Pyshkin, Tews, dan Weinmann (*PTW Attack*). Cukup dengan mengumpulkan 20.000 - 40.000 paket IV (hanya butuh waktu $\sim 60\text{ detik}$ menggunakan tool `aircrack-ng`), kunci rahasia WEP dapat dipecahkan $100\%$.

---

## 3. TRANSISI KE WPA & TKIP (SOLUSI SEMENTARA)

Karena penggantian jutaan perangkat router dan kartu Wi-Fi di seluruh dunia membutuhkan waktu bertahun-tahun, Wi-Fi Alliance pada tahun 2003 merilis **WPA (Wi-Fi Protected Access)** sebagai solusi penambal sementara (*stopgap*) yang dapat dipasang via pembaruan firmware (*firmware upgrade*):

### 3.1 Tiga Lapis Penambal pada TKIP (Temporal Key Integrity Protocol):
1. **Memperbesar Ukuran IV Menjadi 48-Bit:**
   - Ruang nilai IV melonjak drastis dari $2^{24}$ (16,7 juta) menjadi:
     $$2^{48} \approx 281.474.976.710.656\ \text{(281 Triliun)}$$
   - Pada kecepatan 10.000 paket/detik sekalipun, IV collision baru akan terjadi setelah **890 tahun**! Tabrakan IV secara praktis berhasil dimusnahkan.
2. **Per-Packet Key Mixing (Pencampuran Kunci per Paket):**
   - Kunci enkripsi RC4 tidak lagi digabung langsung dengan IV seperti WEP.
   - TKIP menggunakan dua fase fungsi mixing (*Phase 1 & Phase 2 Key Mixing*): Transmitter MAC address, kunci master temporal, dan IV 48-bit dicampur secara matematis untuk menghasilkan kunci RC4 128-bit baru yang unik untuk setiap paket data.
3. **Message Integrity Check (Michael MIC):**
   - WEP menggunakan CRC32 (ICV) yang mudah dimanipulasi penyerang karena linearitasnya.
   - TKIP menggantinya dengan algoritma integritas kriptografis **Michael MIC** (64-bit). Jika terdeteksi 2 paket dengan MIC salah dalam rentang 60 detik (*MIC failure*), AP akan mematikan koneksi selama 1 menit untuk meredam serangan injeksi.

### 3.2 Mengapa TKIP Akhirnya Ditinggalkan (*Deprecated*)?
Meskipun menambal kelemahan IV, fondasi algoritma TKIP tetaplah stream cipher **RC4**. Pada tahun 2008, Erik Tews dan Martin Beck menerbitkan serangan **Beck-Tews Attack** yang berhasil mendekripsi paket data ARP berukuran kecil dalam waktu 15 menit tanpa mengetahui kunci utama. Sejak tahun 2012, Wi-Fi Alliance resmi melarang penggunaan TKIP.

---

## 4. STANDAR WPA2 (IEEE 802.11i), AES-CCMP, & DERIVASI KUNCI

```
                   PIRAMIDA DERIVASI KUNCI WPA2-PSK
                   
                         [ Passphrase User ]
                         (misal: "kuliah2024")
                                  |
                                  v  + [ SSID Kampus (Salt) ]
                       [ PBKDF2: 4096 Iterasi ]
                                  |
                                  v
                       [ PMK: Master Key 256-bit ]
                                  |
               +------------------+------------------+
               |         4-WAY HANDSHAKE             |
               | (Tukar ANonce, SNonce, MAC AP, STA) |
               +------------------+------------------+
                                  |
                                  v  [ PRF-512 Pseudo-Random Function ]
                       [ PTK: Session Key 512-bit ]
                                  |
          +---------------+-------+-------+---------------+
          |               |               |               |
          v               v               v               v
     [ KCK: 128-bit ] [ KEK: 128-bit ] [ TK: 128-bit ] [ MIC Key: 64-bit ]
      Verifikasi MIC   Enkripsi GTK   Enkripsi Data   Integritas Data
       di Handshake     di Pesan M3    Unicast Klien    Unicast Klien
```

### 4.1 Mengapa AES (Advanced Encryption Standard)?
- **Stream Cipher (RC4) vs Block Cipher (AES):**
  - Stream cipher mengenkripsi data bit-per-bit / byte-per-byte. Sangat rentan jika ada manipulasi aliran bit atau pengulangan keystream.
  - Block cipher (AES) mengelompokkan data ke dalam blok berukuran tetap (**128-bit**) dan mengacaknya melalui 10 putaran (*rounds*) permutasi dan substitusi matematis yang sangat kompleks. Sejak diresmikan NIST tahun 2001, belum ada serangan praktis yang mampu menembus AES-128.
- **Mode CCMP (Counter Mode with CBC-MAC Protocol):**
  - **Counter (CTR) Mode:** Menjamin kerahasiaan (*Confidentiality*).
  - **CBC-MAC:** Menghasilkan tanda tangan keaslian pesan (*Integrity*).
  - *Catatan Penting Engineer:* Hanya payload data yang dienkripsi oleh AES. Header 802.11 (MAC pengirim, MAC penerima, BSSID) dan CCMP Header tetap dikirim secara plaintext untuk keperluan routing switch/AP.

---

### 4.2 Derivasi PMK dari Passphrase (PBKDF2)
Kunci yang dimasukkan pengguna saat mengkoneksikan Wi-Fi (kata sandi/passphrase) tidak langsung dipakai mengenkripsi data. Kunci diolah terlebih dahulu melalui fungsi turunan **PBKDF2 (Password-Based Key Derivation Function 2)**:
$$\text{PMK} = \text{PBKDF2}(\text{Passphrase}, \text{SSID}, 4096, 32)$$
- **Komponen:**
  - `Passphrase`: Kata sandi (8 - 63 karakter ASCII).
  - `SSID`: Nama jaringan nirkabel bertindak sebagai **Kriptografi Salt**.
  - `4096`: Jumlah perulangan (*iterations*) fungsi hash HMAC-SHA1.
  - `32`: Panjang kunci hasil derivasi ($32\text{ byte} = 256\text{ bit}$).

> [!IMPORTANT]
> **Mengapa SSID Dijadikan Salt?**
> Jika dua jaringan berbeda sama-sama menggunakan kata sandi "kopi1234", namun SSID-nya berbeda (Jaringan A: `KantinPolitani`, Jaringan B: `RumahDosen`), maka nilai PMK yang dihasilkan akan **berbeda total secara kriptografis**! Hal ini menggagalkan serangan tabel pencarian awal (*precomputed rainbow table attack*). Mengganti nama SSID default router ("Linksys", "TP-Link") ke nama unik kampus adalah langkah pertahanan wajib.

---

### 4.3 Alur 4-Way Handshake WPA2-PSK
Setelah AP dan Klien (STA) sama-sama menghitung nilai PMK secara lokal, mereka melakukan pertukaran 4 frame **EAPoL-Key (IEEE 802.1X)** di udara:

1. **Message 1 (AP $\rightarrow$ STA):**
   - AP membuat angka acak **ANonce** (*AP Nonce*) dan mengirimkannya ke STA.
   - *Tujuan:* Memberikan komponen acak AP ke stasiun klien.
2. **Message 2 (STA $\rightarrow$ AP):**
   - STA membuat angka acak **SNonce** (*Station Nonce*).
   - STA kini memiliki lengkap: PMK, ANonce, SNonce, MAC AP, dan MAC STA. STA menghitung **PTK (Pairwise Transient Key)**.
   - STA mengirimkan **SNonce** beserta tanda tangan **MIC (Message Integrity Check)** yang dihitung menggunakan subkunci KCK.
   - *Verifikasi AP:* AP menerima SNonce, menghitung PTK lokal, lalu memeriksa MIC. Jika MIC cocok, AP yakin 100% bahwa stasiun klien mengetahui kata sandi PMK yang benar!
3. **Message 3 (AP $\rightarrow$ STA):**
   - AP mengirimkan perintah "Install Key" beserta **GTK (Group Temporal Key)** yang telah dienkripsi menggunakan subkunci KEK.
   - Pesan M3 juga dilindungi oleh MIC.
4. **Message 4 (STA $\rightarrow$ AP):**
   - STA mengirimkan frame konfirmasi ACK bahwa seluruh kunci telah berhasil dipasang di kartu jaringan.
   - AP membuka port virtual dan klien resmi dapat mulai berselancar internet.

---

### 4.4 Derivasi PTK (Pairwise Transient Key) & Empat Sub-Kunci
Kunci sesi unicast PTK dihasilkan melalui fungsi ekspansi pseudo-random **PRF-512**:
$$\text{PTK} = \text{PRF-512}(\text{PMK}, \text{"Pairwise key expansion"}, \text{Min(MAC)}, \text{Max(MAC)}, \text{Min(Nonce)}, \text{Max(Nonce)})$$
PTK berukuran **512-bit** yang secara cerdas dipecah menjadi 4 sub-kunci fungsional (*Principle of Key Separation*):
1. **KCK (Key Confirmation Key - 128 bit):** Khusus dipakai menghitung dan memvalidasi nilai MIC pada handshake (Message 2 & Message 4).
2. **KEK (Key Encryption Key - 128 bit):** Khusus dipakai mengenkripsi kunci multicast GTK saat dikirimkan di Message 3.
3. **TK (Temporal Key - 128 bit):** Kunci utama yang dipakai oleh modul hardware AES-CCMP untuk mengenkripsi seluruh payload data internet unicast.
4. **MIC Key (64 bit):** Digunakan untuk fungsi integritas paket data.

---

### 4.5 Mengapa WPA2-PSK Rentan Terhadap Offline Dictionary Attack?
- Pada Message 1, penyerang dapat menangkap **ANonce** dan MAC Address kedua belah pihak.
- Pada Message 2, penyerang dapat menangkap **SNonce** dan nilai **MIC**.
- **Celah Offline:** Penyerang tidak perlu mengirim paket apapun ke AP target. Penyerang cukup membawa pulang file rekaman handshake (`.cap`) ke komputernya:
  1. Penyerang mengambil 1 kata tebakan dari kamus kata sandi (*wordlist*).
  2. Menghitung PMK tebakan: $\text{PMK}_{test} = \text{PBKDF2}(\text{tebakan}, \text{SSID}, 4096)$.
  3. Menghitung PTK tebakan: $\text{PTK}_{test} = \text{PRF-512}(\text{PMK}_{test}, \text{ANonce}, \text{SNonce}, \text{MAC})$.
  4. Menghitung MIC tebakan menggunakan $\text{KCK}_{test}$.
  5. Jika $\text{MIC}_{test} == \text{MIC}_{\text{nyata pada M2}}$, maka kata sandi berhasil dipecahkan!
- Karena proses pencocokan dilakukan secara lokal di GPU penyerang (menggunakan tool `hashcat`), penyerang dapat menguji **jutaan kata sandi per detik** tanpa risiko terblokir oleh router target!

---

## 5. GENERASI MUTAKHIR WPA3-SAE & MEMBONGKAR MITOS KEAMANAN

### 5.1 WPA3-SAE (Simultaneous Authentication of Equals)
- WPA3 menghapus total mekanisme 4-Way Handshake PSK tradisional dan menggantinya dengan **Dragonfly Handshake** berbasis kurva eliptis (Elliptic Curve Cryptography P-256).
- **Zero-Knowledge Proof (ZKP):** Klien dan AP saling membuktikan kepemilikan kata sandi tanpa membocorkan bit atau petunjuk matematis apapun di udara.
- **Forward Secrecy:** Kunci enkripsi sesi diturunkan secara independen dari pertukaran Diffie-Hellman efemeral. Jika suatu hari kata sandi kampus bocor, seluruh rekaman data masa lalu yang pernah disadap oleh penyerang tetap mustahil untuk didekripsi!
- **Anti-Offline Attack:** Penyerang tidak bisa lagi melakukan offline cracking. Setiap tebakan kata sandi harus diuji secara langsung (*online interaction*) dengan AP, sehingga mudah digagalkan melalui mekanisme *rate-limiting* (pemblokiran otomatis setelah 3-5 kali gagal).

---

### 5.2 Membongkar Mitos Pengamanan Nirkabel Populer

#### Mitos #1: "Menyembunyikan SSID (Hide SSID) Membuat Jaringan Aman"
- **Fakta Teknis:** Menyembunyikan SSID hanyalah mematikan penulisan nama SSID di frame Beacon berkala. Namun:
  1. Klien yang ingin terhubung tetap harus memancarkan frame **Probe Request** yang memuat nama SSID target secara terbuka (*plaintext*).
  2. Saat asosiasi berlangsung, AP membalas dengan **Probe Response** dan **Association Response** yang memuat nama SSID secara gamblang.
- Tool sederhana seperti `airodump-ng` akan langsung menampilkan nama SSID tersembunyi begitu ada 1 perangkat resmi yang terhubung ke jaringan tersebut. Menyembunyikan SSID hanya merepotkan pengguna resmi dan tidak menghambat penyerang sama sekali.

#### Mitos #2: "MAC Address Filtering Efektif Membatasi Akses"
- **Fakta Teknis:** Standar IEEE 802.11 mewajibkan alamat MAC pengirim dan penerima berada pada header unencrypted (terbuka) di setiap frame agar switch dan access point dapat meneruskan paket.
- Seorang penyerang cukup menyalakan kartu jaringan ke **Monitor Mode**, mengamati MAC address laptop dosen yang sedang aktif berselancar, lalu mengganti MAC address laptopnya menggunakan perintah sederhana di Linux:
  ```bash
  sudo ip link set dev wlan0 down
  sudo macchanger -m 00:11:22:33:44:55 wlan0
  sudo ip link set dev wlan0 up
  ```
- Dalam tempo 10 detik, penyerang telah berhasil mem-bypass seluruh sistem proteksi MAC filtering kampus!
