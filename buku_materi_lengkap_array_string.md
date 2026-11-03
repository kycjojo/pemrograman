# Buku Pegangan Mandiri: Menguasai Array & String dari Nol Sampai HOTS

Selamat datang! Dokumen ini dirancang khusus sebagai **bekal lengkap sebelum kamu mengerjakan [latihan_soal_array_string.md](./latihan_soal_array_string.md)**.

Soal pemrograman sebenarnya hanyalah **gabungan dari beberapa pola kecil (seperti menyusun kepingan Lego)**. Di buku ini, kamu cukup mempelajari **12 Pola Koding ("Kepingan Lego")** menggunakan contoh sederhana. Jika kamu memahami ke-12 kepingan ini secara berurutan, kamu **pasti bisa** menyelesaikan seluruh soal latihan hingga soal HOTS!

---

## Bab 1: Menguasai Array 1 Dimensi (Deretan Loker)

Bayangkan **Array 1 Dimensi** sebagai satu baris loker bernomor. Semua loker memiliki **nama variabel yang sama** dan **tipe data yang wajib sama** (misalnya `int` semua atau `float` semua).

### 🧩 Kepingan 1: Mengisi & Mencetak Array 1D dengan `for`
Di bahasa C, nomor loker (**indeks**) selalu dimulai dari **`0`**. Jika ada `n = 5` data, maka loker yang dipakai bernomor **`0, 1, 2, 3, 4`** (berhenti di `n - 1`).

```c
#include <stdio.h>
#define MAKS 50 // Kapasitas maksimal loker (tanpa tanda = dan tanpa ;)

int main() {
    int tinggi[MAKS], n;

    printf("Masukkan banyak orang: ");
    scanf("%d", &n);

    // 1. Mengisi loker satu per satu (0 s/d n-1)
    for (int i = 0; i < n; i++) {
        printf("Tinggi ke-%d: ", i + 1); // +1 agar tampilan ke user mulai dari 1
        scanf("%d", &tinggi[i]);
    }

    // 2. Menampilkan kembali seluruh isi loker dalam satu baris
    printf("Daftar tinggi: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", tinggi[i]);
    }
    return 0;
}
```

---

### 🧩 Kepingan 2: Celengan `total = 0` & Pembagian Koma `(float)`
Untuk menghitung rata-rata, siapkan variabel penampung `total` yang **wajib dimulai dari `0`**.
Hati-hati: di bahasa C, membagi sesama bilangan bulat (`int / int`) akan **membuang angka di belakang koma** (`7 / 2` menjadi `3`, bukan `3.5`)!

```c
int total = 0; // WAJIB = 0 agar tidak tercampur angka sampah memori!
for (int i = 0; i < n; i++) {
    total = total + tinggi[i];
}

// Tambahkan (float) di depan agar hasil baginya memiliki desimal:
float rata = (float)total / n;
printf("Rata-rata: %.2f\n", rata); // %.2f = tampilkan 2 angka di belakang koma
```

---

### 🧩 Kepingan 3: Mencari Nilai Terbesar dengan Aman
Jangan pernah menebak nilai awal seperti `terbesar = 0` atau `terbesar = 1` (karena akan salah jika semua datanya bernilai negatif/nol). Jadikan **isi loker pertama (`indeks 0`)** sebagai juara sementara!

```c
int terbesar;

for (int i = 0; i < n; i++) {
    printf("Tinggi ke-%d: ", i + 1);
    scanf("%d", &tinggi[i]);

    // Saat data pertama (i == 0), langsung angkat jadi 'terbesar'.
    // Untuk data berikutnya, baru bandingkan apakah lebih besar.
    if (i == 0 || tinggi[i] > terbesar) {
        terbesar = tinggi[i];
    }
}
printf("Tinggi terbesar: %d\n", terbesar);
```

---

## Bab 2: Fungsi Berparameter Array & Sorting

### 🧩 Kepingan 4: Mengirim Array ke Fungsi (`void` vs `return`)
* Pakai **`void`** jika fungsi bertugas mengisi, mengurutkan, atau menampilkan isi array.
* Pakai **`int` / `float` + `return`** jika fungsi bertugas menghitung dan mengembalikan **1 angka hasil** ke `main()`.

Perhatikan **3 tempat penulisan array** agar tidak terjadi *error* atau *Segmentation Fault*:

