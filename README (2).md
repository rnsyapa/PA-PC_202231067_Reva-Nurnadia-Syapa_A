
# FILTERING CITRA (Teori yang mendukung dan tahapan cara menyeleseaikan projek)

**FILTERING CITRA**

Filtering citra adalah proses manipulasi citra untuk meningkatkan kualitas atau mengekstrak informasi tertentu. Dua metode filtering yang umum digunakan adalah mean filtering dan median filtering. Berikut adalah penjelasan mendalam mengenai kedua metode tersebut:

1. Mean Filtering
Mean filtering adalah teknik smoothing yang digunakan untuk mengurangi noise pada citra. Proses ini bekerja dengan menggantikan setiap piksel dalam citra dengan rata-rata nilai piksel di sekitarnya. Filter ini membantu membuat citra lebih halus dan mengurangi detail kecil atau noise.

Kelebihan:
- Mudah diimplementasikan.
- Efektif untuk mengurangi noise Gaussian.
Kekurangan:
- Dapat mengaburkan tepi (edges) dalam citra.
- Tidak efektif untuk menghilangkan noise impulsif (seperti salt-and-pepper noise).

2. Median Filtering
Median filtering adalah teknik non-linear yang digunakan untuk menghilangkan noise dari citra. Proses ini bekerja dengan menggantikan setiap piksel dalam citra dengan median dari nilai piksel di sekitarnya. Filter ini sangat efektif untuk menghilangkan noise impulsif seperti salt-and-pepper noise.

Kelebihan:
- Efektif untuk menghilangkan noise impulsif.
- Tidak mengaburkan tepi dalam citra sebanyak mean filtering.
Kekurangan:
- Memerlukan lebih banyak komputasi dibandingkan mean filtering.
- Hasilnya mungkin kurang halus dibandingkan mean filtering untuk noise Gaussian.

**Tahapan Cara Menyelesaikan Projek**

1. IMPORT LIBRARY
import cv2 

import matplotlib.pyplot as plt ## untuk memvisualisasi data

import numpy as np ## untuk membaca angka

Pustaka `cv2` adalah bagian dari OpenCV (Open Source Computer Vision Library), yang digunakan untuk memproses gambar dan video. Pustaka `matplotlib.pyplot` adalah modul dari Matplotlib yang digunakan untuk membuat visualisasi data dalam Python. Modul ini menyediakan fungsi untuk membuat grafik, diagram, dan plot, serta sering digunakan untuk menampilkan dan membandingkan gambar hasil pemrosesan. Pustaka `numpy` adalah pustaka fundamental untuk komputasi ilmiah dalam Python, yang menyediakan dukungan untuk array multidimensi dan berbagai fungsi matematika serta aljabar linear.

2. Ketetanggaan Pixel
img = cv2.imread("revaa.jpg")
citra = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

copyCitra1 = citra.copy().astype(float)

m1, n1 = copyCitra1.shape
output1 = np.empty([m1, n1])

print("Shape copy citra 1: ", copyCitra1.shape)
print("Shape output citra 1: ", output1.shape)

print('m1: ', m1)

print('n1: ', n1)

print()

Kode tersebut membaca sebuah gambar bernama "revaa.jpg" menggunakan pustaka OpenCV dan mengonversinya menjadi citra grayscale (abu-abu). Proses ini dilakukan oleh fungsi `cv2.imread` untuk membaca gambar dan `cv2.cvtColor` untuk mengubah gambar dari format BGR ke grayscale. Selanjutnya, citra grayscale tersebut disalin ke dalam variabel `copyCitra1` dan diubah tipe datanya menjadi float untuk presisi lebih tinggi dalam perhitungan selanjutnya. Setelah itu, ukuran (shape) dari `copyCitra1` diambil dan disimpan dalam variabel `m1` dan `n1`, yang merepresentasikan jumlah baris dan kolom pada citra tersebut. Sebuah array kosong `output1` dengan ukuran yang sama dibuat untuk menampung hasil pemrosesan selanjutnya. Terakhir, informasi mengenai ukuran `copyCitra1` dan `output1`, serta nilai `m1` dan `n1`, ditampilkan ke layar untuk verifikasi.

