# Materi 5

## E. Komputasi Determinan dengan Ekspansi Baris dan Invers Menggunakan Metode Adjoin

Pada bab ini, kita akan mendalami dua konsep fundamental dalam aljabar linear numerik, yaitu menghitung nilai determinan menggunakan metode ekspansi baris (kofaktor) serta mencari matriks invers melalui pendekatan adjoin. Kita akan menguji performa kedua metode ini pada berbagai variasi orde matriks, mulai dari ukuran $2 \times 2$, $3 \times 3$, hingga $4 \times 4$.

---

## Bagian 1: Perhitungan Determinan dengan Ekspansi Baris

Secara formal, perhitungan determinan menggunakan ekspansi kofaktor pada baris ke-$i$ dirumuskan sebagai berikut:

$$\det(A) = \sum_{k=1}^{n} (-1)^{i+k} a_{ik} M_{ik}$$

Di mana $a_{ik}$ merupakan elemen matriks pada baris ke-$i$ kolom ke-$k$, sedangkan $M_{ik}$ melambangkan nilai determinan minor setelah baris ke-$i$ dan kolom ke-$k$ dieliminasi dari matriks utama.

---

### Soal 1: Matriks Orde 2x2

Diberikan matriks $A$ berukuran $2 \times 2$ sebagai berikut:

$$A = \begin{pmatrix} -5 & -3 \\ 2 & 3 \end{pmatrix}$$

Untuk matriks ukuran $2 \times 2$, kita bisa langsung menerapkan perkalian silang antara diagonal utama dikurangi diagonal samping:

$$\det(A) = (-5)(3) - (-3)(2)$$
$$\det(A) = -15 - (-6) = -15 + 6 = -9$$

**Hasil Akhir:** $\det(A) = -9$

---

### Soal 2: Matriks Orde 3x3

Diberikan matriks $B$ berukuran $3 \times 3$ dengan struktur elemen berikut:

$$B = \begin{pmatrix} 0 & 3 & -2 \\ 1 & -3 & -1 \\ 0 & 0 & 2 \end{pmatrix}$$

Untuk mengefisiensikan waktu komputasi, kita pilih ekspansi kofaktor pada **baris ke-3**, karena baris ini memuat elemen nol terbanyak sehingga kita hanya perlu menghitung satu sub-matriks minor:

$$\det(B) = 0 \cdot C_{31} + 0 \cdot C_{32} + 2 \cdot C_{33}$$
$$\det(B) = 2 \cdot (-1)^{3+3} \begin{vmatrix} 0 & 3 \\ 1 & -3 \end{vmatrix}$$
$$\det(B) = 2 \cdot 1 \cdot ((0)(-3) - (3)(1))$$
$$\det(B) = 2 \cdot (0 - 3) = -6$$

**Hasil Akhir:** $\det(B) = -6$ 

### Soal 3: Matriks Orde 4x4

Diberikan matriks $C$ berukuran $4 \times 4$ dengan pola elemen simetris sebagai berikut:

$$C = \begin{pmatrix} 2 & -2 & 0 & 0 \\ -2 & 2 & 0 & 0 \\ 0 & 0 & 3 & -3 \\ 0 & 0 & -3 & 3 \end{pmatrix}$$

Apabila kita lakukan analisis struktur pada matriks $C$, terlihat bahwa penjumlahan elemen pada baris pertama dan baris kedua menghasilkan vektor nol jika kita mengalikan matriks ini dengan vektor kolom basis yang tepat. Secara matematis, jika matriks $C$ dikalikan dengan vektor kolom berisi angka 1, kita mendapatkan:

$$
C \cdot \begin{pmatrix} 1 \\ 1 \\ 1 \\ 1 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \\ 0 \\ 0 \end{pmatrix}
$$

Kondisi di atas menunjukkan bahwa matriks memiliki ketergantungan linear antar barisnya, yang berarti salah satu eigenvalue dari matriks ini bernilai 0. Berdasarkan sifat aljabar matriks, jika suatu matriks memiliki minimal satu eigenvalue bernilai nol, maka nilai determinan keseluruhan dari matriks tersebut secara otomatis adalah nol.

**Hasil Akhir:** $\det(C) = 0$

---

## Bagian 2: Invers Matriks dengan Metode Adjoin

Untuk mencari matriks invers menggunakan pendekatan adjoin, kita memanfaatkan hubungan antara nilai determinan utama dengan transpos dari matriks kofaktor:

$$A^{-1} = \frac{1}{\det(A)} \cdot \text{adj}(A)$$

Di mana komponen kofaktor $C_{ij}$ ditentukan oleh rumus: $C_{ij} = (-1)^{i+j} M_{ij}$.

