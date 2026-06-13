# MENCARI A invers matrix

## Invers Matriks dengan Metode Gauss-Jordan

### Diketahui

$$
A = \begin{bmatrix}
1 & 1 & 1 & 1 \\
2 & -1 & 1 & -1 \\
1 & 2 & -1 & 1 \\
3 & -1 & 2 & 1
\end{bmatrix}
$$

---

### Langkah 1: Matriks Augmented

$$
[A \mid I] = \begin{bmatrix}
1 & 1 & 1 & 1 & \mid & 1 & 0 & 0 & 0 \\
2 & -1 & 1 & -1 & \mid & 0 & 1 & 0 & 0 \\
1 & 2 & -1 & 1 & \mid & 0 & 0 & 1 & 0 \\
3 & -1 & 2 & 1 & \mid & 0 & 0 & 0 & 1
\end{bmatrix}
$$

---

### Langkah 2: Eliminasi Kolom 1

Hasil:

$$
\begin{bmatrix}
1 & 1 & 1 & 1 & \mid & 1 & 0 & 0 & 0 \\
0 & -3 & -1 & -3 & \mid & -2 & 1 & 0 & 0 \\
0 & 1 & -2 & 0 & \mid & -1 & 0 & 1 & 0 \\
0 & -4 & -1 & -2 & \mid & -3 & 0 & 0 & 1
\end{bmatrix}
$$

---

### Hasil Akhir

$$
[I \mid A^{-1}]
$$

$$
A^{-1} = \frac{1}{6} \begin{bmatrix}
1 & 1 & 1 & -1 \\
1 & -1 & 1 & 1 \\
1 & 1 & -1 & 1 \\
1 & -1 & -1 & -1
\end{bmatrix}
$$

---

### Bentuk Pecahan

$$
A^{-1} = \begin{bmatrix}
\frac{1}{6} & \frac{1}{6} & \frac{1}{6} & -\frac{1}{6} \\
\frac{1}{6} & -\frac{1}{6} & \frac{1}{6} & \frac{1}{6} \\
\frac{1}{6} & \frac{1}{6} & -\frac{1}{6} & \frac{1}{6} \\
\frac{1}{6} & -\frac{1}{6} & -\frac{1}{6} & -\frac{1}{6}
\end{bmatrix}
$$