```c
#include <stdio.h>
#define MAKS 50

// 1. DEKLARASI DI ATAS MAIN: pakai [] kosong
void isiData(int [], int);
int cariTerbesar(int [], int);

int main() {
    int berat[MAKS], n = 3;

    // 2. SAAT DIPANGGIL DI MAIN: Tulis NAMA ARRAY-nya saja TANPA []!
    isiData(berat, n);
    int juara = cariTerbesar(berat, n);

    printf("Berat terbesar: %d\n", juara);
    return 0;
}

// 3. JUDUL FUNGSI DI BAWAH: pakai [] kosong dengan nama alias bebas (misal x[])
void isiData(int x[], int n) {
    for (int i = 0; i < n; i++) {
        scanf("%d", &x[i]); // Mengubah x[i] otomatis mengubah berat[i] di main!
    }
}

int cariTerbesar(int x[], int n) {
    int maks = x[0];
    for (int i = 1; i < n; i++) {
        if (x[i] > maks) {
            maks = x[i];
        }
    }
    return maks; // Kembalikan 1 angka hasil ke main()
}
```

> [!WARNING]
> **Jangan Samakan Nama `#define` dengan Nama Fungsi/Variabel!**
> Jika kamu memakai `#define max 50`, jangan membuat fungsi bernama `max(...)` karena namanya akan tabrakan! Biasakan menulis konstanta dengan huruf kapital semua seperti `#define MAKS 50`.

---

### 🧩 Kepingan 5: Mengurutkan Array (*Sorting*) & Tukar 3 Gelas (`temp`)
Bayangkan jari kiri `i` menjaga kursi depan, sedangkan jari kanan `j` mengecek kursi-kursi di sebelah kanannya (`j = i + 1`). Jika urutannya terbalik, tukar isinya melewati wadah sementara `temp`:

```c
void urutTurun(int x[], int n) {
    int temp;
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            // Pakai (x[i] > x[j]) untuk urut KECIL ke BESAR (Ascending)
            // Pakai (x[i] < x[j]) untuk urut BESAR ke KECIL (Descending)
            if (x[i] < x[j]) {
                temp = x[i];
                x[i] = x[j];
                x[j] = temp;
            }
        }
    }
}
```
* **Bonus praktis:** Setelah diurutkan dari besar ke kecil (*descending*), nilai **tertinggi** otomatis berada di loker paling depan (**`x[0]`**), dan nilai **terendah** otomatis berada di loker paling belakang (**`x[n - 1]`**)!

---

## Bab 3: Menguasai Array 2 Dimensi (Tabel Baris × Kolom)

Array 2D berbentuk tabel: **`tabel[baris][kolom]`**.
Misalnya mencatat penjualan 3 cup minuman (kolom `0, 1, 2`) selama `n` hari (baris `0 .. n-1`): `int jual[MAKS][3];`.

### 🧩 Kepingan 6: Input Tabel 2D & Mengirimnya ke Fungsi
Saat mengirim Array 2D ke fungsi, **angka kolom kanan wajib ditulis** (`int m[][3]`):

```c
void inputTabel(int m[][3], int n) {
    for (int i = 0; i < n; i++) {
        printf("Hari ke-%d (Kopi Teh Susu): ", i + 1);
        // Membaca 3 angka yang diketik sebaris dipisah spasi:
        scanf("%d %d %d", &m[i][0], &m[i][1], &m[i][2]);
    }
}
```

---

### 🧩 Kepingan 7: Menghitung Rata-Rata per Baris & Cetak Tabel Rapi
Untuk menghitung rata-rata tiap baris `i`, jumlahkan ketiga kolom pada baris tersebut lalu bagi dengan **`3.0`** (pakai `.0` agar hasilnya desimal!).
Saat mencetak tabel, gunakan angka lebar ruangan seperti `%6d` dan `%10.2f` agar kolomnya lurus sejajar, dan letakkan `\n` **hanya di paling ujung kanan**:

```c
void hitungRataBaris(int m[][3], float rata[], int n) {
    for (int i = 0; i < n; i++) {
        rata[i] = (m[i][0] + m[i][1] + m[i][2]) / 3.0;
    }
}

void cetakTabel(int m[][3], float rata[], int n) {
    printf("Hari    Kopi    Teh   Susu   Rata-rata\n");
    printf("--------------------------------------\n");
    for (int i = 0; i < n; i++) {
        printf("%3d   %6d %6d %6d   %9.2f\n",
               i + 1, m[i][0], m[i][1], m[i][2], rata[i]);
    }
}
```

