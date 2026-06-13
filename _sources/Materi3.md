# Materi 3

## C. Studi Kasus Kompleks Eliminasi Gaussian SPL 5x5

Pada materi ini, kita akan menyelesaikan sebuah Sistem Persamaan Linear (SPL) berukuran $5 \times 5$ menggunakan metode Eliminasi Gaussian. Fokus utama dari bab ini adalah memahami bagaimana Operasi Baris Elementer (OBE) bekerja secara bertahap untuk menyederhanakan matriks augmented hingga membentuk matriks identitas agar solusi variabelnya langsung dapat diketahui.

# REPRESENTASI MATRIKS & ELIMINASI GAUSS

## 1. Representasi Matriks
Suatu sistem persamaan linear dapat direpresentasikan dalam bentuk matriks.

* **Contoh Sistem Persamaan:**
$$
\begin{cases}
x + 2y = 8 \\
3x - y = 1
\end{cases}
$$

Bentuk representasi matriksnya adalah:
$$
\begin{bmatrix}
1 & 2 \\
3 & -1
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
=
\begin{bmatrix}
8 \\
1
\end{bmatrix}
$$

---

## 2. Matriks Augmented
Untuk menyelesaikan sistem persamaan menggunakan **metode Eliminasi Gauss**, sistem diubah ke bentuk **matriks augmented**:

$$
\begin{bmatrix}
1 & 2 & \mid & 8 \\
3 & -1 & \mid & 1
\end{bmatrix}
$$

---

## 3. Eliminasi Gauss
Eliminasi Gauss dilakukan dengan **operasi baris elementer (OBE)** hingga diperoleh **matriks eselon baris**.

### Langkah-langkah Umum:
1. Menghilangkan elemen di bawah pivot (angka utama).
2. Menjadikan matriks berbentuk segitiga atau eselon.
3. Melakukan substitusi balik untuk mendapatkan nilai variabel.

### Contoh Tahapan Penyelesaian:
Dari bentuk matriks augmented di atas, dilakukan operasi baris untuk mengenolkan elemen di bawah pivot kolom pertama ($B_2 - 3B_1$):

$$
\begin{bmatrix}
1 & 2 & \mid & 8 \\
0 & -7 & \mid & -23
\end{bmatrix}
$$

#### Penyelesaian via Substitusi Balik:
Dari baris kedua matriks eselon diperoleh:
$$-7y = -23 \longrightarrow y = \frac{23}{7}$$

Substitusikan nilai $y$ ke persamaan pada baris pertama:
$$x + 2\left(\frac{23}{7}\right) = 8 \longrightarrow x = \frac{10}{7}$$

#### Solusi:
$$x = \frac{10}{7}, \quad y = \frac{23}{7}$$

### 4. Tujuan Eliminasi Gauss
* Menyederhanakan sistem persamaan linear.
* Menentukan solusi sistem (tunggal, banyak, atau tidak ada solusi).
* Mempermudah perhitungan pada sistem persamaan yang lebih besar.

### 5. Kesimpulan
Metode Eliminasi Gauss adalah cara sistematis untuk menyelesaikan sistem persamaan linear dengan:
* Mengubah persamaan ke bentuk matriks.
* Menggunakan operasi baris elementer.
* Mendapatkan solusi secara terstruktur dan efisien.

---
---

# RAGAM METODE PENYELESAIAN SPL (2 VARIABEL)

## 1. Metode Substitusi

### Contoh Soal:
$$
\begin{cases}
x + y = 5 \\
x = 2
\end{cases}
$$

### Penyelesaian:
Substitusikan $x = 2$ ke persamaan pertama:
$$2 + y = 5 \longrightarrow y = 3$$

### Solusi:
$$x = 2, \quad y = 3$$

---

## 2. Metode Eliminasi

### Contoh Soal:
$$
\begin{cases}
x + y = 5 \\
x - y = 1
\end{cases}
$$

### Penyelesaian:
Jumlahkan kedua persamaan:
$$(x + y) + (x - y) = 5 + 1 \longrightarrow 2x = 6 \longrightarrow x = 3$$

Substitusi nilai $x = 3$ ke persamaan pertama:
$$3 + y = 5 \longrightarrow y = 2$$

### Solusi:
$$x = 3, \quad y = 2$$

---

## 4. Aturan Cramer

### Contoh Soal:
$$
\begin{cases}
x + y = 5 \\
2x - y = 1
\end{cases}
$$

### Matriks Koefisien:
$$A = \begin{bmatrix} 1 & 1 \\ 2 & -1 \end{bmatrix}$$

### Determinan Utama:
$$\det(A) = (1)(-1) - (1)(2) = -3$$

### Hitung $x$ dan $y$:
$$x = \frac{\begin{vmatrix} 5 & 1 \\ 1 & -1 \end{vmatrix}}{-3} = \frac{-6}{-3} = 2$$

$$y = \frac{\begin{vmatrix} 1 & 5 \\ 2 & 1 \end{vmatrix}}{-3} = \frac{-9}{-3} = 3$$