3. Membuat filter rata-rata
for baris in range(0, m1-1):
    for kolom in range(0, n1-1):
        a1 = baris
        b1 = kolom
        jumlah = copyCitra1[a1-1, b1-1] + copyCitra1[a1-1, b1]  + copyCitra1[a1-1, b1+1] +\
            copyCitra1[a1, b1-1] + copyCitra1[a1,b1] + copyCitra1[a1, b1] +\
            copyCitra1[a1+1, b1-1] + copyCitra1[a1+1, b1] + copyCitra1[a1+1, b1 +1]
        output1[a1,b1] = 1/9*jumlah

fig, axis = plt.subplots(1,2, figsize=(10,10))
ax = axis.ravel()

ax[0].imshow(citra, cmap='gray')
ax[0].set_title('Original Image')

ax[1].imshow(output1, cmap='gray')
ax[1].set_title('Mean Filtered Image')
plt.show()

Kode tersebut merupakan implementasi dari filter rata-rata (mean filter) untuk memproses citra dalam matriks `copyCitra1`. Prosesnya dilakukan dengan mengambil nilai intensitas piksel di sekitar setiap piksel dalam citra menggunakan nested loop untuk setiap baris dan kolom. Di setiap iterasi, nilai intensitas piksel di sekitar piksel saat ini dijumlahkan dan dirata-ratakan dengan faktor skalar 1/9. Hasilnya disimpan dalam matriks `output1`. Hasil akhir dari proses ini adalah citra yang telah mengalami penghalusan, ditampilkan dalam subplot dengan citra asli untuk perbandingan visual.

4. Median Filtering

img_filtering = img.copy()
img_filtering = cv2.cvtColor(img_filtering, cv2.COLOR_BGR2RGB)
img_median = img.copy()
img_median = cv2.cvtColor(img_median, cv2.COLOR_BGR2RGB)
img_median_after = cv2.medianBlur(img_median, 5)

fig, axis = plt.subplots(1,2, figsize=(10,10))
ax = axis.ravel()

ax[0].imshow(img_filtering)
ax[0].set_title('Citra Asli')

ax[1].imshow(img_median_after)
ax[1].set_title('After filter median')
plt.show()

Kode ini menggunakan OpenCV untuk melakukan filtering citra dengan metode filter median. Awalnya, citra `img` disalin ke `img_filtering` dan `img_median`. Kemudian, kedua citra tersebut dikonversi dari format BGR ke RGB menggunakan `cv2.cvtColor` untuk kompatibilitas tampilan dengan matplotlib. Selanjutnya, `img_median` disubmit ke fungsi `cv2.medianBlur` dengan parameter kernel size 5 untuk menerapkan filter median, yang menggantikan setiap piksel dengan nilai median dari nilai piksel di sekitarnya. Hasilnya, citra asli dan citra yang telah di-filter dengan metode median ditampilkan dalam subplot menggunakan matplotlib. Metode ini berguna untuk mengurangi noise dalam citra, menghasilkan citra yang lebih halus dan lebih jelas secara visual.

5. output

import matplotlib.pyplot as plt

fig, axis = plt.subplots(2, 2, figsize=(7, 9))
ax = axis.ravel()

ax[0].imshow(img_filtering, cmap='gray')
ax[0].set_title('Citra Asli')

ax[1].imshow(img_median_after, cmap='gray')
ax[1].set_title('After filter median')

ax[2].imshow(citra, cmap='gray')
ax[2].set_title('Original Image')

ax[3].imshow(output1, cmap='gray')
ax[3].set_title('Mean Filtered Image')

plt.show()

Kode ini menggabungkan empat subplot untuk menampilkan hasil pemrosesan citra dengan dua metode filtering yang berbeda: filter median dan filter rata-rata. Pertama, citra asli dan citra hasil filtering dengan filter median ditampilkan pada subplot pertama dan kedua dengan menggunakan skala abu-abu (cmap='gray'). Subplot ketiga dan keempat menampilkan citra asli dan hasil filtering dengan filter rata-rata secara berurutan. Penggunaan `figsize` yang diberikan adalah (7, 9), yang mengatur ukuran total dari gambar subplot. Dengan plot ini, perbandingan visual antara efek dari kedua metode filtering dapat dengan jelas diamati, memungkinkan untuk memahami efek dari masing-masing teknik dalam memproses citra.

