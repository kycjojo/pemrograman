# Soal Tantangan (Level Up): Array & String (Bahasa C)

Dokumen ini berisi **kumpulan soal tantangan tingkat lanjut** bagi kamu yang sudah berhasil menaklukkan soal utama pada [latihan_soal_array_string.md](./latihan_soal_array_string.md). Seluruh soal String maupun HOTS **diperbolehkan penuh menggunakan `#include <string.h>`** (`strlen`, `strcpy`, `strcat`, `strcmp`, `strcmpi`, `strchr`).

---

## Bagian A: Tantangan Bertingkat ARRAY
*Tema Terhubung: Sistem Analitik Nilai Ujian Kelas*

### 🟢 Tantangan Array 1: Validasi Skor, Posisi Juara Kembar, & Statistik
Buatlah program dengan `#define MAKS 50` yang meminta user memasukkan `n` buah skor ujian (`int`) ke dalam array `skor[MAKS]`.
1. **Validasi Input:** Skor yang sah hanya bernilai **`0` s/d `100`**. Jika user memasukkan angka di luar rentang tersebut (misal `-10` atau `105`), tolak angka tersebut dan minta user menginput ulang untuk mahasiswa yang sama tanpa mengurangi jatah `n`.
2. Hitung dan tampilkan **rata-rata kelas** (`float`, 2 angka belakang koma) serta **jumlah mahasiswa yang mendapat skor di atas rata-rata**.
3. Cari **skor tertinggi**, lalu tampilkan juga **mahasiswa urutan ke berapa saja** yang meraih skor tertinggi tersebut (mengantisipasi jika peraih nilai tertinggi lebih dari 1 orang / juara kembar).

**Contoh Eksekusi:**
```text
Masukkan jumlah mahasiswa: 5
Skor Mhs ke-1: 80
Skor Mhs ke-2: 95
Skor Mhs ke-3: 120
  [!] Skor harus 0-100! Masukkan ulang Skor Mhs ke-3: 70
Skor Mhs ke-4: 95
Skor Mhs ke-5: 60

--- HASIL STATISTIK ---
Rata-rata kelas      : 80.00
Di atas rata-rata    : 2 orang
Skor tertinggi       : 95 (Diraih oleh Mhs ke: 2, 4)
```

---

### 🟡 Tantangan Array 2: Fungsi Peringkat & Perhitungan Median
Kembangkan program **Tantangan Array 1** dengan memecahnya ke dalam fungsi berparameter array:
1. `void inputValid(int s[], int n)` — mengisi array dengan validasi rentang `0–100`.
2. `void urutTurun(int s[], int n)` — mengurutkan isi array dari **terbesar ke terkecil (*descending*)**.
3. `float cariMedian(int s[], int n)` — mengembalikan **nilai tengah (Median)** dari data yang sudah diurutkan:
   * Jika `n` **ganjil**, median adalah nilai tepat di posisi tengah.
   * Jika `n` **genap**, median adalah rata-rata dari **dua nilai** yang berada di tengah.
4. Tampilkan Papan Peringkat (`1` s/d `n`), selisih antara nilai tertinggi dan terendah (*jangkauan/range*), serta nilai Mediannya di `main()`.

**Contoh Eksekusi (Kasus `n` Genap):**
```text
Masukkan jumlah mahasiswa: 4
(Misal input skor: 70, 95, 80, 65)

=== PAPAN PERINGKAT ===
Peringkat 1 : 95
Peringkat 2 : 80
Peringkat 3 : 70
Peringkat 4 : 65

Jangkauan (Tertinggi - Terendah) : 30
Median Kelas                     : 75.00
```

---

### 🔴 Tantangan Array 3: Nilai Berbobot & Analisis Dua Arah (Array 2D + Fungsi)
Setiap mahasiswa kini memiliki **3 komponen nilai** di dalam `int nilai[MAKS][3]`, dengan bobot berbeda:
* Kolom `0` = **Kuis (bobot 20%)**
* Kolom `1` = **UTS (bobot 35%)**
* Kolom `2` = **UAS (bobot 45%)**

Buatlah program menggunakan fungsi yang melakukan **analisis dua arah** pada tabel 2D tersebut:
1. **Arah Baris (Ke Samping):** Fungsi `hitungNilaiAkhir(int nilai[][3], float akhir[], int n)` menghitung Nilai Akhir tiap mahasiswa sesuai persentase bobotnya: `(0.20 * Kuis) + (0.35 * UTS) + (0.45 * UAS)`.
2. **Arah Kolom (Ke Bawah):** Fungsi `hitungRataKomponen(int nilai[][3], float rataKomponen[], int n)` menghitung rata-rata kelas untuk masing-masing komponen ujian (rata-rata Kuis, rata-rata UTS, rata-rata UAS) dan menyimpannya ke array `rataKomponen[3]`.
3. Tampilkan tabel rekap lengkap beserta baris ringkasan rata-rata tiap komponen di bagian paling bawah tabel!

