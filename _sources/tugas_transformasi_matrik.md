# tugas transformasi matrik
# kode program pertama
import numpy as np

def transformasi_grup(matriks_titik, vektor_translasi):
    """
    Menghitung pergeseran untuk banyak titik sekaligus.
    """
    # NumPy akan otomatis menambahkan vektor ke setiap baris matriks
    return matriks_titik + vektor_translasi

# 1. Definisikan Vektor Pergeseran (Geser 2 ke kanan sesuai gambar)
vektor_T = np.array([2, 0])

# 2. Definisikan Grup Titik Biru Kiri (A, B, C, D)
# Koordinat x dari -4 sampai -3
titik_biru_kiri = np.array([
    [-4, 3], # A
    [-3, 3], # B
    [-4, 2], # C
    [-3, 2]  # D
])

# 3. Definisikan Grup Titik Biru Kanan (E, G, F, H)
# Koordinat x dari 3 sampai 4
titik_biru_kanan = np.array([
    [3, 3], # E
    [4, 3], # G
    [3, 2], # F
    [4, 2]  # H
])

# 4. Hitung semua titik merah secara otomatis
titik_merah_kiri = transformasi_grup(titik_biru_kiri, vektor_T)
titik_merah_kanan = transformasi_grup(titik_biru_kanan, vektor_T)

# Output Hasil
print("--- HASIL TRANSFORMASI ---")
print(f"Titik Biru Kiri (-4 s/d -3) menjadi Merah Kiri:\n{titik_merah_kiri}")
print(f"\nTitik Biru Kanan (3 s/d 4) menjadi Merah Kanan:\n{titik_merah_kanan}")

# kode program ke 2
import numpy as np
import matplotlib.pyplot as plt

def visualisasi_transformasi_otomatis(titik_kiri_input, vektor_geser):
    # 1. Konversi input ke NumPy Array untuk operasi matriks
    P_kiri = np.array(titik_kiri_input)
    T = np.array(vektor_geser)

    # 2. Definisikan Titik Biru Kanan (Referensinya)
    P_kanan = np.array([[3, 3], [4, 3], [3, 2], [4, 2]])

    # 3. Hitung Titik Merah secara OTOMATIS (P' = P + T)
    P_merah_kiri = P_kiri + T
    P_merah_kanan = P_kanan + T

    # 4. Proses Menggambar dengan Matplotlib
    plt.figure(figsize=(10, 6))

    # Menggambar Titik
    plt.scatter(P_kiri[:,0], P_kiri[:,1], color='blue', s=100, label='Titik Biru (Asal)', edgecolors='black', zorder=5)
    plt.scatter(P_kanan[:,0], P_kanan[:,1], color='blue', s=100, edgecolors='black', zorder=5)
    plt.scatter(P_merah_kiri[:,0], P_merah_kiri[:,1], color='red', s=100, label='Titik Merah (Hasil)', edgecolors='black', zorder=5)
    plt.scatter(P_merah_kanan[:,0], P_merah_kanan[:,1], color='red', s=100, edgecolors='black', zorder=5)

    # Pengaturan Canvas
    plt.axhline(0, color='black', linewidth=1)
    plt.axvline(0, color='black', linewidth=1)
    plt.grid(True, which='both', linestyle='--', linewidth=0.5)
    plt.xlim(-6, 8)
    plt.ylim(-1, 5)
    plt.legend()
    plt.title(f"Transformasi Matriks Dinamis (Geser x={vektor_geser[0]})")

    # --- BAGIAN PERBAIKAN: MEMAKSA SEMUA ANGKA MUNCUL ---
    # Tentukan jangkauan yang Anda inginkan
    xticks = np.arange(-6, 9, 1) # Membuat urutan dari -6 sampai 8 dengan jarak 1
    # Instruksi spesifik ke Matplotlib untuk sumbu X
    plt.xticks(xticks)
    # ----------------------------------------------------

    plt.show()

# --- EKSEKUSI ---
# Input awal yang ingin Anda coba ubah-ubah:
titik_awal = [[-4, 3], [-3, 3], [-4, 2], [-3, 2]]
pergeseran = [2, 0] # Geser x = 2

visualisasi_transformasi_otomatis(titik_awal, pergeseran)

