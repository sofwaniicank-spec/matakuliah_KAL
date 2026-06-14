# Dokumentasi Cara Kerja Program Face Recognition dengan SVD / Eigenfaces
# Dokumentasi Cara Kerja Program Face Recognition dengan SVD / Eigenfaces

---

## 1. Tujuan Program
Program ini digunakan untuk melakukan **pengenalan wajah (*face recognition*)** menggunakan metode komputasi aljabar linear:
* *Singular Value Decomposition* (SVD)
* *Eigenfaces*
* *Euclidean Distance*

**Alur Sederhana Sistem:**
1. Gambar wajah dibaca.
2. Diubah menjadi angka/matriks.
3. Direduksi dimensinya menggunakan SVD.
4. Dibandingkan tingkat kemiripannya.
5. Dipilih wajah paling mirip.

Karena manusia rupanya suka mengubah wajah menjadi ribuan angka lalu memaksa matriks mencari identitas seseorang. Dunia benar-benar memberi aljabar linear pekerjaan yang aneh.

---

## 2. Library yang Harus Diinstall
Program membutuhkan beberapa library Python standar untuk lingkungan komputasi.

### Install Python
Gunakan spesifikasi:
* Python 3.10+ (Disarankan Python 3.11 atau 3.12)

Cek versi Python di komputer kamu:
```bash
python --version

### Install Dependensi 
pip install numpy pillow
### Library yang digunakan:
![alt text](image-20.png)

struktur dataset
dataset/
│
├── train/
│ ├── face1/
│ │ ├── img1.jpg
│ │ ├── img2.jpg
│ │
│ ├── face2/
│ ├── foto1.jpg
│ ├── foto2.jpg
│
└── test.jpg

## Penjelasan

### Folder Dataset

- Folder **train** berisi data training.
- Setiap subfolder dianggap sebagai **1 orang**.
- Nama folder digunakan sebagai **label identitas**.
- `test.jpg` adalah gambar yang ingin dikenali oleh sistem.

---

## 4. Cara Menjalankan Program

### Menjalankan Dataset Asli

```bash
python "pengenalan copy.py" --train dataset/train --test dataset/test.jpg --size 64x64
```

### Menjalankan Mode Demo

```bash
python "pengenalan copy.py" --demo
```

Mode demo akan:

- Membuat dataset wajah palsu secara otomatis.
- Menjalankan proses SVD.
- Melakukan pengenalan wajah.

Dengan demikian, meskipun belum memiliki dataset asli, program tetap dapat diuji. Komputer akan membuat wajah sintetis untuk membuktikan bahwa metode matematika yang digunakan bekerja dengan baik.

---

## 5. Alur Besar Program

Secara umum program bekerja dengan urutan sebagai berikut:

```text
Load gambar
↓
Ubah grayscale
↓
Resize gambar
↓
Flatten menjadi vektor
↓
Gabungkan menjadi matriks X
↓
Hitung mean face
↓
Centering data
↓
Lakukan SVD
↓
Ambil eigenface
↓
Proyeksikan wajah
↓
Hitung jarak Euclidean
↓
Pilih wajah paling mirip
```

---

## 6. Penjelasan Step-by-Step Pengolahan Data

### STEP 1 — Membaca Dataset

**Fungsi:**

```python
load_training_images()
```

**Kode utama:**

```python
for person_dir in sorted(path for path in train_dir.iterdir() if path.is_dir()):
```

#### Yang Terjadi

- Program membuka folder training.
- Membaca seluruh subfolder.
- Nama subfolder dianggap sebagai label identitas orang.
- Semua gambar di dalam subfolder dimuat ke dalam sistem.

#### Contoh Struktur Dataset

```text
train/
 ├── face1/
 ├── face2/
