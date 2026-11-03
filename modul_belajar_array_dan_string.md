# Modul Belajar Materi: Array dan String (Bahasa C)

Dokumen ini merangkum inti konsep **Praktikum 18–19 (Array 1 & 2)** serta **Praktikum 21–22 (String 1 & 2 & `<string.h>`)** sebagai bekal teori sebelum mengerjakan:
* **Lembar Soal (Level Up):** [latihan_soal_array_string.md](./latihan_soal_array_string.md)
* **Panduan Dekomposisi & Gerakan:** [panduan_penyelesaian_dekomposisi.md](./panduan_penyelesaian_dekomposisi.md)

---

## Bagian 1: Ringkasan Konsep ARRAY (Praktikum 18 & 19)

### 1. Array 1D & 2D
* **Array 1 Dimensi:** Sekumpulan loker bertipe data **sama** dengan **nama variabel sama**, diakses dengan indeks mulai dari **`0` s/d `n - 1`**.
  ```c
  int skor[5];                   // Pesan 5 loker (indeks 0 s/d 4)
  int hari[] = {31, 28, 31, 30}; // Ukuran boleh kosong JIKA langsung diisi {}
  ```
* **Array 2 Dimensi (Tabel Baris × Kolom):** Indeks kiri adalah **baris**, indeks kanan adalah **kolom** (`int nilai[baris][kolom];`). Jika ukuran baris dikosongkan saat inisialisasi, **ukuran kolom kanan tetap wajib ditulis** (`int data[][3] = ...`).

### 2. Array sebagai Parameter Fungsi (*Alias*)
Mengirim array ke fungsi berarti mengirim **alamat memori aslinya (*alias*)**—setiap perubahan pada parameter di dalam fungsi otomatis mengubah array asli di `main()`.

| Posisi Penulisan | Contoh Array 1D | Contoh Array 2D | Aturan Penting |
| :--- | :--- | :--- | :--- |
| **1. Deklarasi di atas `main`** | `void urut(int []);` | `void cetak(int [][3]);` | Kurung pertama boleh kosong |
| **2. Pemanggilan di `main`** | `urut(skor);` | `cetak(nilai);` | **DILARANG pakai `[]` sama sekali!** |
| **3. Judul fungsi di bawah** | `void urut(int x[])` | `void cetak(int m[][3])` | Nama parameter bebas |

---

## Bagian 2: Ringkasan Konsep STRING & `<string.h>` (Praktikum 21 & 22)

### 1. Wujud Asli String di Memori
String di bahasa C adalah **Array 1D bertipe `char`** yang diakhiri karakter penanda berhenti **`'\0'` (NULL)**. Kata `"RINI"` (4 huruf) membutuhkan minimal `char nama[5]` (`'R'`, `'I'`, `'N'`, `'I'`, `'\0'`).

> [!CAUTION]
> **3 Aturan Emas String di Bahasa C:**
> 1. Setelah deklarasi, string **tidak boleh diisi dengan `=`** (`nama = "BUDI";` → error, wajib pakai `strcpy`).
> 2. Dua string **tidak boleh dibandingkan dengan `==`** (`nama == "BUDI"` → salah, wajib pakai `strcmp` atau `strcmpi`).
> 3. Pada `scanf("%s", teks);`, **tidak perlu tanda `&`** di depan nama array string.

### 2. Input Kalimat Ber-spasi (`fgets`) & Dua Trik Pentingnya
* `scanf("%s", teks)` hanya membaca **1 kata** (berhenti begitu bertemu spasi).
* Untuk membaca **kalimat penuh spasi secara aman**, gunakan `fgets(teks, sizeof(teks), stdin);`.
* **Trik 1 — Membuang sisa Enter (`'\n'`) bawaan `fgets`:**
  `fgets` ikut menyimpan tombol Enter `'\n'` di ujung kalimat sebelum `'\0'`. Potong dengan `strlen`:
  ```c
  int pjg = strlen(teks);
  if (pjg > 0 && teks[pjg - 1] == '\n') {
      teks[pjg - 1] = '\0';
  }
  ```
* **Trik 2 — Mencampur `scanf` angka lalu `fgets` kalimat:**
  Selalu panggil `getchar();` satu kali sesudah `scanf` sebelum memanggil `fgets`, agar sisa Enter dari `scanf` tidak langsung memakan giliran `fgets`!

### 3. Kode ASCII & Fungsi Pustaka `#include <string.h>`
* **Rentang ASCII:** Huruf besar `'A'`–`'Z'` (`65`–`90`), huruf kecil `'a'`–`'z'` (`97`–`122`), selisihnya **`32`**. Karakter angka `'0'`–`'9'` (`48`–`57`).

> [!WARNING]
> **Koreksi Salah Ketik Modul Praktikum 22 (Hal. 108):**
> Di modul tertulis `z = 112`, padahal kode ASCII yang benar untuk `'z'` adalah **`122`** (`90 + 32 = 122`). Lebih aman lagi, tulis langsung karakter berpetik satu di dalam kodemu seperti `c >= 'a' && c <= 'z'`.

| Fungsi `<string.h>` | Kegunaan | Catatan Penting |
| :--- | :--- | :--- |
| `strlen(s)` | Menghitung panjang karakter `s` | Karakter `'\0'` tidak ikut dihitung. |
| `strcpy(tujuan, asal)` | Menyalin isi `asal` ke `tujuan` | Menimpa isi lama di `tujuan`. |
| `strcat(tujuan, sumber)` | Menyambung `sumber` ke ekor `tujuan` | Pastikan ukuran `tujuan` cukup lebar! |
| `strcmp(s1, s2)` | Bandingkan *Case Sensitive* | Hasil **`0` artinya SAMA PERSIS**, `< 0` jika `s1 < s2`, `> 0` jika `s1 > s2`. |
| `strcmpi(s1, s2)` | Bandingkan *Non-Case Sensitive* | Mengabaikan perbedaan huruf besar & kecil (`0` jika sama). |
| `strchr(s, kar)` | Mencari karakter `kar` di dalam `s` | Menghasilkan `NULL` jika karakter tidak ditemukan. |

