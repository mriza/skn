# INSTRUMEN EVALUASI: KUIS & TUGAS PERTEMUAN 1
**Mata Kuliah:** Sistem Komunikasi Nirkabel  
**Topik Khusus:** Dasar Keamanan, Protokol Enkripsi, & Autentikasi Nirkabel  
**Program Studi:** Teknologi Rekayasa Komputer (TRK) - Politani  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Pertemuan:** Minggu IX  

---

## BAGIAN 1: KUIS INTERAKTIF PEMAHAMAN ENKRIPSI & HANDSHAKE (DURASI: 45 MENIT)

### A. Soal Pilihan Ganda (Bobot: 50 Poin / @5 Poin)

1. Mode pada kartu antarmuka jaringan nirkabel (wireless NIC) yang memungkinkannya menangkap seluruh frame 802.11 di udara secara pasif tanpa perlu terasosiasi ke Access Point tertentu adalah:
   - A. Managed Mode
   - B. Master Mode
   - C. Monitor Mode
   - D. Ad-Hoc Mode

2. Kegiatan memetakan lokasi dan mencari jaringan nirkabel yang rentan secara mobile (menggunakan kendaraan atau berjalan kaki) dengan memanfaatkan laptop, adapter Wi-Fi berdaya tinggi, dan penerima GPS dinamakan:
   - A. Phishing
   - B. Wardriving
   - C. Port Knocking
   - D. Reverse Engineering

3. Pada algoritma enkripsi stream cipher RC4 (WEP), fungsi utama dari **Initialization Vector (IV)** adalah:
   - A. Menyimpan kata sandi administrator router.
   - B. Memberikan variasi pada kunci rahasia agar keystream yang dihasilkan berbeda untuk setiap paket data.
   - C. Mengatur alokasi alamat IP secara otomatis.
   - D. Membatasi bandwidth kecepatan internet klien.

4. Mengapa ruang gerak ukuran IV yang kecil pada WEP (hanya 24-bit atau sekitar 16,7 juta kemungkinan) dianggap sebagai cacat desain yang sangat fatal?
   - A. Karena membuat perangkat router menjadi sangat panas.
   - B. Karena pada jaringan yang sibuk, nilai IV pasti berulang (*IV Collision*) dalam hitungan jam, memungkinkan penyerang menghilangkan keystream melalui operasi XOR ($C_1 \oplus C_2 = P_1 \oplus P_2$).
   - C. Karena frekuensi 2.4 GHz tidak mampu memancarkan paket 24-bit.
   - D. Karena IV 24-bit tidak kompatibel dengan kabel UTP Cat5e.

5. Tiga lapis mekanisme perbaikan yang dihadirkan oleh protokol **WPA-TKIP** untuk menambal kelemahan WEP adalah:
   - A. Penggantian RC4 ke DES, penambahan panjang SSID, dan penonaktifan DHCP.
   - B. Perbesaran IV menjadi 48-bit, Per-Packet Key Mixing, dan integritas Michael MIC 64-bit.
   - C. Penggunaan sertifikat HTTPS, penutupan port 80, dan pembatasan MAC address.
   - D. Penggunaan frekuensi 5 GHz, modulasi OFDM, dan MIMO.

6. Perbedaan mendasar antara algoritma enkripsi **RC4** (WEP/TKIP) dengan **AES** (WPA2) adalah:
   - A. RC4 adalah block cipher 256-bit, sedangkan AES adalah stream cipher bit-per-bit.
   - B. RC4 adalah stream cipher berurutan bit/byte, sedangkan AES adalah block cipher yang memproses data dalam blok tetap 128-bit melalui putaran permutasi dan substitusi yang kokoh.
   - C. RC4 hanya bisa berjalan di sistem operasi Linux, sedangkan AES hanya di Windows.
   - D. RC4 tidak memerlukan kunci, sedangkan AES memerlukan kunci.

