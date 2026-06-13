# Materi 6

## F. Transformasi Matriks dan Implementasi Mesin Vektor 2D

Materi keenam ini berfokus pada salah satu implementasi paling krusial dari aljabar linear dalam dunia ilmu komputer, yaitu transformasi geometri. Proses ini merupakan fondasi dasar yang digunakan dalam engine game, grafika komputer, dan pengolahan citra digital untuk memanipulasi posisi, orientasi, serta skala dari suatu objek visual.

---

## 1. Konsep Dasar Transformasi Matriks

Secara umum, transformasi matriks merupakan sebuah mekanisme pemetaan koordinat ruang vektor awal menuju koordinat ruang vektor yang baru menggunakan operasi perkalian matriks linear. Formula matematisnya ditulis sebagai berikut:

$$\mathbf{y} = A\mathbf{x}$$

Di mana komponen pembentuknya adalah:
* **$A$** melambangkan matriks transformasi linear yang bertindak sebagai operator balik.
* **$\mathbf{x}$** melambangkan vektor kolom dari titik koordinat awal sebelum proses perubahan.
* **$\mathbf{y}$** melambangkan vektor kolom dari titik koordinat baru hasil keluaran transformasi.

---

## 2. Mekanisme Refleksi Terhadap Sumbu Y

Refleksi atau pencerminan adalah jenis transformasi isometri yang membalikkan posisi objek melintasi suatu garis sumbu acuan. Dalam ruang kartesius dua dimensi (2D), operasi pencerminan terhadap Sumbu Y akan mengakibatkan nilai posisi pada sumbu X berbalik tanda (positif menjadi negatif atau sebaliknya), sedangkan nilai posisi vertikal pada sumbu Y tidak mengalami perubahan sama sekali.

Struktur matriks transformasi standar untuk operasi refleksi sumbu Y dinotasikan sebagai:

$$M_y = \begin{bmatrix} -1 & 0 \\ 0 & 1 \end{bmatrix}$$

---

## 3. Pembuktian Aljabar Linier pada Refleksi Sumbu Y

Jika kita memiliki sebuah vektor koordinat awal $\mathbf{x} = \begin{bmatrix} x \\ y \end{bmatrix}$ dan mengalikannya dengan matriks operator $M_y$, proses perhitungannya dapat dijabarkan secara linear:

$$\begin{bmatrix} x' \\ y' \end{bmatrix} = \begin{bmatrix} -1 & 0 \\ 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix}$$

Menggunakan prinsip operasi perkalian baris dikalikan dengan kolom, kita peroleh persamaan berikut:

$$\begin{bmatrix} x' \\ y' \end{bmatrix} = \begin{bmatrix} (-1 \cdot x) + (0 \cdot y) \\ (0 \cdot x) + (1 \cdot y) \end{bmatrix}$$

$$\begin{bmatrix} x' \\ y' \end{bmatrix} = \begin{bmatrix} -x \\ y \end{bmatrix}$$

Melalui pembuktian aljabar ini, terlihat jelas bahwa posisi spasial horizontal objek akan berpindah melintasi sumbu y secara simetris, sementara ketinggian atau posisi vertikalnya tetap konsisten.

---

## 4. Contoh Perhitungan Kasus Titik Tunggal

Sebagai simulasi awal, kita ambil contoh sebuah titik koordinat tunggal $K(2, 3)$. Kita akan mencari koordinat bayangan $K'$ setelah dikenakan operator refleksi sumbu Y.

Representasi vektor kolom dari titik mula-mula:
$$\mathbf{x} = \begin{bmatrix} 2 \\ 3 \end{bmatrix}$$

Maka hasil transformasinya adalah:
$$\mathbf{y} = \begin{bmatrix} -1 & 0 \\ 0 & 1 \end{bmatrix} \begin{bmatrix} 2 \\ 3 \end{bmatrix} = \begin{bmatrix} -2 \\ 3 \end{bmatrix}$$

Berdasarkan kalkulasi matriks di atas, titik $K(2, 3)$ secara akurat berpindah menuju koordinat baru $K'(-2, 3)$.
# 5. Implementasi Simultan pada Struktur Bangun Datar