### Solusi:
$$x = 2, \quad y = 3$$

---

## 5. Metode Numerik (Iterasi – Jacobi)

### Contoh Soal:
Sistem yang telah diubah ke bentuk eksplisit variabel:
$$
\begin{cases}
x = \frac{5 - y}{2} \\
y = \frac{4 - x}{3}
\end{cases}
$$

### Iterasi Awal:
Ambil tebakan awal: $x^{(0)} = 0, \quad y^{(0)} = 0$

### Iterasi 1:
$$x^{(1)} = \frac{5 - 0}{2} = 2.5$$
$$y^{(1)} = \frac{4 - 0}{3} \approx 1.33$$

### Iterasi 2:
$$x^{(2)} = \frac{5 - 1.33}{2} \approx 1.835$$
$$y^{(2)} = \frac{4 - 2.5}{3} = 0.5$$

*Iterasi dilanjutkan secara berulang hingga nilai variabel mencapai **konvergen**.*

---
---

# SISTEM PERSAMAAN LINIER EMPAT VARIABEL (SPL 4x5)

### Hasil OBE Matriks Segitiga Atas:
$$
\text{Hasil: } \begin{bmatrix}
1 & 1 & 1 & \mid & 6 \\
0 & -1 & -3 & \mid & -9 \\
0 & 0 & 7 & \mid & 19
\end{bmatrix}
$$

### 4. Substitusi Balik
Dari matriks segitiga atas di atas, dilakukan proses *back-substitution* sehingga diperoleh nilai akhir komponen vektor:

$$
\begin{bmatrix}
x \\
y \\
z
\end{bmatrix}
=
\begin{bmatrix}
\frac{17}{7} \\
\frac{6}{7} \\
\frac{19}{7}
\end{bmatrix}
$$

---

## B. Sistem Persamaan Linier Empat Variabel

### 1. Sistem Persamaan
$$
\begin{cases}
x + y + z + w = 10 \\
2x + y + z + w = 13 \\
x + 2y + z + w = 14 \\
x + y + 2z + w = 15
\end{cases}
$$

### 2. Matriks Augmented
Bentuk representasi matriks gabungannya adalah:
$$
\begin{bmatrix}
1 & 1 & 1 & 1 & \mid & 10 \\
2 & 1 & 1 & 1 & \mid & 13 \\
1 & 2 & 1 & 1 & \mid & 14 \\
1 & 1 & 2 & 1 & \mid & 15
\end{bmatrix}
$$

---
---

# MATERI 3

## C. Studi Kasus Kompleks Eliminasi Gaussian SPL 5x5

Pada materi ini, kita akan menyelesaikan sebuah Sistem Persamaan Linear (SPL) berukuran $5 \times 5$ menggunakan metode Eliminasi Gaussian. Fokus utama dari bab ini adalah memahami bagaimana Operasi Baris Elementer (OBE) bekerja secara bertahap untuk menyederhanakan matriks augmented hingga membentuk matriks identitas agar solusi variabelnya langsung dapat diketahui.

---

## Representasi Sistem Persamaan Linear dan Matriks Augmented

Berikut adalah struktur model matematika dari SPL lima variabel yang menjadi objek kajian kita:

$$x_1 + x_2 + x_3 + x_4 + x_5 = 1$$
$$x_2 + x_3 + x_4 + x_5 = 2$$
$$x_3 + x_4 + x_5 = 3$$
$$x_4 + x_5 = 4$$
$$x_5 = 5$$

Untuk mempermudah proses komputasi, koefisien variabel beserta konstanta di ruas kanan kita formulasikan ke dalam bentuk matriks augmented $[A \mid B]$ awal sebagai berikut:

$$
\begin{bmatrix}
1 & 1 & 1 & 1 & 1 & \mid & 1 \\
0 & 1 & 1 & 1 & 1 & \mid & 2 \\
0 & 0 & 1 & 1 & 1 & \mid & 3 \\
0 & 0 & 0 & 1 & 1 & \mid & 4 \\
0 & 0 & 0 & 0 & 1 & \

## Proses Transformasi Operasi Baris Elementer (OBE)

Tujuan dari algoritma ini adalah mentransformasikan matriks di atas menjadi bentuk eselon baris terreduksi. Kita akan mengeksekusi reduksi elemen kolom secara bertahap berdasarkan posisi pivot utama.

### Tahap 1: Analisis Pivot Kolom Pertama

Pada baris pertama kolom pertama, kita sudah mendapatkan nilai pivot bernilai 1. Jika kita perhatikan elemen di bawah baris pertama pada kolom ini, seluruhnya sudah bernilai 0.

* **Evaluasi:** Tidak diperlukan operasi baris tambahan untuk kolom pertama. Matriks tetap dalam kondisi awal dan kita bisa langsung melangkah ke target pivot berikutnya.

---

### Tahap 2: Eliminasi Elemen Kolom Kelima

