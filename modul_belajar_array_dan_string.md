# Ringkasan Cepat (Cheat-Sheet): Array dan String (Bahasa C)

Dokumen ini adalah lembar contekan kilat (*cheat-sheet*) pendamping untuk:
1. **Buku Pegangan Materi (12 Kepingan Lego):** [buku_materi_lengkap_array_string.md](./buku_materi_lengkap_array_string.md)
2. **Lembar Latihan Soal:** [latihan_soal_array_string.md](./latihan_soal_array_string.md)
3. **Panduan Dekomposisi & Gerakan:** [panduan_penyelesaian_dekomposisi.md](./panduan_penyelesaian_dekomposisi.md)

---

## 1. Intisari ARRAY (Praktikum 18 & 19)

* **Array 1 Dimensi:** Deretan loker dengan nama dan tipe data yang wajib sama. Indeks selalu mulai dari **`0` s/d `n - 1`**.
  * Deklarasi: `int skor[50];` atau langsung diisi: `int hari[] = {31, 28, 31};`.
* **Array 2 Dimensi:** Tabel `[baris][kolom]`, contoh: `int nilai[20][3];` (`20` mahasiswa, `3` nilai ujian).
* **Aturan Parameter Fungsi (*Alias* Alamat Memori Sama):**

| Posisi Penulisan | Array 1D | Array 2D | Aturan Wajib |
| :--- | :--- | :--- | :--- |
| **Deklarasi atas** | `void urut(int [], int);` | `void rata(int [][3], int);` | Kolom kanan 2D wajib ditulis |
| **Pemanggilan di `main`** | `urut(skor, n);` | `rata(nilai, n);` | **DILARANG menulis `[]`!** |
| **Judul fungsi bawah** | `void urut(int x[], int n)` | `void rata(int m[][3], int n)` | Mengubah `x`/`m` otomatis mengubah array asli |

* **Rumus Wajib Diingat:**
  * Rata-rata desimal dari `int total`: `float rata = (float)total / n;`
  * Patokan awal nilai terbesar: ambil dari data pertama (`skor[0]`), jangan tebak `0` atau `1`.
  * Tukar 2 elemen saat *sorting*: `temp = x[i];` → `x[i] = x[j];` → `x[j] = temp;`.

---

## 2. Intisari STRING & `<string.h>` (Praktikum 21 & 22)

* **Wujud String di Memori:** Array `char` yang wajib diakhiri karakter penutup **`'\0'` (NULL)**. Kata `"RINI"` (4 huruf) minimal butuh `char nama[5];`.
* **Input 1 Kata Tanpa Spasi:** `scanf("%s", nama);` *(tanpa tanda `&`!)*.
* **Input Kalimat Ber-spasi:** `fgets(kalimat, sizeof(kalimat), stdin);`.
* **Daftar Nama Banyak Orang (*Array of String*):** `char nama[MAKS][30];` → cukup panggil 1 kurung siku **`nama[i]`** untuk mengakses seluruh nama orang ke-`i`.

> [!CAUTION]
> **Larangan Utama pada String:**
> * Dilarang mengisi ulang string dengan `=` (`nama = "Budi";` → salah, gunakan `strcpy`).
> * Dilarang membandingkan isi string dengan `==` (`nama == "Budi"` → salah, gunakan `strcmp` / `strcmpi`).

### Tabel Fungsi Pustaka `#include <string.h>`

| Fungsi | Kegunaan | Contoh & Catatan Penting |
| :--- | :--- | :--- |
| `strlen(s)` | Panjang huruf `s` | `int p = strlen("PENS");` → `4` (`'\0'` tidak dihitung). |
| `strcpy(tujuan, asal)` | Menyalin string | `strcpy(user, depan);` (pengganti tanda `=`). |
| `strcat(tujuan, tambah)` | Menyambung ke belakang | `strcat(user, "_");` (pastikan wadah `tujuan` cukup lebar). |
| `strcmp(s1, s2)` | Bandingkan (*Case Sensitive*) | **`== 0` artinya SAMA PERSIS** (`"Abc"` beda dengan `"abc"`). |
| `strcmpi(s1, s2)` | Bandingkan (*Non-Case Sensitive*) | **`== 0` artinya SAMA** (`"Abc"` dianggap sama dengan `"abc"`). |
| `strchr(daftar, kar)` | Cari 1 huruf di dalam string | `strchr("aiueo", c) != NULL` artinya huruf `c` ditemukan! |

> [!WARNING]
> **Catatan Kode ASCII (Koreksi Modul Hal. 108):**
> Huruf kapital `'A'`–`'Z'` bernilai `65`–`90`, sedangkan huruf kecil `'a'`–`'z'` bernilai `97`–`122` (bukan `112` seperti salah ketik di modul; selisih besar & kecil selalu `32`).