---

## Bab 4: Menguasai String & Pustaka `<string.h>`

Di bahasa C, **String adalah array `char` yang diakhiri karakter penutup `'\0'` (NULL)**.
Kata `"PENS"` (4 huruf) membutuhkan minimal 5 kotak memori: `'P'`, `'E'`, `'N'`, `'S'`, `'\0'`.

> [!CAUTION]
> **3 Aturan Emas String di Bahasa C:**
> 1. Pada `scanf("%s", teks);`, **tidak perlu tanda `&`** di depan nama variabel string.
> 2. String **tidak bisa diisi dengan `=`** sesudah deklarasi (`teks = "Halo";` → error! Gunakan `strcpy`).
> 3. String **tidak bisa dibandingkan dengan `==`** (`teks == "Halo"` → salah! Gunakan `strcmp` atau `strcmpi`).

---

### 🧩 Kepingan 8: Merakit & Mengukur String (`strcpy`, `strcat`, `strlen`)
Gunakan `#include <string.h>` di bagian atas program untuk memakai fungsi-fungsi praktis ini:

```c
#include <stdio.h>
#include <string.h>

int main() {
    char depan[25] = "Andi";
    char belakang[25] = "Wijaya";
    char akun[55]; // Pastikan ukurannya cukup besar untuk gabungan!

    // 1. strcpy(tujuan, asal): Menyalin kata pertama ke wadah tujuan
    strcpy(akun, depan);        // Isi 'akun' sekarang: "Andi"

    // 2. strcat(tujuan, tambahan): Menyambung teks ke bagian ekor tujuan
    strcat(akun, "_");          // Isi 'akun' sekarang: "Andi_"
    strcat(akun, belakang);     // Isi 'akun' sekarang: "Andi_Wijaya"

    // 3. strlen(teks): Menghitung panjang karakter (tanpa menghitung '\0')
    int panjang = strlen(akun); // Hasilnya: 11

    printf("Akun: %s (%d karakter)\n", akun, panjang);
    return 0;
}
```

---

### 🧩 Kepingan 9: Membandingkan Dua String (`strcmp` vs `strcmpi`)
* **`strcmp(s1, s2)`** → Membandingkan secara **Case Sensitive** (huruf besar dan kecil dianggap **BERBEDA**, cocok untuk *password*).
* **`strcmpi(s1, s2)`** → Membandingkan secara **Non-Case Sensitive** (huruf besar dan kecil dianggap **SAMA**, cocok untuk *username* atau pencarian nama).

> [!IMPORTANT]
> **Ingat Hasilnya Terbalik dari Dugaan Biasa!**
> `strcmp` dan `strcmpi` menghitung **selisih** kode huruf kedua kata. Jika kedua kata **sama persis**, selisihnya adalah **`0`**!
> * `strcmp(a, b) == 0` → Kedua kata **SAMA**.
> * `strcmp(a, b) != 0` → Kedua kata **BERBEDA**.

```c
if (strcmpi(inputUser, "Andi_Wijaya") == 0) {
    // Mengetik "andi_wijaya" atau "ANDI_WIJAYA" tetap masuk ke sini!
    if (strcmp(inputPass, "Kunci123") == 0) {
        // Password wajib persis "Kunci123"
        printf("Login Berhasil!\n");
    } else {
        printf("Password salah!\n");
    }
} else {
    printf("Username tidak ditemukan!\n");
}
```

---

### 🧩 Kepingan 10: Cek Karakter (`strchr`) & Membalik Kata (`\0`)
1. **Mengecek apakah 1 huruf termasuk kelompok tertentu dengan `strchr`:**
   Fungsi `strchr(daftarHuruf, kar)` mencari apakah karakter `kar` ada di dalam `daftarHuruf`. Jika **ketemu**, hasilnya **`!= NULL`**.
2. **Membalik susunan kata ke array lain:**
   Ambil huruf dari belakang (`pjg - 1 - i`), lalu **wajib pasang penutup `'\0'`** di ujung akhir!