Kita jadikan elemen pada baris kelima kolom kelima (angka 1) sebagai basis pivot. Target kita adalah mengeliminasi atau menolkan semua nilai 1 yang berada di atas baris kelima pada kolom tersebut.

* **Operasi OBE:** $R_1 \leftarrow R_1 - R_5$, $R_2 \leftarrow R_2 - R_5$, $R_3 \leftarrow R_3 - R_5$, $R_4 \leftarrow R_4 - R_5$

Hasil matriks setelah reduksi kolom kelima:

$$
\begin{bmatrix}
1 & 1 & 1 & 1 & 0 & \mid & -4 \\
0 & 1 & 1 & 1 & 0 & \mid & -3 \\
0 & 0 & 1 & 1 & 0 & \mid & -2 \\
0 & 0 & 0 & 1 & 0 & \mid & -1 \\
0 & 0 & 0 & 0 & 1 & \mid & 5
\end{bmatrix}
$$

---

### Tahap 3: Eliminasi Elemen Kolom Keempat

Selanjutnya, kita bergerak ke pivot baris keempat kolom keempat. Kita bersihkan elemen-elemen bernilai 1 yang berada di atas baris keempat pada kolom ini.

* **Operasi OBE:** $R_1 \leftarrow R_1 - R_4$, $R_2 \leftarrow R_2 - R_4$, $R_3 \leftarrow R_3 - R_4$

Hasil matriks setelah reduksi kolom keempat:

$$
\begin{bmatrix}
1 & 1 & 1 & 0 & 0 & \mid & -3 \\
0 & 1 & 1 & 0 & 0 & \mid & -2 \\
0 & 0 & 1 & 0 & 0 & \mid & -1 \\
0 & 0 & 0 & 1 & 0 & \mid & -1 \\
0 & 0 & 0 & 0 & 1 & \mid & 5
\end{bmatrix}
$$

---

### Tahap 4: Eliminasi Elemen Kolom Ketiga

Dengan cara yang sama, kita gunakan elemen diagonal pada baris ketiga kolom ketiga sebagai acuan untuk menolkan nilai di atasnya.

* **Operasi OBE:** $R_1 \leftarrow R_1 - R_3$, $R_2 \leftarrow R_2 - R_3$

Hasil matriks setelah reduksi kolom ketiga:

$$
\begin{bmatrix}
1 & 1 & 0 & 0 & 0 & \mid & -2 \\
0 & 1 & 0 & 0 & 0 & \mid & -1 \\
0 & 0 & 1 & 0 & 0 & \mid & -1 \\
0 & 0 & 0 & 1 & 0 & \mid & -1 \\
0 & 0 & 0 & 0 & 1 & \mid & 5
\end{bmatrix}
$$

---

### Tahap 5: Penyelesaian Akhir Kolom Kedua

Langkah terakhir dari rangkaian OBE ini adalah membersihkan elemen di atas pivot baris kedua kolom kedua. Kita hilangkan angka 1 pada baris pertama menggunakan basis baris kedua.

* **Operasi OBE:** $R_1 \leftarrow R_1 - R_2$

Hasil transformasi final matriks menjadi matriks identitas sempurna:

$$
\begin{bmatrix}
1 & 0 & 0 & 0 & 0 & \mid & -1 \\
0 & 1 & 0 & 0 & 0 & \mid & -1 \\
0 & 0 & 1 & 0 & 0 & \mid & -1 \\
0 & 0 & 0 & 1 & 0 & \mid & -1 \\
0 & 0 & 0 & 0 & 1 & \mid & 5
\end{bmatrix}
$$ 
## Kesimpulan Himpunan Penyelesaian

Karena matriks koefisien di sebelah kiri telah berhasil dikonversi penuh menjadi matriks identitas, kita dapat langsung membaca nilai kebenaran dari masing-masing variabel sistem persamaan linear ini tanpa perlu substitusi balik lagi:

$$x_1 = -1$$
$$x_2 = -1$$
$$x_3 = -1$$
$$x_4 = -1$$
$$x_5 = 5$$

---

## Validasi Logika Menggunakan Kode Python (NumPy)

Untuk membuktikan validitas langkah OBE di atas, skrip Python berikut mengeksekusi pencarian solusi nilai variabel secara otomatis:

import numpy as np

# Menyusun matriks koefisien A sesuai kasus dari dosen
A = np.array([[1, 1, 1, 1, 1],
              [0, 1, 1, 1, 1],
              [0, 0, 1, 1, 1],
              [0, 0, 0, 1, 1],
              [0, 0, 0, 0, 1]])

# Menyusun vektor hasil B
B = np.array([1, 2, 3, 4, 5])

# Menghitung solusi linear dengan numpy
solusi_komputer = np.linalg.solve(A, B)

print("--- VERIFIKASI SELESAI ---")
print("Hasil perhitungan variabel oleh sistem:")
for i, nilai in enumerate(solusi_komputer, 1):
    print(f"Nilai x_{i} = {nilai:.1f}")