**Contoh Eksekusi:**
```text
Masukkan jumlah mahasiswa: 3
Mhs 1 (Kuis UTS UAS): 80 80 90
Mhs 2 (Kuis UTS UAS): 70 80 70
Mhs 3 (Kuis UTS UAS): 90 95 80

Mhs    Kuis     UTS     UAS    Nilai Akhir
------------------------------------------
 1       80      80      90          84.50
 2       70      80      70          73.50
 3       90      95      80          87.25
------------------------------------------
Rata2 80.00   85.00   80.00
```

---

## Bagian B: Tantangan Bertingkat STRING (`#include <string.h>` Diperbolehkan!)
*Tema Terhubung: Sistem Keamanan Sandi, Pembersih Kalimat, & Moderator Pesan*

### 🟢 Tantangan String 1: Validator Kekuatan Password Berlapis (`strlen`, `strcmpi`, `strchr`)
Buatlah program pembuatan akun yang meminta `username` dan `password` (tanpa spasi). Program akan terus meminta user membuat ulang `password` (`do-while`) selama belum memenuhi **keempat syarat keamanan** berikut sekaligus:
1. Panjang `password` minimal **8 karakter** (gunakan `strlen`).
2. `password` **tidak boleh sama** dengan `username` meskipun huruf besar/kecilnya dibedakan (gunakan `strcmpi`).
3. `password` wajib mengandung minimal **1 huruf kapital (`A-Z`)**, **1 huruf kecil (`a-z`)**, dan **1 angka (`0-9`)**.
4. `password` wajib mengandung minimal **1 karakter simbol khusus** yang terdaftar di dalam string `"!@#$%&*"` (gunakan `strchr`).

Setiap kali ditolak, tampilkan **pesan kesalahan spesifik** syarat mana saja yang belum terpenuhi!

**Contoh Eksekusi:**
```text
Masukkan username: Andi26

Buat password: andi26
  [X] Ditolak: Kurang dari 8 karakter!
  [X] Ditolak: Password tidak boleh sama dengan username!
  [X] Ditolak: Belum ada huruf kapital & simbol khusus (!@#$%&*)!

Buat password: KampusPENS26
  [X] Ditolak: Belum ada simbol khusus (!@#$%&*)!

Buat password: Kampus@PENS26
  [V] Password kuat! Akun berhasil dibuat.
```

---

### 🟡 Tantangan String 2: Detektor *Kalimat* Palindrom (`fgets`, `<string.h>`, Fungsi)
Uji palindrom pada **satu kalimat utuh yang mengandung spasi dan tanda baca** (contoh terkenal: `"Kasur ini rusak!"` atau `"Ibu Ratna, antar ubi."`).

Buatlah program dengan `fgets()` dan `<string.h>` yang memiliki fungsi:
1. `void saringHuruf(char asli[], char bersih[])` — menyaring kalimat `asli` sehingga **hanya huruf alfabet (`A-Z`, `a-z`) dan angka (`0-9`)** saja yang masuk ke `bersih[]` (semua spasi, koma, titik, tanda seru, dan Enter `\n` dibuang!), sekaligus mengubah semua huruf kapital menjadi huruf kecil.
2. `int cekPalindrom(char bersih[])` — memeriksa apakah isi `bersih[]` merupakan palindrom (boleh menggunakan `strlen` dengan dua indeks ujung-ke-ujung, atau membalik string lalu membandingkannya dengan `strcmp`).

**Contoh Eksekusi:**
```text
Masukkan sebuah kalimat: Ibu Ratna, antar ubi!
Hasil penyaringan      : iburatnaantarubi
Panjang huruf bersih   : 16 karakter
Kesimpulan             : KALIMAT PALINDROM!
```

---

### 🔴 Tantangan String 3: Sensor Kata Terlarang pada Kalimat Chat (`fgets`, `<string.h>`, Fungsi)
Buatlah program *Chat Moderator* yang menerima:
1. Satu **kalimat pesan obrolan** penuh spasi (`char pesan[200]`, gunakan `fgets`).
2. Satu **kata terlarang** tanpa spasi (`char terlarang[30]`).