7. Kunci master berukuran 256-bit pada WPA2-PSK yang diturunkan dari Passphrase pengguna dan nama SSID melalui fungsi PBKDF2 (4096 iterasi HMAC-SHA1) disebut:
   - A. Pairwise Transient Key (PTK)
   - B. Pairwise Master Key (PMK)
   - C. Group Temporal Key (GTK)
   - D. Key Confirmation Key (KCK)

8. Kunci sesi sementara berukuran 512-bit yang dihasilkan dari pertukaran 4-Way Handshake (menggabungkan PMK, ANonce, SNonce, MAC AP, dan MAC STA) untuk mengenkripsi traffic unicast disebut:
   - A. Pairwise Transient Key (PTK)
   - B. Pre-Shared Key (PSK)
   - C. Master Session Key (MSK)
   - D. Initialization Vector (IV)

9. Mengapa seorang penyerang yang berhasil merekam frame Message 1 dan Message 2 dari 4-Way Handshake dapat membongkar kata sandi secara *offline* di komputernya?
   - A. Karena kata sandi dikirim dalam teks jelas pada Message 1.
   - B. Karena Message 2 memuat SNonce dan nilai MIC yang dapat diuji coba kecocokannya dengan kamus kata sandi secara lokal tanpa perlu berinteraksi dengan AP target.
   - C. Karena router otomatis mati setelah Message 2 terkirim.
   - D. Karena Message 2 mematikan seluruh enkripsi firewall AP.

10. Mengapa fitur menyembunyikan SSID (*Hide SSID*) tidak dapat melindungi jaringan nirkabel dari penyerang?
    - A. Karena sinyal radio otomatis padam jika SSID disembunyikan.
    - B. Karena nama SSID tetap dikirimkan dalam bentuk teks terbuka (*plaintext*) saat klien melakukan probe request atau asosiasi ke AP.
    - C. Karena undang-undang telekomunikasi mewajibkan SSID berstatus publik.
    - D. Karena hanya kartu Wi-Fi buatan Intel yang bisa membaca hidden SSID.

---

### B. Soal Analisis Kritis & Hitungan (Bobot: 50 Poin / @25 Poin)

**Soal 1 (Analisis Matematis IV Collision & Keruntuhan WEP):**  
Di sebuah gedung laboratorium komputer Politani yang menggunakan jaringan Wi-Fi lama berbasis WEP-128, tercatat rata-rata lalu lintas data padat sebesar 2.000 paket per detik.
1. Hitung berapa jam waktu yang dibutuhkan hingga seluruh ruang nilai IV 24-bit ($2^{24} = 16.777.216$) habis terpakai dan pasti terjadi perulangan nilai IV (*IV Collision*)!
2. Jelaskan dengan persamaan matematis operasi XOR mengapa ketika terjadi IV Collision pada dua paket ($C_1$ dan $C_2$), penyerang dapat melenyapkan keystream dan membongkar data asli ($P_1 \oplus P_2$)!

**Soal 2 (Arsitektur Derivasi Kunci WPA2: PMK vs PTK):**  
Jelaskan perbedaan mendasar antara **PMK (Pairwise Master Key)** dan **PTK (Pairwise Transient Key)** dalam arsitektur WPA2-PSK:
1. Bagaimana PMK dibentuk dari passphrase pengguna melalui fungsi PBKDF2? Mengapa nama SSID dijadikan salah satu input (*salt*) penting?
2. Bagaimana PTK dibentuk saat pertukaran 4-Way Handshake? Sebutkan 4 sub-kunci fungsional yang berada di dalam PTK 512-bit beserta peran masing-masing!

---

## BAGIAN 2: TUGAS TERSTRUKTUR (LAPORAN ANALISIS PAKET & PERBANDINGAN ENKRIPSI)

### Petunjuk Tugas:
1. Sifat: Tugas Individu. Waktu pengumpulan: 1 Minggu ke depan.
2. Format: Laporan Teknis PDF (5 - 7 Halaman).

