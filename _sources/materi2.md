# SISTEM PERSAMAAN LINEAR

**Nama:** SHOFWANI
**NIM:** 250411100090
**Kelas:** 2A
**Mata Kuliah:** KOMPUTASI ALJABAR LINIER  

---

## 1.1 Sistem Persamaan Linear

Perhitungan dan studi solusi persamaan, khususnya sistem persamaan, memiliki peran yang sangat penting dalam matematika. Meskipun demikian, ini bukan satu-satunya fokus kajian para matematikawan.

Pada bab ini, akan dikembangkan teori yang hampir lengkap mengenai salah satu jenis persamaan matematika yang paling sederhana, yaitu persamaan linear. Pembahasan ini berfungsi sebagai pengantar tidak langsung menuju aljabar linear.

Melalui deskripsi parametrik solusi sistem linear, akan diperkenalkan konsep-konsep dasar dalam aljabar linear, antara lain:

* Ruang vektor
* Subruang
* Rentang (*span*)
* Kebebasan linear

Selain itu, bab ini juga memperkenalkan salah satu alat komputasi terpenting dalam aljabar linear, yaitu eliminasi Gauss, yang digunakan untuk menyelesaikan sistem persamaan linear secara sistematis.

---

## 1.1.1 Sistem Persamaan Linear

### Definisi 1.1.1 Persamaan Linear

Sebuah **ekspresi linear** dalam $n$ variabel $(x_1, x_2, \dots, x_n)$ adalah ungkapan matematika yang memiliki bentuk:

$$a_1x_1 + a_2x_2 + \dots + a_nx_n$$

Di mana $a_1, a_2, \dots, a_n$ merupakan bilangan real tetap (konstanta).

### Bentuk Standar

Persamaan linear adalah persamaan yang dapat disederhanakan (menggunakan penjumlahan dan pengurangan) menjadi **bentuk standar** berikut:

$$a_1x_1 + a_2x_2 + \dots + a_nx_n = b$$

> **Catatan:** Jika sebuah fungsi tidak dapat disederhanakan ke dalam bentuk standar di atas hanya dengan operasi penjumlahan dan pengurangan, maka fungsi tersebut dikategorikan sebagai **nonlinier**.

### Klasifikasi Persamaan

Berdasarkan nilai konstanta $b$ pada bentuk standar, persamaan linear dibedakan menjadi dua jenis:

| Jenis Persamaan | Syarat |
| :--- | :--- |
| **Homogen** | Jika nilai $b = 0$ |
| **Tidak Homogen** | Jika nilai $b \neq 0$ |

## 1.1.2. Contoh Persamaan Linier

Persamaan linier adalah persamaan yang setiap variabelnya berpangkat satu dan tidak saling dikalikan.

![alt text](image.png)

# a). Persamaan: 2x + 5 = 9
x = (9 - 5) / 2
print("Nilai x =", x)

# b). Persamaan: 7y - 3 = 11
y = (11 + 3) / 7
print("Nilai y =", y)