---

### Soal 4: Invers Matriks Orde 2x2

Menggunakan matriks $A$ pada Soal 1: $A = \begin{pmatrix} -5 & -3 \\ 2 & 3 \end{pmatrix}, \quad \det(A) = -9$.

Untuk matriks $2 \times 2$, matriks adjoin diperoleh secara instan dengan menukar posisi elemen diagonal utama dan mengubah tanda visual elemen diagonal samping:

$$\text{adj}(A) = \begin{pmatrix} 3 & 3 \\ -2 & -5 \end{pmatrix}$$

Maka komponen inversnya adalah: $A^{-1} = -\frac{1}{9} \begin{pmatrix} 3 & 3 \\ -2 & -5 \end{pmatrix} = \begin{pmatrix} -3/9 & -3/9 \\ 2/9 & 5/9 \end{pmatrix} = \begin{pmatrix} -1/3 & -1/3 \\ 2/9 & 5/9 \end{pmatrix}$.

---

### Soal 5: Invers Matriks Orde 3x3

Menggunakan matriks $B$ pada Soal 2: $B = \begin{pmatrix} 0 & 3 & -2 \\ 1 & -3 & -1 \\ 0 & 0 & 2 \end{pmatrix}, \quad \det(B) = -6$.

Kita hitung seluruh sembilan elemen kofaktor $C_{ij}$ secara manual:

* $C_{11} = +((-3)(2) - (-1)(0)) = -6$
* $C_{12} = -((1)(2) - (-1)(0)) = -2$
* $C_{13} = +((1)(0) - (-3)(0)) = 0$
* $C_{21} = -((3)(2) - (-2)(0)) = -6$
* $C_{22} = +((0)(2) - (-2)(0)) = 0$
* $C_{23} = -((0)(0) - (3)(0)) = 0$
* $C_{31} = +((3)(-1) - (-2)(-3)) = -3 - 6 = -9$
* $C_{32} = -((0)(-1) - (-2)(1)) = -(0 + 2) = -2$
* $C_{33} = +((0)(-3) - (3)(1)) = -3$

Kita susun matriks kofaktor $C$, kemudian kita lakukan operasi transpos untuk mendapatkan matriks adjoin:

$$\text{adj}(B) = C^T = \begin{pmatrix} -6 & -6 & -9 \\ -2 & 0 & -2 \\ 0 & 0 & -3 \end{pmatrix}$$

Langkah terakhir, kalikan matriks adjoin dengan skalar seper-determinan:

$$B^{-1} = -\frac{1}{6} \begin{pmatrix} -6 & -6 & -9 \\ -2 & 0 & -2 \\ 0 & 0 & -3 \end{pmatrix} = \begin{pmatrix} 1 & 1 & 3/2 \\ 1/3 & 0 & 1/3 \\ 0 & 0 & 1/2 \end{pmatrix}$$

### Soal 6: Invers Matriks Orde 4x4

Menggunakan matriks $C$ pada Soal 3:

$$C = \begin{pmatrix} 2 & -2 & 0 & 0 \\ -2 & 2 & 0 & 0 \\ 0 & 0 & 3 & -3 \\ 0 & 0 & -3 & 3 \end{pmatrix}, \quad \det(C) = 0$$

Berdasarkan hasil kalkulasi pada bagian pertama, nilai determinan matriks $C$ adalah nol. Dalam terminologi aljabar linear, matriks dengan determinan nol dikategorikan sebagai matriks singular. Karena rumus invers melibatkan pembagian dengan nilai determinan, maka operasi tersebut tidak dapat didefinisikan.

**Kesimpulan:** Matriks $C$ tidak memiliki matriks invers ($C^{-1}$ tidak ada).

---

## Verifikasi Menggunakan Skrip Python (NumPy)

Untuk menguji ketepatan hasil perhitungan manual di atas, kita bisa menjalankan fungsi invers dan determinan dari pustaka NumPy lewat kode berikut:

import numpy as np

# Definisi Matriks Soal 2x2 dan 3x3
A = np.array([[-5, -3],
              [ 2,  3]])

B = np.array([[ 0,  3, -2],
              [ 1, -3, -1],
              [ 0,  0,  2]])

print("--- VERIFIKASI MATRIKS A ---")
print(f"Determinan A : {np.linalg.det(A):.1f}")
print(f"Invers A :\n{np.linalg.inv(A)}\n")

print("--- VERIFIKASI MATRIKS B ---")
print(f"Determinan B : {np.linalg.det(B):.1f}")
print(f"Invers B :\n{np.linalg.inv(B)}")
