# Materi 2

## B. Menyelesaikan Sistem Persamaan Linear 5x5 dengan Berbagai Metode

Setelah memahami dasar-dasar aljabar linear pada materi sebelumnya, sekarang kita akan masuk ke studi kasus yang lebih kompleks. Di halaman ini, kita akan menyelesaikan Sistem Persamaan Linear (SPL) berukuran $5 \times 5$ menggunakan tiga pendekatan berbeda: Eliminasi Gauss-Jordan, Aturan Cramer dengan pendekatan Matrix Determinant Lemma, dan Metode Adjoin.

Tujuan dari materi ini adalah untuk melihat bagaimana *computational logic* bekerja dalam menyelesaikan sistem persamaan berdimensi besar.

---

## Kasus Sistem Persamaan Linear 5x5

Berikut adalah sistem persamaan linear lima variabel $(x_1, x_2, x_3, x_4, x_5)$ yang akan kita selesaikan:

$$
\begin{cases}
3x_1 + x_2 + x_3 + x_4 + x_5 = 4 \\
x_1 + 3x_2 + x_3 + x_4 + x_5 = 5 \\
x_1 + x_2 + 3x_3 + x_4 + x_5 = 6 \\
x_1 + x_2 + x_3 + 3x_4 + x_5 = 7 \\
x_1 + x_2 + x_3 + x_4 + 3x_5 = 8
\end{cases}
$$

Jika kita representasikan ke dalam bentuk matriks augmented $[A \mid B]$, susunannya adalah sebagai berikut:

$$
\begin{bmatrix}
3 & 1 & 1 & 1 & 1 & \mid & 4 \\
1 & 3 & 1 & 1 & 1 & \mid & 5 \\
1 & 1 & 3 & 1 & 1 & \mid & 6 \\
1 & 1 & 1 & 3 & 1 & \mid & 7 \\
1 & 1 & 1 & 1 & 3 & \mid & 8
\end{bmatrix}
$$

---

## Metode 1: Eliminasi Gauss-Jordan Step-by-Step

Kita akan mengubah matriks augmented di atas menjadi bentuk eselon baris terreduksi (di mana matriks koefisien sebelah kiri berubah menjadi matriks identitas) menggunakan Operasi Baris Elementer (OBE).

### Langkah 1: Membuat Pivot Utama pada Baris Pertama

Untuk mempermudah perhitungan, kita tukar Baris 1 ($R_1$) dengan Baris 2 ($R_2$) agar angka 1 naik ke atas menjadi pivot utama.  
* **Operasi:** $R_1 \leftrightarrow R_2$

$$
\begin{bmatrix}
1 & 3 & 1 & 1 & 1 & \mid & 5 \\
3 & 1 & 1 & 1 & 1 & \mid & 4 \\
1 & 1 & 3 & 1 & 1 & \mid & 6 \\
1 & 1 & 1 & 3 & 1 & \mid & 7 \\
1 & 1 & 1 & 1 & 3 & \mid & 8
\end{bmatrix}
$$

### Langkah 2: Eliminasi Kolom Pertama di Bawah Pivot

Kita nolkan elemen-elemen di bawah pivot kolom pertama pada baris 2, 3, 4, dan 5.  
* **Operasi:** $R_2 - 3R_1$, $R_3 - R_1$, $R_4 - R_1$, $R_5 - R_1$

$$
\text{Hasil: } \begin{bmatrix}
1 & 3 & 1 & 1 & 1 & \mid & 5 \\
0 & -8 & -2 & -2 & -2 & \mid & -11 \\
0 & -2 & 2 & 0 & 0 & \mid & 1 \\
0 & -2 & 0 & 2 & 0 & \mid & 2 \\
0 & -2 & 0 & 0 & 2 & \mid & 3
\end{bmatrix}
$$

### Langkah 3: Membuat Pivot pada Kolom Kedua

Kita ubah elemen pada baris kedua kolom kedua menjadi 1 dengan mengalikannya dengan skalar.  
* **Operasi:** $-\frac{1}{8}R_2$

$$
\begin{bmatrix}
1 & 3 & 1 & 1 & 1 & \mid & 5 \\
0 & 1 & \frac{1}{4} & \frac{1}{4} & \frac{1}{4} & \mid & \frac{11}{8} \\
0 & -2 & 2 & 0 & 0 & \mid & 1 \\
0 & -2 & 0 & 2 & 0 & \mid & 2 \\
0 & -2 & 0 & 0 & 2 & \mid & 3
\end{bmatrix}
$$

---

### Langkah 4: Eliminasi di Bawah Pivot Kolom Kedua

Kita nolkan nilai -2 pada baris 3, 4, dan 5 di bawah pivot kolom kedua.  
* **Operasi:** $R_3 + 2R_2$, $R_4 + 2R_2$, $R_5 + 2R_2$