Tugas fungsi yang harus kamu buat:
* Periksa setiap kata di dalam `pesan`. Apabila ada kata yang cocok dengan `terlarang` secara **Non-Case Sensitive** (`strcmpi` — sehingga `"Bodoh"`, `"BODOH"`, dan `"bodoh"` semuanya tertangkap), ubah seluruh huruf pada kata tersebut menjadi karakter bintang `'*'` sepanjang kata itu (`strlen`), lalu susun kembali kalimat hasil sensornya (gunakan bantuan `strcpy` / `strcat` atau penulisan per kata).
* Hitung dan tampilkan juga **berapa kali** kata terlarang tersebut ditemukan dalam kalimat!

**Contoh Eksekusi:**
```text
Masukkan pesan chat : Dasar BODOH sekali spammer bodoh dan Bodoh ini
Kata yang disensor  : bodoh

Pesan hasil sensor  : Dasar ***** sekali spammer ***** dan ***** ini
Total kata disensor : 3 kali
```

---

## Bagian C: Tantangan Puncak Ekstra (SUPER HOTS)
*Gabungan Penuh: Array 1D + Array 2D + String (`fgets` & `<string.h>`) + Fungsi + Parallel Sorting + Tie-Breaker + Searching*

### 🔥 Studi Kasus: Sistem Peringkat, Predikat, & Pencarian Nama Lengkap Mahasiswa
Gabungkan seluruh kemampuan Array dan String (`<string.h>`) untuk membangun sistem rekap akademik `n` mahasiswa (`#define MAKS 20`):

1. **Penyimpanan Data Paralel:**
   * **Nama Lengkap (Boleh Mengandung Spasi!):** Simpan di `char nama[MAKS][40]` menggunakan `fgets` (pastikan karakter Enter `'\n'` di ujung input dibersihkan menggunakan bantuan `strlen`, dan gunakan `getchar()` sesudah `scanf` angka sebelum memanggil `fgets`).
   * **3 Nilai Ujian (Bahasa, Matematika, Digital):** Simpan di `int nilai[MAKS][3]`.
   * **Rata-rata & Predikat String:** Hitung rata-rata ke `float rata[MAKS]`, lalu isi otomatis `char predikat[MAKS][15]` menggunakan `strcpy` dengan aturan:
     * `rata >= 80.0` → `"Cumlaude"`
     * `rata >= 65.0` dan `< 80.0` → `"Lulus"`
     * `rata < 65.0` → `"Remedial"`
2. **Fungsi Pengurutan Paralel + *Tie-Breaker* Abjad:**
   * Urutkan seluruh data dari **rata-rata tertinggi ke terendah**.
   * **Aturan Seri (*Tie-Breaker*):** Jika nilai rata-rata dua mahasiswa **sama persis**, urutkan keduanya berdasarkan **abjad Nama Lengkap A ke Z** secara *non-case-sensitive* (`strcmpi`).
   * Pastikan **keempat tabel** (`nama`, `nilai` 3 kolom, `rata`, dan `predikat`) ikut ditukar bersama-sama!
3. **Tabel Laporan & Pencarian Nama:**
   * Tampilkan tabel berisi Peringkat, Nama Lengkap, ketiga nilai, Rata-rata, dan Predikatnya secara lurus dan rapi.
   * Minta user menginput nama lengkap yang ingin dicari (dengan `fgets`), cari secara *non-case-sensitive* (`strcmpi`), lalu tampilkan peringkat dan detail nilainya (atau pesan tidak ditemukan).

**Contoh Eksekusi:**
```text
Masukkan jumlah mahasiswa: 4

Mhs 1 - Nama Lengkap: Ahmad Fauzi
Nilai (Bhs Mat Dig) : 81 90 75
Mhs 2 - Nama Lengkap: Budi Santoso
Nilai (Bhs Mat Dig) : 80 70 70
Mhs 3 - Nama Lengkap: Adang Pratama
Nilai (Bhs Mat Dig) : 50 83 87
Mhs 4 - Nama Lengkap: Citra Dewi
Nilai (Bhs Mat Dig) : 60 55 62

=== TABEL PERINGKAT AKADEMIK ===
Rank  Nama Lengkap        Bhs   Mat   Dig   Rata2    Predikat
---------------------------------------------------------------
 1    Ahmad Fauzi          81    90    75   82.00    Cumlaude
 2    Adang Pratama        50    83    87   73.33    Lulus
 3    Budi Santoso         80    70    70   73.33    Lulus
 4    Citra Dewi           60    55    62   59.00    Remedial
---------------------------------------------------------------

Cari Nama Lengkap: adang pratama
Ditemukan! Adang Pratama ada di Peringkat 2 | Nilai: 50, 83, 87 | Rata2: 73.33 (Lulus)
```
