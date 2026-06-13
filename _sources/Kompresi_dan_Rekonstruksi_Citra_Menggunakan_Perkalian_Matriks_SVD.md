# Materi 10: Kompresi dan Rekonstruksi Citra Menggunakan Perkalian Matriks SVD

Pada materi pelengkap ini, kita akan mempraktikkan instruksi khusus mengenai bagaimana sebuah matriks acak dapat disusun sedemikian rupa hingga membentuk sebuah gambar digital, lalu mendekomposisinya menggunakan *Singular Value Decomposition* (SVD) untuk kemudian dikalikan kembali secara parsial agar memunculkan gambar itu kembali secara utuh.

---

## 1. Konsep Dasar Gambar Sebagai Matriks

Di dalam representasi grafika komputer, sebuah citra digital dua dimensi (2D) *grayscale* sejatinya adalah sebuah matriks persegi berdimensi $m \times n$. Setiap elemen di dalam matriks tersebut ($a_{ij}$) menyimpan nilai intensitas cahaya piksel (skala numerik kontinu) pada koordinat baris dan kolom tertentu.

Melalui teorema SVD, matriks gambar $A$ ini dapat dipecah menjadi tiga komponen matriks pengali:

$$A = U\Sigma V^T$$

Jika kita tuliskan dalam bentuk penjumlahan dari perkalian vektor luar (*outer product*), persamaan di atas dapat ditransformasikan menjadi:

$$A = \sum_{i=1}^{r} \sigma_i u_i v_i^T$$

Di mana $\sigma_i$ adalah nilai singular yang sudah terurut dari besar ke kecil, $u_i$ melambangkan kolom fitur matriks $U$, dan $v_i^T$ adalah baris dari matriks $V^T$.

---

## 2. Strategi Rekonstruksi Gambar Lewat Perkalian Matriks Parsial

Inti dari tugas ini adalah membuktikan bahwa kita tidak perlu mengalikan seluruh baris dan kolom matriks $U, \Sigma, V^T$ untuk membentuk gambar. Kita cukup mengambil sejumlah kecil komponen utama ($k$ buah rank pertama) yang memiliki nilai singular terbesar.

Proses perkalian matriks secara berjenjang ini dirumuskan sebagai:

$$A_k = U_k \Sigma_k V_k^T$$

* **Jika $k$ sangat kecil (misal $k = 1$ atau $k = 2$):** Hasil perkalian matriks hanya menghasilkan bayangan pola garis horizontal dan vertikal kabur (mirip bintik TV rusak). Hal ini terjadi karena informasi nilai singular yang diambil masih sangat sedikit.
* **Jika $k$ ditingkatkan secara bertahap (misal $k = 5, 10,$ hingga $20$):** Perkalian matriks antar-komponen tersebut secara ajaib mulai merekonstruksi dan memunculkan kembali detail gambar objek aslinya dengan sangat tajam dan akurat.

---

## 3. Implementasi Kode Program Python Simulator SVD Image

Berikut adalah kode Python lengkap yang secara khusus membuat matriks gambar objek geometris buatan, melakukan dekomposisi SVD, lalu mengalikan balik matriks tersebut secara bertahap untuk memunculkan gambar ke layar Colab:
import numpy as np
import matplotlib.pyplot as plt

def jalankan_simulasi_svd_gambar():
    # 1. MEMBUAT MATRIKS AWAL YANG MENGHASILKAN GAMBAR (Bentuk Huruf 'X' Digital)
    # Kita buat matriks ukuran 50 x 50 piksel bernilai nol (hitam)
    dim = 50
    A = np.zeros((dim, dim))

    # Mengisi matriks secara diagonal agar membentuk pola silang 'X' (putih bernilai 1.0)
    for i in range(dim):
        A[i, i] = 1.0
        A[i, dim - i - 1] = 1.0

    print("="*60)
    print("SIMULASI REKONSTRUKSI GAMBAR LEWAT PERKALIAN MATRIKS SVD")
    print("="*60)
    print(f"Dimensi Matriks Gambar Asal A: {A.shape}")

    # 2. PROSES DEKOMPOSISI SVD
    U, S, VT = np.linalg.svd(A, full_matrices=False)

    # Buat kanvas grafik untuk membandingkan hasil perkalian matriks
    fig, axes = plt.subplots(1, 4, figsize=(15, 4))

    # Tampilkan Gambar Asli dari Matriks Master
    axes[0].imshow(A, cmap='gray')
    axes[0].set_title("Matriks Gambar Asli (A)")
    axes[0].axis('off')

    # 3. PROSES PERKALIAN BALIK MATRIKS SECARA BERTAHAP (Rank-k)
    # Urutan jumlah komponen k yang akan diuji untuk dikalikan balik
    pilihan_k = [1, 3, 10]

    for idx, k in enumerate(pilihan_k):
        # Mengambil potongan matriks U, S, VT sebanyak k komponen saja
        U_k = U[:, :k]
        S_k = np.diag(S[:k]) # Mengubah array nilai singular menjadi matriks diagonal
        VT_k = VT[:k, :]

        # PROSES INTI DOSEN: Mengalikan matriks kembali sehingga menghasilkan gambar
        # A_k = U_k * S_k * VT_k
        A_reconstructed = U_k @ S_k @ VT_k

        # Tampilkan hasil gambar rekonstruksi ke subplot grafik
        axes[idx + 1].imshow(A_reconstructed, cmap='gray')
        axes[idx + 1].set_title(f"Hasil Perkalian (k = {k})")
        axes[idx + 1].axis('off')

    plt.tight_layout()
    plt.show()

# Jalankan fungsi simulator
jalankan_simulasi_svd_gambar()