$$
\begin{bmatrix}
1 & 3 & 1 & 1 & 1 & \mid & 5 \\
0 & 1 & \frac{1}{4} & \frac{1}{4} & \frac{1}{4} & \mid & \frac{11}{8} \\
0 & 0 & \frac{5}{2} & \frac{1}{2} & \frac{1}{2} & \mid & \frac{15}{4} \\
0 & 0 & \frac{1}{2} & \frac{5}{2} & \frac{1}{2} & \mid & \frac{19}{4} \\
0 & 0 & \frac{1}{2} & \frac{1}{2} & \frac{5}{2} & \mid & \frac{23}{4}
\end{bmatrix}
$$

---

### Langkah 5: Membuat Pivot pada Kolom Ketiga

* **Operasi:** $\frac{2}{5}R_3$

$$
\begin{bmatrix}
1 & 3 & 1 & 1 & 1 & \mid & 5 \\
0 & 1 & \frac{1}{4} & \frac{1}{4} & \frac{1}{4} & \mid & \frac{11}{8} \\
0 & 0 & 1 & \frac{1}{5} & \frac{1}{5} & \mid & \frac{3}{2} \\
0 & 0 & \frac{1}{2} & \frac{5}{2} & \frac{1}{2} & \mid & \frac{19}{4} \\
0 & 0 & \frac{1}{2} & \frac{1}{2} & \frac{5}{2} & \mid & \frac{23}{4}
\end{bmatrix}
$$

---

### Langkah 6: Eliminasi di Bawah Pivot Kolom Ketiga

* **Operasi:** $R_4 - \frac{1}{2}R_3$, $R_5 - \frac{1}{2}R_3$

$$
\begin{bmatrix}
1 & 3 & 1 & 1 & 1 & \mid & 5 \\
0 & 1 & \frac{1}{4} & \frac{1}{4} & \frac{1}{4} & \mid & \frac{11}{8} \\
0 & 0 & 1 & \frac{1}{5} & \frac{1}{5} & \mid & \frac{3}{2} \\
0 & 0 & 0 & \frac{12}{5} & \frac{2}{5} & \mid & 4 \\
0 & 0 & 0 & \frac{2}{5} & \frac{12}{5} & \mid & 5
\end{bmatrix}
$$

---

### Langkah 7: Membuat Pivot pada Kolom Keempat

* **Operasi:** $\frac{5}{12}R_4$

$$
\begin{bmatrix}
1 & 3 & 1 & 1 & 1 & \mid & 5 \\
0 & 1 & \frac{1}{4} & \frac{1}{4} & \frac{1}{4} & \mid & \frac{11}{8} \\
0 & 0 & 1 & \frac{1}{5} & \frac{1}{5} & \mid & \frac{3}{2} \\
0 & 0 & 0 & 1 & \frac{1}{6} & \mid & \frac{5}{3} \\
0 & 0 & 0 & \frac{2}{5} & \frac{12}{5} & \mid & 5
\end{bmatrix}
$$

---

### Langkah 8: Eliminasi di Bawah Pivot Kolom Keempat

* **Operasi:** $R_5 - \frac{2}{5}R_4$

$$
\begin{bmatrix}
1 & 3 & 1 & 1 & 1 & \mid & 5 \\
0 & 1 & \frac{1}{4} & \frac{1}{4} & \frac{1}{4} & \mid & \frac{11}{8} \\
0 & 0 & 1 & \frac{1}{5} & \frac{1}{5} & \mid & \frac{3}{2} \\
0 & 0 & 0 & 1 & \frac{1}{6} & \mid & \frac{5}{3} \\
0 & 0 & 0 & 0 & \frac{7}{3} & \mid & \frac{13}{3}
\end{bmatrix}
$$

### Langkah 9: Membuat Pivot Akhir pada Kolom Kelima

* **Operasi:** $\frac{3}{7}R_5$

$$
\begin{bmatrix}
1 & 3 & 1 & 1 & 1 & \mid & 5 \\
0 & 1 & \frac{1}{4} & \frac{1}{4} & \frac{1}{4} & \mid & \frac{11}{8} \\
0 & 0 & 1 & \frac{1}{5} & \frac{1}{5} & \mid & \frac{3}{2} \\
0 & 0 & 0 & 1 & \frac{1}{6} & \mid & \frac{5}{3} \\
0 & 0 & 0 & 0 & 1 & \mid & \frac{13}{7}
\end{bmatrix}
$$

Hingga tahap ini, kita sudah mendapatkan bentuk Eselon Baris (Segitiga Atas). Jika kita meneruskan eliminasi ke arah atas (Gauss-Jordan) untuk membuat elemen di atas diagonal menjadi nol, kita akan memperoleh hasil akhir matriks identitas yang langsung menunjukkan solusi setiap variabel:

$$x_1 = -\frac{1}{7}, \quad x_2 = \frac{6}{7}, \quad x_3 = \frac{13}{7}, \quad x_4 = \frac{20}{7}, \quad x_5 = \frac{27}{7}$$

---

## Metode 2: Aturan Cramer dan Perhitungan Determinan

Untuk menggunakan Aturan Cramer, kita memerlukan nilai determinan dari matriks utama $A$. Karena matriks $A$ memiliki struktur khusus, kita bisa menyatakannya ke dalam bentuk penjumlahan matriks diagonal $D$ dan matriks *rank-one* $uv^T$:

$$A = D + uv^T$$

Di mana komponen pembentuknya adalah:

$$
D = \begin{bmatrix}
2 & 0 & 0 & 0 & 0 \\
0 & 2 & 0 & 0 & 0 \\
0 & 0 & 2 & 0 & 0 \\
0 & 0 & 0 & 2 & 0 \\
0 & 0 & 0 & 0 & 2
\end{bmatrix},
\quad
u = \begin{bmatrix}
1 \\
1 \\
1 \\
1 \\
1
\end{bmatrix},
\quad
v^T = \begin{bmatrix}
1 & 1 & 1 & 1 & 1
\end{bmatrix}
$$

---

### Menghitung Determinan Utama dengan Matrix Determinant Lemma

Berdasarkan teorema *Matrix Determinant Lemma*, rumus untuk mencari nilai determinannya adalah:

$$\det(A) = \det(D) \cdot (1 + v^T D^{-1} u)$$

1. Nilai $\det(D)$ karena berupa matriks diagonal adalah hasil kali elemen diagonal utamanya:  
   $$\det(D) = 2 \times 2 \times 2 \times 2 \times 2 = 32$$

2. Karena $D^{-1}$ hanya membalik nilai diagonal menjadi $\frac{1}{2}$, operasi bentuk kuadrat $v^T D^{-1} u$ menghasilkan jumlah pecahan berikut:  
   $$v^T D^{-1} u = \frac{1}{2} + \frac{1}{2} + \frac{1}{2} + \frac{1}{2} + \frac{1}{2} = \frac{5}{2}$$

3. Substitusikan semua komponen ke rumus utama:  
   $$\det(A) = 32 \cdot \left(1 + \frac{5}{2}\right) = 32 \cdot \frac{7}{2} = 112$$

Jadi, nilai Determinan Utama $|A|$ adalah **112**.

---

### Pencarian Variabel dengan Aturan Cramer

Berdasarkan aturan Cramer, kita mencari nilai variabel dengan mengganti kolom ke-$i$ dengan vektor konstanta hasil, lalu menghitung determinan

## Metode 3: Metode Adjoin

Pendekatan ketiga adalah menggunakan rumus invers matriks berbasis matriks kofaktor dan adjoin:

$$A^{-1} = \frac{1}{\det(A)} \cdot \text{adj}(A)$$

Karena matriks koefisien $A$ kita bersifat simetris terhadap diagonal utamanya, matriks kofaktor yang terbentuk juga akan menghasilkan struktur yang simetris. Nilai invers dari matriks $A$ ini adalah:

$$
A^{-1} = \frac{1}{112} \begin{bmatrix}
48 & -16 & -16 & -16 & -16 \\
-16 & 48 & -16 & -16 & -16 \\
-16 & -16 & 48 & -16 & -16 \\
-16 & -16 & -16 & 48 & -16 \\
-16 & -16 & -16 & -16 & 48
\end{bmatrix}
$$

Untuk mendapatkan vektor solusi akhir $X$, kita tinggal mengalikan matriks invers tersebut dengan vektor hasil $B$:

$$X = A^{-1} \cdot B$$

$$
\begin{bmatrix}
x_1 \\
x_2 \\
x_3 \\
x_4 \\
x_5
\end{bmatrix}
= \frac{1}{112}
\begin{bmatrix}
48 & -16 & -16 & -16 & -16 \\
-16 & 48 & -16 & -16 & -16 \\
-16 & -16 & 48 & -16 & -16 \\
-16 & -16 & -16 & 48 & -16 \\
-16 & -16 & -16 & -16 & 48
\end{bmatrix}
\begin{bmatrix}
4 \\
5 \\
6 \\
7 \\
8
\end{bmatrix}
=
\begin{bmatrix}
-\frac{1}{7} \\
\frac{6}{7} \\
\frac{13}{7} \\
\frac{20}{7} \\
\frac{27}{7}
\end{bmatrix}
$$

---

## Validasi Kode Program Menggunakan Python (NumPy)

Untuk memastikan seluruh perhitungan manual di atas tepat dan akurat, skrip Python berikut mengesekusi penyelesaian sistem persamaan ini secara numerik:
import numpy as np

# Definisikan matriks koefisien A berukuran 5x5
A = np.array([[3, 1, 1, 1, 1],
              [1, 3, 1, 1, 1],
              [1, 1, 3, 1, 1],
              [1, 1, 1, 3, 1],
              [1, 1, 1, 1, 3]])

# Definisikan vektor hasil B
B = np.array([4, 5, 6, 7, 8])

# Hitung determinan utama
det_A = np.linalg.det(A)

# Selesaikan persamaan Ax = B
solusi = np.linalg.solve(A, B)

print("--- HASIL VERIFIKASI SELESAI ---")
print(f"Nilai Determinan Utama A : {det_A:.1f}")
print("Himpunan Penyelesaian Variabel:")
for i, nilai in enumerate(solusi, 1):
    print(f"x_{i} = {nilai:.4f}")
    