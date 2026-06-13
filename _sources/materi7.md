# Materi 7

## G. Komputasi Nilai Eigen Menggunakan Algoritma Iterasi Faktorisasi QR

Pada bab ini, kita akan mempelajari pendekatan numerik untuk mencari nilai eigen (*eigenvalues*) dari suatu matriks persegi. Jika pada materi sebelumnya kita mencari nilai eigen menggunakan persamaan karakteristik determinan secara analitis ($\det(A - \lambda I) = 0$), di dalam *computational* aljabar linear, proses tersebut kurang efisien untuk matriks berdimensi besar.

Sebagai gantinya, kita menerapkan algoritma iteratif modern yang digunakan secara luas pada superkomputer, yaitu **Algoritma Iterasi QR**.

---

### 1. Fondasi Teoretis Faktorisasi QR

Algoritma QR bekerja berdasarkan teorema aljabar linear yang menyatakan bahwa setiap matriks persegi riil $A$ dapat didekomposisi atau difaktorkan menjadi jumlah perkalian dua matriks khusus, yaitu matriks $Q$ dan matriks $R$:

$$A = Q \cdot R$$

Di mana karakteristik masing-masing matriks tersebut adalah:

* **Matriks $Q$ (Matriks Ortogonal/Ortonormal):** Merupakan matriks yang kolom-kolomnya terdiri dari vektor-vektor satuan yang saling tegak lurus (ortogonal). Sifat utamanya adalah hasil transpos matriks sama dengan inversnya ($Q^T = Q^{-1}$), sehingga jika dikalikan dengan transposnya akan menghasilkan matriks identitas ($Q^T Q = I$).
* **Matriks $R$ (Matriks Segitiga Atas / *Upper Triangular Matrix*):** Merupakan matriks di mana seluruh elemen angka di bawah diagonal utamanya bernilai nol.

---

### 2. Mekanisme Kerja Iterasi QR

Logika utama dari algoritma ini adalah melakukan proses faktorisasi dan perkalian balik secara berulang-ulang (*looping*). Alur algoritmanya dapat dijabarkan sebagai berikut:

1. Kita mulai dengan matriks awal $A_0 = A$.
2. Pada iterasi ke-$k$, kita faktorkan matriks aktif menjadi komponen ortogonal dan segitiga atas:
   $$A_k = Q_k \cdot R_k$$
3. Langkah krusial berikutnya adalah melakukan **perkalian balik** kedua matriks hasil dekomposisi tersebut untuk membentuk matriks baru $A_{k+1}$ bagi iterasi selanjutnya:
   $$A_{k+1} = R_k \cdot Q_k$$

#### Mengapa Proses Ini Menghasilkan Nilai Eigen?

Secara aljabar, jika kita substitusikan nilai $R_k = Q_k^{-1} A_k$ ke dalam persamaan perkalian balik, kita akan melihat sebuah hubungan kesamaan:

$$A_{k+1} = R_k Q_k = (Q_k^{-1} A_k) Q_k = Q_k^T A_k Q_k$$

Persamaan $A_{k+1} = Q_k^T A_k Q_k$ membuktikan bahwa matriks $A_{k+1}$ memiliki sifat **serupa (*similar*)** dengan matriks $A_k$. Berdasarkan teorema aljabar linear, dua matriks yang serupa dipastikan memiliki nilai eigen yang sama persis.

Apabila proses dekomposisi dan perkalian balik ini dieksekusi secara berulang-ulang ($A_0 \rightarrow A_1 \rightarrow A_2 \rightarrow A_3 \rightarrow \dots \rightarrow A_k$), matriks akan mengalami konvergensi secara numerik. Elemen-elemen di bawah diagonal utama secara bertahap akan mengecil mendekati nol, dan matriks secara otomatis berubah menjadi bentuk segitiga atas baru, di mana **nilai-nilai eigen asli dari matriks tersebut akan muncul secara berurutan pada elemen diagonal utamanya**.

---

### 3. Studi Kasus Perhitungan Sistem

Dalam implementasi program ini, kita menguji algoritma numerik pada matriks simetris berorde $2 \times 2$ berikut:

$$A = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix}$$

Ketika program mengeksekusi fungsi dekomposisi `np.linalg.qr()`, komputer menggunakan algoritma berbasis transformasi Householder atau proses Gram-Schmidt untuk memisahkan matriks $A$ secara presisi.

# Analisis Hasil Iterasi Konvergensi