```c
// Contoh 1: Menghitung berapa huruf vokal di dalam sebuah kata
int hitungVokal(char kata[]) {
    int jumlah = 0;
    int pjg = strlen(kata);
    for (int i = 0; i < pjg; i++) {
        // Cek apakah kata[i] ada di dalam "aiueoAIUEO"
        if (strchr("aiueoAIUEO", kata[i]) != NULL) {
            jumlah++;
        }
    }
    return jumlah;
}

// Contoh 2: Membalik kata (misal "Buku" -> "ukuB")
void balikKata(char asal[], char hasil[]) {
    int pjg = strlen(asal);
    for (int i = 0; i < pjg; i++) {
        hasil[i] = asal[pjg - 1 - i]; // Ambil huruf dari belakang
    }
    hasil[pjg] = '\0'; // WAJIB: pasang segel penutup string!
}
```

---

## Bab 5: Menggabungkan Array & String (Senjata Penakluk HOTS!)

### 🧩 Kepingan 11: *Array of String* & Pengurutan Paralel
Untuk menyimpan daftar nama banyak orang (masing-masing maksimal 29 huruf + `'\0'`), gunakan Array 2D `char`:
```c
char daftarNama[MAKS][30];
```
**Kemudahannya:** Cukup tulis **1 kurung siku `daftarNama[i]`**, maka itu sudah dianggap sebagai **1 string nama utuh milik orang ke-`i`** (`scanf("%s", daftarNama[i]);`)!

Jika setiap orang di `daftarNama[i]` juga punya angka `skor[i]`, maka saat mengurutkan skor, **namanya juga wajib ikut ditukar memakai `strcpy`** agar pemilik skor tidak tertukar:

```c
int tempSkor;
char tempNama[30];

for (int i = 0; i < n - 1; i++) {
    for (int j = i + 1; j < n; j++) {
        if (skor[i] < skor[j]) { // Urut menurun dari skor tertinggi
            // 1. Tukar angkanya memakai =
            tempSkor = skor[i];
            skor[i] = skor[j];
            skor[j] = tempSkor;

            // 2. Tukar string namanya memakai 3 langkah strcpy!
            strcpy(tempNama, daftarNama[i]);
            strcpy(daftarNama[i], daftarNama[j]);
            strcpy(daftarNama[j], tempNama);
        }
    }
}
```
*(Tips tampilan tabel: gunakan `%-14s` pada `printf` untuk mencetak `daftarNama[i]` rata kiri selebar 14 karakter agar kolom angkanya tetap lurus rapi!)*

---

### 🧩 Kepingan 12: Mencari Nama dengan Bendera `ketemu`
Saat mencari nama di dalam daftar, jangan menaruh pesan `"Tidak ditemukan"` di dalam `else` milik `for`! Gunakan variabel penanda `ketemu = 0`:

```c
int ketemu = 0; // Awalnya anggap belum ketemu

for (int i = 0; i < n; i++) {
    if (strcmpi(daftarNama[i], dicari) == 0) { // Cocok walau beda besar/kecil huruf
        printf("Ditemukan! %s ada di urutan ke-%d (Skor: %d)\n",
               daftarNama[i], i + 1, skor[i]);
        ketemu = 1; // Tandai sudah ketemu!
        break;      // Hentikan pencarian
    }
}

// Periksa di LUAR loop:
if (ketemu == 0) {
    printf("Nama tidak ditemukan.\n");
}
```

---

## Peta Kesiapan Latihan: Kepingan Mana Dipakai di Soal Mana?

Lihat betapa ringkasnya—seluruh soal di [latihan_soal_array_string.md](./latihan_soal_array_string.md) tersusun murni dari ke-12 kepingan di atas:

| Nomor Soal di Lembar Latihan | Kepingan Lego yang Digunakan |
| :--- | :--- |
| **🟢 Soal Array 1** | Kepingan **1** + **2** + **3** |
| **🟡 Soal Array 2** | Kepingan **4** + **5** |
| **🔴 Soal Array 3** | Kepingan **4** + **6** + **7** |
| **🟢 Soal String 1** | Kepingan **8** (`strcpy`, `strcat`, `strlen`) |
| **🟡 Soal String 2** | Kepingan **8** + **9** (`strcmp`, `strcmpi`) |
| **🔴 Soal String 3** | Kepingan **9** + **10** (`strchr` & membalik kata) |
| **🔥 SOAL HOTS** | Kepingan **5** + **11** + **12** |

Selamat mencoba merakit kodemu! Gunakan [panduan_penyelesaian_dekomposisi.md](./panduan_penyelesaian_dekomposisi.md) sebagai pendamping langkah kerjamu jika diperlukan.