### Muatan Wajib Laporan:
1. **Analisis Paket Capture Wireshark:**
   - Lampirkan screenshot frame Beacon: Jelaskan field **RSN Information Element** (Cipher Suite, Auth Key Management).
   - Lampirkan screenshot urutan 4 frame **EAPOL-Key Handshake**: Tunjukkan field ANonce pada Message 1, SNonce dan MIC pada Message 2, serta instalasi GTK pada Message 3.
2. **Tabel Komparasi 4 Generasi Protokol Enkripsi:**
   - Susun tabel perbandingan komprehensif antara: **WEP, WPA-TKIP, WPA2-CCMP, dan WPA3-SAE**.
   - Parameter yang dibandingkan: Algoritma Chiper (RC4 vs AES vs ECC), Ukuran IV/Nonce, Mekanisme Integritas (CRC32 vs Michael vs CBC-MAC), Ketahanan terhadap Offline Attack, dan Status Standardisasi Saat Ini.

---

## BAGIAN 3: KUNCI JAWABAN KUIS PILIHAN GANDA & PEMBAHASAN

### Kunci Jawaban Pilihan Ganda:
1. **C** | 2. **B** | 3. **B** | 4. **B** | 5. **B** | 6. **B** | 7. **B** | 8. **A** | 9. **B** | 10. **B**

### Pembahasan Soal Analisis:

**Soal 1:**
1. *Waktu habisnya IV 24-bit:*
   $$\text{Waktu (detik)} = \frac{16.777.216}{2.000} = 8.388,6\text{ detik}$$
   $$\text{Waktu (jam)} = \frac{8.388,6}{3.600} \approx \mathbf{2,33\text{ Jam (sekitar 2 jam 20 menit)}}.$$
   *(Artinya, hanya dalam waktu kurang dari 2,5 jam, tabrakan IV pasti terjadi $100\%$!).*
2. *Lenyapnya Keystream pada IV Collision:*
   - Paket 1: $C_1 = P_1 \oplus K$
   - Paket 2: $C_2 = P_2 \oplus K$
   - Karena kedua paket menggunakan nilai IV yang sama, maka keystream $K$ bernilai identik.
   - Operasi XOR ciphertext:
     $$C_1 \oplus C_2 = (P_1 \oplus K) \oplus (P_2 \oplus K)$$
     Karena sifat asosiatif dan komutatif serta $K \oplus K = 0$:
     $$C_1 \oplus C_2 = P_1 \oplus P_2 \oplus (K \oplus K) = \mathbf{P_1 \oplus P_2}$$
   - Keystream $K$ hilang total dari persamaan, menyisakan XOR dari dua plaintext asli yang mudah direkonstruksi oleh penyerang.

**Soal 2:**
1. *Derivasi PMK & Peran SSID:*
   - $\text{PMK} = \text{PBKDF2}(\text{Passphrase}, \text{SSID}, 4096, 32)$.
   - SSID berfungsi sebagai *cryptographic salt*. Tanpa SSID sebagai salt, dua jaringan yang menggunakan password yang sama akan menghasilkan PMK yang persis sama, sehingga rentan diserang menggunakan tabel pencarian massal (*precomputed rainbow table*). Dengan adanya SSID sebagai salt, penyerang terpaksa menghitung ulang kalkulasi dari awal untuk setiap nama jaringan unik.
2. *Pembentukan PTK & 4 Sub-Kunci:*
   - $\text{PTK} = \text{PRF-512}(\text{PMK}, \text{ANonce}, \text{SNonce}, \text{MAC AP}, \text{MAC STA})$.
   - Empat sub-kunci di dalam PTK 512-bit:
     1. **KCK (128-bit):** Memverifikasi integritas frame handshake (MIC) di M2 & M4.
     2. **KEK (128-bit):** Mengenkripsi kunci broadcast GTK saat dikirim di M3.
     3. **TK (128-bit):** Kunci data unicast klien untuk modul enkripsi AES-CCMP.
     4. **MIC Key (64-bit):** Menjaga integritas data unicast klien.