Melalui skrip loop sebanyak 10 kali iterasi, matriks $A$ mengalami transformasi bentuk struktural. Kita dapat menganalisis perkembangan konvergensinya sebagai berikut:

* **Pada Iterasi Awal (Iterasi 1):** Matriks hasil perkalian balik $A_1 = R_0 Q_0$ masih memuat angka yang tersebar di luar diagonal utama, namun strukturnya sudah mulai condong dominan ke arah elemen diagonal.
* **Pada Iterasi Akhir (Iterasi 10):** Matriks telah mencapai kondisi konvergen sempurna. Nilai elemen pada posisi baris kedua kolom pertama ($a_{21}$) telah mengecil drastis hingga mendekati nilai nol mutlak.

Setelah perulangan ke-10 selesai, struktur matriks final yang diperoleh adalah:

$$A_{10} \approx \begin{bmatrix} 3.0000 & 0.0000 \\ 0.0000 & 1.0000 \end{bmatrix}$$

Berdasarkan nilai diagonal utama matriks hasil iterasi ke-10 tersebut, kita langsung mendapatkan dua nilai eigen sistem secara akurat, yaitu: $\lambda_1 = 3.0000$ dan $\lambda_2 = 1.0000$.

---

## Berikut Kode Python-nya
import numpy as np

# Matriks awal sesuai soal (2 1, 1 2)
A = np.array([[2, 1],
              [1, 2]], dtype=float)

def tugas_qr_iterasi(matriks_awal, n_iterasi=10):
    Ak = matriks_awal.copy()

    print("="*60)
    print("PROGRAM FAKTORISASI QR - TUGAS ALJABAR LINEAR")
    print("="*60)
    print(f"Matriks Awal:\n{Ak}\n")

    # Loop ini akan berjalan sebanyak 10 kali sesuai permintaan Bapak
    for k in range(1, n_iterasi + 1):
        # 1. Proses Faktorisasi: Mencari Q (Ortonormal) dan R (Segitiga Atas)
        Qk, Rk = np.linalg.qr(Ak)

        # 2. Proses Perkalian Balik: Ak+1 = Rk * Qk
        Ak_next = Rk @ Qk

        # Tampilkan detail setiap langkahnya
        print(f"--- ITERASI KE-{k} ---")
        print(f"Q{k} (Matriks Ortogonal):\n{Qk}")
        print(f"R{k} (Matriks Segitiga Atas):\n{Rk}")
        print(f"A{k+1} (Hasil R{k} * Q{k}):\n{Ak_next}")
        print("-" * 30)

        # Simpan hasil untuk iterasi berikutnya
        Ak = Ak_next

    print("\n" + "="*60)
    print(f"HASIL AKHIR SETELAH {n_iterasi} ITERASI:")
    print("="*60)
    print(f"Matriks Akhir:\n{Ak}")
    print(f"\nNilai Eigen (Lihat angka diagonalnya):")
    print(f"λ1 = {Ak[0,0]:.4f}")
    print(f"λ2 = {Ak[1,1]:.4f}")

# Menjalankan 10 iterasi
tugas_qr_iterasi(A, 10)
# 4. Alur Logika Fungsi `tugas_qr_iterasi`

Ketika skrip Python dijalankan, interpreter komputer mengeksekusi baris kode berdasarkan urutan instruksi logis berikut:

1. **Inisialisasi Duplikasi Data:** Perintah `matriks_awal.copy()` digunakan untuk menyalin struktur data asli ke dalam variabel operasional `Ak` agar matriks awal $A$ tidak rusak atau berubah nilainya selama proses komputasi.
2. **Eksekusi Dekomposisi Simultan:** Di dalam blok perulangan `for`, perintah `np.linalg.qr(Ak)` memanggil fungsi sub-rutin tingkat tinggi NumPy untuk mengekstrak matriks ortogonal (`Qk`) dan matriks segitiga atas (`Rk`).
3. **Penyusunan Ulang Matriks:** Operator `@` pada baris `Rk @ Qk` menginstruksikan proses perkalian *dot-product* matriks secara paralel untuk menghasilkan struktur matriks baru yang serupa bagi iterasi berikutnya.
4. **Ekstrak Komponen Diagonal:** Setelah perulangan menyentuh batas `n_iterasi=10`, program mengakses memori indeks array `Ak[0,0]` dan `Ak[1,1]` untuk menampilkan nilai eigen utama secara teks di terminal.