```

Maka label yang terbentuk adalah:

- `face1`
- `face2`

---

### STEP 2 — Membaca Gambar

**Fungsi:**

```python
load_grayscale_image()
```

**Kode:**

```python
image = Image.open(path).convert("L").resize(size)
```

#### a. Membuka Gambar

```python
Image.open(path)
```

Gambar dibaca dari file yang tersimpan pada folder dataset.

#### b. Mengubah ke Grayscale

```python
.convert("L")
```

Gambar RGB yang terdiri dari:

- Merah (Red)
- Hijau (Green)
- Biru (Blue)

diubah menjadi gambar dengan satu kanal warna abu-abu (*grayscale*).

**Tujuan:**

- Komputasi lebih ringan.
- Lebih mudah diproses sebagai matriks.
- SVD lebih fokus pada pola intensitas cahaya daripada warna.

#### c. Resize Gambar

```python
.resize(size)
```

Semua gambar harus memiliki ukuran yang sama, misalnya:

```text
64 × 64 piksel
```

**Mengapa penting?**

Karena seluruh gambar nantinya akan disusun menjadi matriks dengan dimensi yang seragam. Jika ukuran gambar berbeda, proses SVD tidak dapat dilakukan.

---

### STEP 3 — Mengubah Gambar Menjadi Matriks

**Kode:**

```python
matrix = np.asarray(image, dtype=np.float64) / 255.0
```

#### Hasil

```python
[[0.1 0.2 0.3]
 [0.5 0.8 0.1]]
```

Setiap piksel diubah menjadi nilai numerik antara:

- `0` = hitam
- `1` = putih

Normalisasi dilakukan dengan membagi seluruh nilai piksel dengan 255 sehingga nilainya berada pada rentang 0 hingga 1.

---

### STEP 4 — Flatten Menjadi Vektor

**Kode:**

```python
vector = matrix.reshape(-1, 1)
```

#### Penjelasan

Gambar yang semula berbentuk matriks 2 dimensi diubah menjadi vektor 1 dimensi.

Contoh:

Matriks:

```python
[[1 2]
 [3 4]]
```

Menjadi:

```python
[[1]
 [2]
 [3]
 [4]]
```

Proses ini disebut **flattening**, yaitu mengubah seluruh piksel gambar menjadi satu kolom data agar dapat digunakan dalam perhitungan matriks dan proses SVD.
### Contoh Matriks

```text
[[1 2]
 [3 4]]
```

Menjadi Vektor Kolom:

```text
[1]
[2]
[3]
[4]
```

**Kenapa dilakukan?**

Karena algoritma SVD bekerja pada bentuk vektor.

---

## STEP 5 — Membentuk Matriks Training X

### Kode

```python
x_matrix = np.hstack(vectors)
```

Semua vektor digabung menjadi:

```text
X = [x₁  x₂  x₃  ...  xₙ]
```

Contoh susunan kolom:

```text
⎡1  4  7⎤
⎢2  5  8⎥
⎣3  6  9⎦
```

Maka:

- Setiap kolom = 1 wajah
- Setiap baris = nilai piksel tertentu

---

## STEP 6 — Menghitung Mean Face

### Kode

```python
mean_face = np.mean(x_matrix, axis=1, keepdims=True)
```

Program menghitung wajah rata-rata.

### Secara Matematis

\[
\mu = \text{rata-rata seluruh wajah}
\]

Hasilnya disebut **mean face**. Ini penting karena algoritma ingin mencari perbedaan wajah terhadap wajah rata-rata.

---

## STEP 7 — Centering Data

### Kode

```python
centered_matrix = x_matrix - mean_face
```

Artinya setiap gambar dikurangi wajah rata-rata.

### Kenapa?

Karena PCA/SVD bekerja lebih baik jika data dipusatkan terhadap mean. Jika tidak dicenter, variasi data sulit dianalisis dan eigenface kurang representatif.

---

## STEP 8 — Singular Value Decomposition (SVD)

### Kode

```python
u_matrix, singular_values, vt_matrix = np.linalg.svd(centered_matrix)
```

Inilah inti program.

Rumus:

\[
X = U \Sigma V^T
\]

### Penjelasan Komponen Matriks Hasil Dekomposisi

| Matriks | Fungsi |
|----------|---------|
| **U** | Basis fitur wajah |
| **Σ** | Besarnya informasi |
| **Vᵀ** | Koefisien transformasi |

---

## Apa itu Eigenface?

Kolom pada matriks **U** disebut **eigenface**.

Eigenface adalah pola wajah utama yang ditemukan sistem. Eigenface bukan wajah manusia secara langsung, melainkan representasi matematis yang menangkap karakteristik penting dari kumpulan wajah pada dataset.

Dengan menggunakan eigenface, sistem dapat merepresentasikan wajah berdimensi tinggi ke ruang fitur yang lebih kecil tanpa kehilangan informasi penting yang dibutuhkan untuk proses pengenalan wajah.
## STEP 9 — Memilih Komponen Penting

### Kode

```python
u_k = u_matrix[:, :component_count]
```

Program hanya mengambil beberapa komponen terbaik dari matriks eigenface.

### Kenapa?

Karena komponen dengan nilai terbesar mengandung informasi yang paling penting, sedangkan komponen dengan nilai kecil biasanya hanya berisi noise atau informasi yang kurang signifikan.

### Tujuan

Melakukan **reduksi dimensi** sehingga jumlah data yang diproses menjadi lebih sedikit tanpa kehilangan informasi penting.

```text
4096 piksel
      ↓
