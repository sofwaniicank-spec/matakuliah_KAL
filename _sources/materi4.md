# Materi 4

## D. Teori Fundamental dan Fondasi Sistem Persamaan Linear

Sebelum melakukan komputasi tingkat lanjut menggunakan operasi baris elementer, kita perlu memahami terlebih dahulu karakteristik struktur aljabar dari Sistem Persamaan Linear (SPL). Pemahaman teori ini penting agar kita dapat menentukan efisiensi algoritma pemrograman saat menyelesaikan masalah multivariabel.

---

## Konsep Dasar Persamaan Linear

Secara matematis, persamaan linear dengan $n$ jumlah variabel $(x_1, x_2, \dots, x_n)$ merupakan sebuah persamaan yang dapat dikonversi ke dalam format baku berikut:

$$a_1x_1 + a_2x_2 + \dots + a_nx_n = b$$

Dalam pemodelan data, kita membagi komponen di atas menjadi tiga bagian utama:

* **Variabel / Peubah:** Elemen $x_1, x_2, \dots, x_n$ merupakan nilai tidak diketahui yang ingin dicari oleh sistem komputer.
* **Koefisien:** Nilai $a_1, a_2, \dots, a_n$ adalah konstanta atau bilangan riil tetap yang terikat langsung di depan variabel.
* **Konstanta Ruas Kanan:** Nilai $b$ merupakan konstanta riil murni hasil dari persamaan.

---

## Klasifikasi Berdasarkan Sifat Persamaan

Kita dapat mengelompokkan persamaan matematika ke dalam beberapa kategori berdasarkan perilaku variabel dan nilai konstanta ruas kanannya:

1. **Sistem Homogen:** Terjadi apabila nilai konstanta di ruas kanan sama dengan nol ($b = 0$).
2. **Sistem Non-Homogen:** Terjadi apabila nilai konstanta di ruas kanan tidak sama dengan nol ($b \neq 0$).
3. **Persamaan Non-Linear:** Kondisi di mana suatu persamaan gagal memenuhi syarat linearitas. Ciri utamanya adalah adanya variabel yang memiliki pangkat selain satu (misal: $x_1^2$), adanya operasi perkalian silang antar variabel bebas (misal: $x_1x_2$), atau variabel tersebut terjebak di dalam fungsi transenden/non-polinomial seperti $\sin(x)$, $\ln(x)$, maupun $e^x$.

---

## Karakteristik dan Sifat Solusi SPL

Sistem Persamaan Linear (SPL) adalah gabungan terstruktur dari beberapa persamaan linear. Ditinjau dari sudut pandang geometris maupun analisis numerik, sebuah SPL selalu terikat pada salah satu dari tiga kemungkinan sifat solusi di bawah ini:

1. **Sistem Tidak Konsisten (Inconsistent System):** Sistem persamaan yang sama sekali tidak memiliki solusi. Secara visual geometri, garis-garis persamaan di dalam ruang tidak pernah saling berpotongan atau bergerak secara sejajar.
2. **Sistem Konsisten Solusi Tunggal (Unique Solution):** Sistem persamaan yang memiliki tepat satu pasang nilai variabel yang valid. Kondisi ini terpenuhi jika garis-garis persamaan saling berilangan di satu titik potong koordinat yang spesifik.
3. **Sistem Konsisten Solusi Tak Hingga (Infinite Solutions):** Sistem persamaan yang memiliki banyak sekali penyelesaian. Hal ini biasanya terjadi jika garis persamaan saling berhimpit satu sama lain, sehingga setiap titik di sepanjang garis merupakan solusi yang valid.

---

## Formulasi Berbasis Struktur Matriks

Untuk mempermudah pemrosesan paralel oleh memori komputer, sekumpulan persamaan linear diubah ke dalam bentuk representasi matriks $[A \mid b]$:

* **Matriks Koefisien ($A$):** Wadah dua dimensi berukuran $m \times n$ untuk menyimpan seluruh angka koefisien variabel dari sistem persamaan.
* **Vektor Konstanta ($b$):** Vektor kolom berukuran $m \times 1$ untuk menampung seluruh nilai di ruas kanan persamaan.
* **Matriks Augmented ($[A \mid b]$):** Matriks gabungan yang menempelkan vektor $b$ di sebelah kanan matriks $A$. Matriks augmented inilah yang menjadi objek utama saat mengeksekusi algoritma reduksi baris.

---

## Otomatisasi Komputasi Menggunakan SageMath

Selain menggunakan pustaka NumPy pada Python, kita juga bisa memanfaatkan SageMath untuk melakukan analisis simbolik dan manipulasi struktur matriks aljabar secara instan. Berikut adalah contoh sintaks implementasi konkret pada SageMath untuk membentuk sebuah matriks augmented:

## SageMath Cell Interaktif

Kamu bisa langsung mencoba dan memodifikasi sintaks SageMath di bawah ini. Silakan klik tombol **"Evaluate"** untuk melihat hasil komputasinya secara langsung:

```python
# Ketik atau modifikasi kode SageMath kamu di sini
A = matrix(QQ, 3, 3, [[2, 1, -1], [1, 3, 2], [-1, 1, 3]])
b = matrix(QQ, 3, 1, [[8], [13], [4]])
M = A.augment(b)
M.subdivide([], [3])
show(M)