Dalam arsitektur perangkat lunak grafis, pemrosesan objek tidak dilakukan per titik secara parsial, melainkan secara paralel menggunakan matriks koordinat gabungan. Kita akan menguji performa ini pada objek segitiga yang dibentuk oleh tiga titik sudut: $K(2,3)$, $L(5,3)$, dan $M(3,6)$.

Kita susun titik-titik tersebut ke dalam sebuah matriks koordinat $\mathbf{X}$ berukuran $2 \times 3$ di mana baris pertama menampung komponen koordinat X dan baris kedua menampung komponen koordinat Y:

$$\mathbf{X} = \begin{bmatrix} 2 & 5 & 3 \\ 3 & 3 & 6 \end{bmatrix}$$

Langkah berikutnya, kita kalikan matriks refleksi murni $\mathbf{M}_y$ dengan matriks koordinat gabungan $\mathbf{X}$:

$$\mathbf{Y} = \begin{bmatrix} -1 & 0 \\ 0 & 1 \end{bmatrix} \begin{bmatrix} 2 & 5 & 3 \\ 3 & 3 & 6 \end{bmatrix}$$

$$\mathbf{Y} = \begin{bmatrix} -2 & -5 & -3 \\ 3 & 3 & 6 \end{bmatrix}$$

Melalui satu kali operasi perkalian matriks di atas, komputer langsung mendapatkan seluruh koordinat bayangan baru untuk objek segitiga tersebut, yaitu pada titik $K'(-2,3)$, $L'(-5,3)$, dan $M'(-3,6)$.

---

# 6. Analisis Karakteristik Matriks Refleksi

* **Pemberbalikan Orientasi Ruang (Orientation Reversing):** Operasi pencerminan membalikkan urutan arah orientasi dari objek geometris. Jika orientasi titik asal dibaca searah jarum jam, maka objek hasil transformasi akan berbalik menjadi berlawanan arah jarum jam.
* **Nilai Determinan Negatif:** Matriks refleksi murni akan selalu menghasilkan nilai determinan sebesar $-1$. $\det(\mathbf{M}_y) = (-1)(1) - (0)(0) = -1$. Nilai negatif ini merupakan representasi aljabar bahwa orientasi spasial dari ruang vektor tersebut telah dibalik dari kondisi semulanya.
* **Sifat Isometri Luas:** Walaupun orientasi ruangnya berbalik, nilai mutlak atau absolut dari determinannya adalah $|-1| = 1$. Hal ini membuktikan bahwa transformasi ini bersifat isometri, yaitu hanya mengubah posisi objek tanpa melakukan distorsi bentuk, perubahan jarak antar titik, ataupun pengubahan total luas area pada bangun aslinya.

---

# Panduan Menjalankan Aplikasi: 2D Vector Engine (Reflection & Translation)

Bagian ini memuat dokumentasi teknis serta panduan operasional untuk menjalankan aplikasi interaktif berbasis desktop yang berfungsi sebagai simulator transformasi geometri linear.

## Deskripsi Sistem

Program ini merupakan aplikasi simulator grafis berbasis Python dengan antarmuka GUI yang dibangun menggunakan pustaka PyQt5 dan visualisasi grafik dari Matplotlib. Perangkat lunak ini dirancang untuk memproses transformasi geometri dua dimensi secara dinamis, yang meliputi fitur refleksi sumbu Y, translasi pergeseran posisi, serta manipulasi koordinat objek menggunakan teknik interaksi *drag and drop* langsung pada area plot kartesius.

## Kebutuhan Lingkungan Eksekusi

Sebelum mengeksekusi program utama, pastikan lingkungan komputasi lokal Anda telah memenuhi spesifikasi berikut:

* Interpreter Python versi 3.x atau yang lebih baru.
* Terminal konsol atau Command Prompt yang mendukung eksekusi skrip ekstern.
* Sistem operasi yang dilengkapi dengan subsistem Graphical User Interface (Windows, macOS, atau distribusi Linux berbasis desktop).

## Instalasi Dependensi Pustaka

Lakukan instalasi pustaka pihak ketiga yang dibutuhkan oleh engine simulator dengan menjalankan perintah berikut pada terminal Anda:

```bash
pip install numpy matplotlib PyQt5