20 fitur penting
```

---

## STEP 10 — Proyeksi Wajah Training

### Kode

```python
train_weights = u_k.T @ centered_matrix
```

### Penjelasan

Semua wajah pada dataset training diproyeksikan ke ruang eigenface.

Hasil proyeksi ini menghasilkan representasi baru berupa bobot fitur (*feature weights*) yang lebih ringkas dibandingkan data piksel asli.

---

## STEP 11 — Memproses Wajah Test

### Kode

```python
test_centered = test_image.vector - mean_face
```

Kemudian:

```python
test_weights = u_k.T @ test_centered
```

### Penjelasan

Proses yang dilakukan adalah:

1. Gambar uji (*test image*) dikurangi dengan mean face.
2. Hasil pengurangan diproyeksikan ke ruang eigenface.
3. Diperoleh bobot fitur wajah uji yang nantinya dibandingkan dengan data training.

---

## STEP 12 — Menghitung Jarak

### Kode

```python
distance = np.linalg.norm(
    test_weights - train_weights[:, [index]]
)
```

### Penjelasan

Program menghitung **jarak Euclidean** antara wajah uji dan setiap wajah pada data training.

Semakin kecil nilai jarak yang diperoleh, maka semakin mirip kedua wajah tersebut.

Secara matematis:

\[
d(x,y)=\sqrt{\sum_{i=1}^{n}(x_i-y_i)^2}
\]

Jarak yang paling kecil menunjukkan tingkat kemiripan tertinggi.

---

## STEP 13 — Menentukan Prediksi

### Kode

```python
distances.sort(key=lambda row: row[2])
```

### Penjelasan

Program mengurutkan seluruh hasil perhitungan jarak dari yang terkecil hingga terbesar.

Contoh hasil:

| Label | Jarak |
|---------|---------|
| face1 | 0.21 |
| face2 | 1.90 |

Karena **face1** memiliki jarak paling kecil, maka sistem menyimpulkan bahwa gambar `test.jpg` paling mirip dengan **face1**.

---

## STEP 14 — Threshold

### Kode

```python
accepted = nearest_distance <= computed_threshold
```

### Penjelasan

Threshold digunakan untuk menentukan apakah wajah berhasil dikenali atau tidak.

Logika yang digunakan:

- Jika jarak ≤ threshold → wajah dikenali.
- Jika jarak > threshold → wajah tidak dikenali.

Output yang diberikan:

```text
UNKNOWN
```

Dengan demikian sistem dapat menolak wajah yang tidak terdapat pada dataset training.

---

# 7. Visualisasi yang Dihasilkan

Program menghasilkan beberapa visualisasi untuk membantu analisis proses pengenalan wajah.

### Mean Face

Rata-rata dari seluruh wajah pada dataset training.

### Centered Face

Wajah yang telah dikurangi dengan nilai mean face sehingga hanya menyisakan variasi penting.

### Eigenface

Pola fitur utama wajah yang diperoleh dari proses dekomposisi SVD.

### Reconstruction

Wajah hasil rekonstruksi menggunakan sejumlah komponen eigenface.

### Error Image

Perbedaan antara gambar asli dan hasil rekonstruksi.

---

# 8. Penjelasan Fungsi Penting

## `parse_size()`

Mengubah input ukuran gambar dalam bentuk string seperti:

```text
64x64
```

menjadi format tuple:

```python
(64, 64)
```

---

## `image_paths()`

Mencari dan mengumpulkan seluruh file gambar yang terdapat dalam direktori dataset.

---

## `normalize_to_uint8()`

Mengubah nilai matriks hasil perhitungan kembali ke rentang citra standar (0–255) agar dapat divisualisasikan sebagai gambar.

---

## `matrix_to_image()`

Mengonversi array atau matriks NumPy menjadi objek gambar yang dapat disimpan atau ditampilkan.

---

## `save_grid()`

Menggabungkan beberapa gambar hasil analisis menjadi satu gambar komposit dalam bentuk grid.

Contohnya:

- Mean Face
- Eigenface
- Reconstruction
- Error Image

ditampilkan dalam satu file gambar.

---

## `choose_threshold()`

Menghitung nilai threshold secara otomatis berdasarkan distribusi data training sehingga sistem dapat menentukan batas pengenalan wajah secara lebih adaptif.

---

## `recognize_with_svd()`

Merupakan fungsi utama dari seluruh algoritma.

Fungsi ini bertanggung jawab untuk:

1. Membaca data training.
2. Menghitung mean face.
3. Melakukan centering data.
4. Menjalankan Singular Value Decomposition (SVD).
5. Membentuk eigenface.
6. Memproyeksikan data training dan data uji.
7. Menghitung jarak Euclidean.
8. Menentukan hasil pengenalan wajah.
9. Menghasilkan visualisasi analisis.

Fungsi ini menjadi pusat dari seluruh proses pengenalan wajah berbasis **Eigenface** dan **Singular Value Decomposition (SVD)**.# 9. Rumus Penting yang Dipakai

### Mean Face
$$\mu = \text{rata-rata seluruh wajah}$$

### Centering
$$A = X - \mu$$

### SVD
$$A = U \Sigma V^T$$

### Proyeksi Eigenface
$$W = U^T A$$
$$\text{SSEuclideanDistance} \ \Omega d = \|x - y\|$$

---

# 10. Output Program

Program menghasilkan dua komponen keluaran utama:
* **File laporan (`laporan_svd.txt`):** Berisi salinan matriks, nilai singular, hasil prediksi, bobot jarak, dan komponen eigenface.
* **Folder visualisasi (`hasil_analisis_svd`):** Berisi berkas gambar mean face, eigenface, grafik perkembangan singular value, hingga visualisasi reconstruction.

---

# 11. Kesimpulan Cara Kerja Program

Secara singkat:
1. Gambar diubah menjadi angka.
2. Angka diproses menjadi matriks.
3. SVD mencari pola utama wajah (*eigenfaces*).
4. Wajah diproyeksikan ke ruang fitur rendah.
5. Jarak spasial dihitung.
6. Wajah terdekat dipilih sebagai hasil pengenalan.
Program ini sebenarnya adalah gabungan dari pengolahan citra, aljabar linear, reduksi dimensi, dan klasifikasi sederhana. Menariknya, inti pengenalan wajah di sini bukan AI modern beratus miliaran parameter, tapi matematika klasik yang sudah ada sejak lama. Kadang solusi elegan memang tidak perlu GPU seharga motor.