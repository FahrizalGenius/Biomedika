---
title: biomedika

---
# Biomedika

Tahap 1: Kuantisasi (Penyederhanaan Derajat Keabuan)
Untuk memungkinkan perhitungan manual secara matriks $\mathbf{4} {\times} \mathbf{4}$, nilai intensitas piksel asli (8bit, rentang 0-255) dikuantisasi menjadi 4 tingkat keabuan ( $0,1,2,3$ ) dengan rentang sebagai berikut:

- 0-63 diubah menjadi 0
- 64-127 diubah menjadi 1
- 128-191 diubah menjadi 2
- 192-255 diubah menjadi 3

Matriks Asli ( ${I}_{\text {asli): }}$
$$
\left[\begin{array}{llll}
223 & 232 & 207 & 159 \\
185 & 220 & 173 & 146 \\
156 & 178 & 153 & 140 \\
168 & 189 & 162 & 148
\end{array}\right]
$$

Matriks Hasil Kuantisasi (I):
$$
\left[\begin{array}{llll}
3 & 3 & 3 & 2 \\
2 & 3 & 2 & 2 \\
2 & 2 & 2 & 2 \\
2 & 2 & 2 & 2
\end{array}\right]
$$

Tahap 2: Pembentukan Matriks GLCM Mentah
Parameter yang digunakan untuk perhitungan adalah Jarak $({\alpha})=\mathbf{1}$ dan $\operatorname{Arah}({\theta})=\mathbf{0}^{\circ}$ (Horizontal, dari kiri ke kanan). Kita memindai pasangan piksel yang berdampingan di setiap baris matriks $I$ :
- Baris 1: $(3,3),(3,3),(3,2)$
- Baris 2: $(2,3),(3,2),(2,2)$
- Baris 3: $(2,2),(2,2),(2,2)$
- Baris 4: $(2,2),(2,2),(2,2)$

Rekapitulasi frekuensi pasangan:
- Pasangan $(2,2)$ muncul 7 kali
- Pasangan $(2,3)$ muncul 1 kali
- Pasangan $(3,2)$ muncul 2 kali
- Pasangan $(3,3)$ muncul 2 kali
- Total pasangan $(N)=7+1+2+2=12$

Tabel GLCM Mentah $C$:

| ilj | 0 | 1 | 2 |
| :--- | :--- | :--- | :--- |
| 0 | 0 | 0 | 0 |
| 1 | 0 | 0 | 0 |
| 2 | 0 | 0 | 7 |
| 3 | 0 | 0 | 2 |

Tabel GLCM Ternormalisasi ( $P$ ):


3: Normalisasi Matriks GLCM
Membagi setiap nilai pada matriks $C$ dengan total pasangan ( $N=12$ ) untuk mendapatkan probabilitas $P(i, j)$.}

| i j | 0 | 1 | 2 |
| :--- | :--- | :--- | :--- |
| 0 | 0 | 0 | 0 |
| 1 | 0 | 0 | 0 |
| 2 | 0 | 0 | 7/12 |
| 3 | 0 | 0 | 2/12 |

Tahap 4: Ekstraksi Fitur GLCM
Kita hanya akan menghitung indeks baris (i) dan kolom (j) yang memiliki nilai probabilitas lebih dari 0, yaitu: $(2,2),(2,3),(3,2),(3,3)$.
1. Contrast

Mengukur perbedaan intensitas lokal.
Contrast $=\sum_{i, j}|i-j|^2 P(i, j)$
- Untuk $(2,2):|2-2|^2 \times(7 / 12)=0$
- Untuk $(2,3):|2-3|^2 \times(1 / 12)=1 \times(1 / 12)=1 / 12$
- Untuk $(3,2):|3-2|^2 \times(2 / 12)=1 \times(2 / 12)=2 / 12$
- Untuk $(3,3):|3-3|^2 \times(2 / 12)=0$

Total Contrast $=\frac{1}{12}+\frac{2}{12}=\frac{3}{12}=0.25$
2. Homogeneity

Mengukur keseragaman citra.
Homogeneity $=\sum_{i, j} \frac{P(i, j)}{1+|i-j|^2}$
- Untuk $(2,2): \frac{7 / 12}{1+0}=7 / 12$
- Untuk $(2,3): \frac{1 / 12}{1+\mathrm{I}}=\frac{1 / 12}{2}=1 / 24$
- Untuk $(3,2): \frac{2 / 12}{1+1}=\frac{2 / 12}{2}=2 / 24=1 / 12$
- Untuk $(3,3): \frac{2 / 12}{1+0}=2 / 12$

Total Homogeneity $=\frac{7}{12}+\frac{1}{24}+\frac{1}{12}+\frac{2}{12}=\frac{14}{24}+\frac{1}{24}+\frac{2}{24}+\frac{4}{24}=\frac{21}{24}=0.875$


