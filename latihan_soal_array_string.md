# Lembar Latihan Soal Bertingkat: Array & String (Bahasa C)

Seluruh soal disusun dengan tingkat kesulitan bertahap yang ramah dipelajari namun saling menyambung dari level dasar hingga gabungan. Untuk soal String dan HOTS, kamu **diperbolehkan penuh menggunakan pustaka `#include <string.h>`**.

---

## Bagian A: Soal Bertingkat ARRAY
*Tema Terhubung: Pengolahan Nilai Ujian Kelas*

### 🟢 Soal Array 1 (Level Dasar): Rata-Rata & Skor Tertinggi Kelas
Buatlah program dengan konstanta `#define MAKS 50` yang meminta user memasukkan jumlah mahasiswa `n`, lalu menginput `n` buah skor ujian (`int`) ke dalam array 1 dimensi `skor[MAKS]`.
Setelah semua skor masuk, tampilkan kembali:
1. Seluruh daftar skor yang telah diinput dalam satu baris.
2. Nilai **rata-rata** kelas (`float`, tampilkan 2 angka di belakang koma).
3. Skor **tertinggi** yang ada di dalam array tersebut.

**Contoh Eksekusi:**
```text
Masukkan jumlah mahasiswa: 5
Skor ke-1: 80
Skor ke-2: 65
Skor ke-3: 90
Skor ke-4: 75
Skor ke-5: 85

Daftar skor      : 80 65 90 75 85
Rata-rata kelas  : 79.00
Skor tertinggi   : 90
```

---

### 🟡 Soal Array 2 (Level Menengah): Papan Peringkat dengan Fungsi
Kembangkan program dari **Soal Array 1** dengan memecah prosesnya ke dalam 3 fungsi yang menjadikan **array sebagai parameter**:
1. `void inputSkor(int s[], int n)` — bertugas meminta input `n` buah skor ke dalam array.
2. `void urutTurun(int s[], int n)` — bertugas mengurutkan isi array dari **nilai terbesar ke terkecil (*descending*)**.
3. `void tampilRanking(int s[], int n)` — bertugas menampilkan daftar skor berurutan mulai dari Peringkat 1 hingga Peringkat `n`.
4. Panggil ketiga fungsi tersebut secara berurutan di dalam `main()`, lalu tampilkan juga skor tertinggi dan skor terendahnya.

**Contoh Eksekusi:**
```text
Masukkan jumlah mahasiswa: 5
Skor ke-1: 80
Skor ke-2: 65
Skor ke-3: 90
Skor ke-4: 75
Skor ke-5: 85

=== PAPAN PERINGKAT ===
Peringkat 1 : 90
Peringkat 2 : 85
Peringkat 3 : 80
Peringkat 4 : 75
Peringkat 5 : 65

Skor Tertinggi: 90 | Skor Terendah: 65
```

---

### 🔴 Soal Array 3 (Level Lanjutan): Rekap 3 Nilai Ujian (Array 2D + Fungsi)
Kembangkan lagi programmu ke **Array 2 Dimensi**: sekarang setiap mahasiswa memiliki **3 nilai ujian** (**Tugas**, **UTS**, dan **UAS**) yang disimpan dalam `int nilai[MAKS][3]`.
1. Buat fungsi untuk menginput 3 nilai milik `n` mahasiswa ke dalam `nilai[MAKS][3]`.
2. Buat fungsi `void hitungRata(int nilai[][3], float rata[], int n)` yang menghitung rata-rata dari 3 nilai tiap mahasiswa (`(Tugas + UTS + UAS) / 3.0`) dan menyimpannya ke array 1 dimensi `float rata[MAKS]`.
3. Tampilkan tabel rekapitulasi yang memuat Nomor Mahasiswa, nilai Tugas, UTS, UAS, dan Rata-ratanya secara sejajar.

**Contoh Eksekusi:**
```text
Masukkan jumlah mahasiswa: 3

Mahasiswa 1 (Tugas UTS UAS): 80 85 90
Mahasiswa 2 (Tugas UTS UAS): 70 75 65
Mahasiswa 3 (Tugas UTS UAS): 90 85 95

Mhs   Tugas   UTS   UAS   Rata-rata
-----------------------------------
 1      80     85    90       85.00
 2      70     75    65       70.00
 3      90     85    95       90.00
-----------------------------------
```

---

## Bagian B: Soal Bertingkat STRING (`#include <string.h>` Diperbolehkan)
*Tema Terhubung: Pembuatan Akun, Login, & Pemeriksa Kata*

### 🟢 Soal String 1 (Level Dasar): Pembuat Username & Cek Panjang Password
Buatlah program pendaftaran akun sederhana menggunakan fungsi pustaka `<string.h>` (`strcpy`, `strcat`, `strlen`):
1. Minta user menginput `namaDepan`, `namaBelakang`, dan `password` (masing-masing **1 kata tanpa spasi**).
2. Bentuk `username` secara otomatis dengan menggabungkan `namaDepan`, tanda garis bawah `"_"`, dan `namaBelakang` menggunakan `strcpy` serta `strcat`.
3. Hitung panjang karakter `password` menggunakan `strlen`:
   * Jika panjangnya **kurang dari 6 karakter**, tampilkan peringatan `"Password terlalu pendek! (Minimal 6 karakter)"`.
   * Jika **6 karakter atau lebih**, tampilkan `"Akun berhasil dibuat!"` beserta `username` dan panjang password-nya.

**Contoh Eksekusi:**
```text
Nama Depan    : Budi
Nama Belakang : Santoso
Password      : rahasia12

Username Anda    : Budi_Santoso
Panjang Password : 9 karakter
Status           : Akun berhasil dibuat!
```