# Analisis Teknis Mekanisme Transformasi Matriks (Translasi)

Di bawah ini adalah penjelasan mendalam mengenai logika matematika dan komputasi di balik mekanisme pergeseran objek yang terjadi pada program simulator:

## 1. Proses Pergeseran Koordinat Secara Akurat

Secara teknis, perpindahan objek yang terjadi di dalam grafik bukan sekadar perubahan visual di layar monitor, melainkan hasil dari operasi translasi pada ruang vektor dua dimensi (2D). Setiap titik asal yang kita miliki diwakili oleh matriks data $P$ dengan koordinat $(x, y)$ yang telah didefinisikan secara statis di dalam baris kode.

Agar titik-titik tersebut dapat berpindah menuju posisi baru (menjadi titik merah $P'$), kita harus menerapkan sebuah vektor translasi:

$$T = \begin{bmatrix} dx \\ dy \end{bmatrix}$$

Dalam studi kasus ini, nilai yang ditetapkan adalah $dx = 2$ dan $dy = 0$. Hal ini berarti sistem secara teliti akan menambahkan setiap elemen koordinat $x$ pada titik biru dengan konstanta 2, sedangkan nilai koordinat $y$ akan tetap dipertahankan karena tidak ada instruksi pergeseran vertikal.

Proses kalkulasi ini dieksekusi menggunakan pustaka NumPy melalui operasi tervektor (*vectorized operation*), sehingga seluruh perhitungan berjalan presisi dan efisien pada level memori tanpa memerlukan struktur perulangan manual (*looping*).

---

## 2. Mekanisme Matriks Penggerak Homogen

Selain memanfaatkan operasi penjumlahan vektor biasa seperti formula $P + T$, di dalam konsep grafika komputer terdapat metode yang lebih canggih, yaitu menggunakan **Matriks Transformasi Homogen berukuran $3 \times 3$**.

Matriks homogen ini bertindak sebagai operator linear tunggal yang menyatukan proses translasi dan transformasi lainnya. Struktur matriks penggerak untuk kasus pergeseran $dx = 2$ ini dirumuskan sebagai:

$$M = \begin{bmatrix} 1 & 0 & 2 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}$$

Dengan menggunakan representasi koordinat homogen ini, koordinat kartesius 2D $(x, y)$ diubah sementara menjadi koordinat 3D $[x, y, 1]^T$. Melalui struktur ini, kita tidak lagi menggunakan operasi penjumlahan terpisah, melainkan murni menggunakan **Perkalian Matriks**:

$$\begin{bmatrix} x' \\ y' \\ 1 \end{bmatrix} = \begin{bmatrix} 1 & 0 & 2 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$$

Setiap koordinat titik biru yang dikalikan dengan matriks operator $M$ akan langsung menghasilkan posisi koordinat titik merah yang baru secara otomatis dan simultan.

---

## 3. Kesimpulan Teoretis

Transformasi geometri pada ruang digital dapat terjadi karena adanya interaksi linear yang konsisten antara Matriks Data (representasi objek titik biru) dengan Matriks Operator (bertindak sebagai penggerak).

Pendekatan menggunakan matriks operator ini sangat krusial dalam ilmu komputer. Hanya dengan mendefinisikan satu matriks operator yang presisi, sistem komputer mampu mengontrol, memanipulasi, dan menggeser ribuan hingga jutaan objek titik koordinat sekaligus dalam waktu singkat. Konsep fundamental inilah yang mendasari bagaimana objek di dalam video game atau aplikasi grafis modern dapat bergerak dengan mulus, akurat, dan responsif.

---

# Penjelasan Teknis Komputasi Transformasi Matriks

Pada bagian ini, kita akan membedah logika matematika dan alur pemrograman yang digunakan di dalam skrip Python di atas. Program tersebut menerapkan konsep **Translasi Simultan (Grup)** memanfaatkan efisiensi pemrosesan paralel dari pustaka NumPy.

# 1. Formulasi Matematika Translasi 2D

Secara geometris, memindahkan atau menggeser sebuah titik koordinat $(x, y)$ di dalam ruang kartesius sejauh vektor translasi $T = (dx, dy)$ dilakukan menggunakan operasi penjumlahan vektor:

$$x' = x + dx$$
$$y' = y + dy$$

Pada skrip pemrograman kita, vektor pergeseran didefinisikan melalui variabel `pergeseran = [2, 0]`. Hal ini berarti:

* Objek akan digeser secara horizontal ke arah kanan sebesar **2 satuan** ($dx = 2$).
* Objek **tidak mengalami pergeseran vertikal** sama sekali pada sumbu Y ($dy = 0$).

---

# 2. Algoritma Perhitungan Paralel Berbasis NumPy *Broadcasting*

Kelebihan utama dari baris kode `P_kiri + T` terletak pada pemanfaatan fitur *Broadcasting* bawaan NumPy. Secara matematis, kelompok titik koordinat awal (A, B, C, D) disusun menjadi sebuah matriks berdimensi $4 \times 2$ bernama `titik_biru_kiri`:

$$\text{titik\_biru\_kiri} = \begin{bmatrix} -4 & 3 \\ -3 & 3 \\ -4 & 2 \\ -3 & 2 \end{bmatrix}$$

Sedangkan vektor translasi kita merupakan array 1 dimensi berukuran $1 \times 2$, yaitu vektor $T = \begin{bmatrix} 2 & 0 \end{bmatrix}$.

Secara aturan aljabar matriks murni, operasi penjumlahan antara matriks $4 \times 2$ dengan matriks $1 \times 2$ tidak dapat didefinisikan karena ketidaksesuaian dimensi ruang. Namun, di dalam pustaka NumPy, sistem akan otomatis menduplikasi dan mendistribusikan vektor `T` ke setiap baris matriks titik secara simultan di dalam memori komputer.

Visualisasi operasi aljabar di latar belakang komputer dapat dijabarkan sebagai berikut:

$$\begin{bmatrix} -4 & 3 \\ -3 & 3 \\ -4 & 2 \\ -3 & 2 \end{bmatrix} + \begin{bmatrix} 2 & 0 \\ 2 & 0 \\ 2 & 0 \\ 2 & 0 \end{bmatrix} = \begin{bmatrix} -4+2 & 3+0 \\ -3+2 & 3+0 \\ -4+2 & 2+0 \\ -3+2 & 2+0 \end{bmatrix} = \begin{bmatrix} -2 & 3 \\ -1 & 3 \\ -2 & 2 \\ -1 & 2 \end{bmatrix}$$

Hasil komputasi di atas langsung menjadi koordinat baru untuk `titik_merah_kiri`. Hanya dengan satu baris perintah aritmatika, komputer mampu memproses banyak titik sekaligus tanpa membuang memori lewat proses perulangan (*looping*).

---

# 3. Alur Logika Fungsi `visualisasi_transformasi_otomatis`

Ketika fungsi visualisasi dieksekusi di dalam lingkungan Google Colab, interpreter Python menjalankan rangkaian instruksi sebagai berikut:

1. **Konversi Tipe Data:** Mengubah koordinat matriks mentah dari `titik_awal` menjadi objek array terstruktur NumPy (`P_kiri`) agar siap memproses operasi *broadcasting*.
2. **Kalkulasi Titik Baru:** Mengeksekusi penjumlahan matriks gabungan secara otomatis untuk mendapatkan koordinat baru kelompok kiri (`P_merah_kiri`) dan kelompok kanan (`P_merah_kanan`).
3. **Penyusunan Grafik Visual (Matplotlib Plotting):**
   * Fungsi `plt.scatter()` pertama dan kedua bertugas menggambar seluruh titik koordinat asal yang diwakili oleh warna **biru**.
   * Fungsi `plt.scatter()` ketiga dan keempat bertugas memetakan titik koordinat baru hasil transformasi yang diwakili oleh warna **merah**.
4. **Kalibrasi Skala Sumbu Grafik:** Perintah `plt.xticks(np.arange(-6, 9, 1))` menginstruksikan sistem grafik untuk menampilkan interval angka sumbu X secara presisi dengan jarak konstan 1 satuan (dari skala -6 hingga 8). Langkah ini sangat penting agar pengguna dapat mengukur jarak perpindahan vektor spasial secara akurat secara visual.