---

### 🟡 Soal String 2 (Level Menengah): Simulasi Login Akun (`strcmp` & `strcmpi`)
Lanjutkan program dari **Soal String 1**! Setelah akun berhasil dibuat (`username` dan `password` sudah tersimpan), tambahkan fitur **Login**:
1. Minta user mengetikkan `inputUser` dan `inputPass`.
2. Periksa kecocokan `inputUser` dengan `username` secara **Non-Case Sensitive** menggunakan `strcmpi` (huruf besar/kecil diabaikan; mengetik `"budi_santoso"` tetap dianggap benar).
3. Periksa kecocokan `inputPass` dengan `password` secara **Case Sensitive** menggunakan `strcmp` (huruf besar/kecil wajib sama persis).
4. Tampilkan hasil login secara spesifik: **`Login Berhasil!`**, **`Username tidak ditemukan!`**, atau **`Password salah!`**.

**Contoh Eksekusi (lanjutan dari registrasi di atas):**
```text
=== SILAKAN LOGIN ===
Masukkan Username : budi_santoso
Masukkan Password : Rahasia12
Hasil             : Password salah! (Perhatikan huruf besar/kecil)
```

---

### 🔴 Soal String 3 (Level Lanjutan): Hitung Huruf Vokal & Cek Kata Palindrom
*Palindrom* adalah kata yang dibaca dari depan maupun belakang menghasilkan kata yang sama (contoh: `katak`, `malam`, `KasurRusak`).
Dengan memanfaatkan `#include <string.h>` dan fungsi buatan sendiri, buatlah program yang menerima **1 kata tanpa spasi**, lalu memprosesnya melalui 2 fungsi:
1. `int hitungVokal(char kata[])` — menghitung ada berapa banyak huruf vokal (`a, i, u, e, o`, baik huruf kecil maupun kapital) di dalam `kata[]` (boleh memakai bantuan `strlen` dan `strchr`).
2. `void balikKata(char asal[], char hasil[])` — mengisi `hasil[]` dengan susunan huruf terbalik dari `asal[]`.
3. Di dalam `main()`, tampilkan jumlah huruf vokalnya, hasil kata setelah dibalik, lalu gunakan **`strcmpi(kata, hasil)`** untuk menentukan apakah kata tersebut **PALINDROM** atau **BUKAN PALINDROM** (tanpa peduli huruf besar/kecil)!

**Contoh Eksekusi:**
```text
Masukkan sebuah kata : Malam
Jumlah huruf vokal   : 2
Kata setelah dibalik : malaM
Kesimpulan           : KATA PALINDROM!
```

---

## Bagian C: Tantangan Puncak (SOAL HOTS)
*Gabungan Materi: Array 1D + Array of String + `<string.h>` + Fungsi + Sorting + Searching*

### 🔥 Studi Kasus: Papan Peringkat & Pencarian Nilai Mahasiswa
Gabungkan konsep **Array** dan **String** ke dalam satu program untuk mengelola nama dan nilai ujian milik `n` mahasiswa (`#define MAKS 20`):

1. **Penyimpanan Data Berpasangan (Paralel):**
   * Simpan **nama panggilan** tiap mahasiswa (1 kata tanpa spasi) ke dalam array karakter 2 dimensi: `char nama[MAKS][30];`.
   * Simpan **nilai ujian** tiap mahasiswa ke dalam array integer 1 dimensi: `int nilai[MAKS];`.
2. **Fungsi Pengurutan Peringkat Paralel:**
   * Buat fungsi untuk mengurutkan daftar mahasiswa dari **nilai tertinggi ke nilai terendah (*descending*)**.
   * **Aturan Penting:** Setiap kali posisi angka `nilai[i]` dan `nilai[j]` ditukar, **nama pemiliknya (`nama[i]` dan `nama[j]`) WAJIB ikut ditukar** menggunakan `strcpy` agar nilai seorang mahasiswa tidak tertukar ke nama temannya!
3. **Tampilkan Papan Peringkat:**
   * Cetak tabel berisi Peringkat (`1` s/d `n`), Nama Mahasiswa, dan Nilainya.
4. **Fitur Pencarian Nama Mahasiswa:**
   * Setelah tabel tampil, minta user mengetikkan 1 nama panggilan yang ingin dicari.
   * Cari di dalam daftar menggunakan `strcmpi` (huruf besar/kecil diabaikan; mengetik `"edi"` tetap menemukan `"Edi"`).
   * Jika ditemukan, tampilkan ia berada di **Peringkat berapa** dan **berapa nilainya**. Jika tidak ditemukan, tampilkan **`Mahasiswa tidak ditemukan.`**.

**Contoh Eksekusi:**
```text
Masukkan jumlah mahasiswa: 4

Mhs 1 - Nama Panggilan : Ahmad
Mhs 1 - Nilai Ujian    : 85
Mhs 2 - Nama Panggilan : Dani
Mhs 2 - Nilai Ujian    : 70
Mhs 3 - Nama Panggilan : Edi
Mhs 3 - Nilai Ujian    : 92
Mhs 4 - Nama Panggilan : Budi
Mhs 4 - Nilai Ujian    : 78

=== PAPAN PERINGKAT KELAS ===
Rank   Nama          Nilai
--------------------------
 1     Edi              92
 2     Ahmad            85
 3     Budi             78
 4     Dani             70
--------------------------

Cari nama mahasiswa: ahmad
Ditemukan! Ahmad berada di Peringkat 2 dengan nilai 85.
```
