
# PROJECT UTS PENGOLAHAN CITRA 2024

Ketentuan Project :
- Potretlah sebuah citra yang berisi Nama Lengkap masing-masing
- Nama ditulis tangan menggunakan pena dengan tinta Merah,hijau,dan biru
- Pemilihan uratan warna dibebaskan.

Pengerjaan project menggunakan bahasa python dan yang dikerjakan sebegai berikut :
1. Deteksi warna pada citra
2. Carilah dan urutkan ambang batas terkecil sampai terbesar





## Authors

- [@angelnatassya](https://www.github.com/angelnatassya)


## Aplikasi

 Gunakan aplikasi Jupiter Notebook pada Anaconda Navigator.
 
 Gambar Inputan :
 
 ![Nama](https://github.com/angelnatassya/pcd_uts/blob/main/nm.jpg)

 Bukti Pengambilan Gambar :

 ![Nama](https://github.com/angelnatassya/pcd_uts/blob/main/loc.jpg)


1. Deteksi warna pada Citra
   
⁂ Pendeteksian Warna Biru
- Import Library yang akan digunakan.
```bash
import cv2
import matplotlib.pyplot as plt
import numpy as np
```
- Import image (nama file 'nm').
```bash
img=cv2.imread('nm.jpg')
```
- Ubah warna gambar dari format BGR (Blue-Green-Red) menjadi HSV (Hue-Saturation-Value)
```bash
hsv_img = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
```
- Deteksi warna menggunakan HSV
```bash
lower_blue = np.array([90, 50, 50])
upper_blue = np.array([130, 255, 255])
```
- Gunakan mask untuk menggunakan rentang warna tertentu dari HSV
```bash
mask = cv2.inRange(hsv_img, lower_blue, upper_blue)
```
- Tampilkan gambar asli dan histogram menggunakan perintah berikut
```bash
plt.figure(figsize=(12, 6))
plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Gambar Asli')

plt.subplot(2, 2, 2)
plt.hist(img.ravel(), 256, [0, 256])
plt.title('Histogram Gambar Asli')
```
![hist](https://github.com/angelnatassya/pcd_uts/blob/main/histogramasli.png)
"Histogram pada gambar original menunjukkan distribusi intensitas piksel dari kiri ke kanan. Jika histogram lebih tinggi dari 200 hingga 250, itu menandakan bahwa ada banyak piksel dalam gambar yang memiliki intensitas tinggi dalam rentang tersebut. Hal ini mengindikasikan adanya area dalam gambar dengan intensitas yang signifikan di antara 200 dan 250."
- Mask deteksi biru dan histogram
```bash
plt.subplot(2, 2, 3)
plt.imshow(mask, cmap='gray')
plt.title('Mask Deteksi Warna Biru')

plt.subplot(2, 2, 4)
plt.hist(mask.ravel(), 256, [0, 256])
plt.title('Histogram Mask Deteksi Warna Biru')

plt.show()
```
![hist](https://github.com/angelnatassya/pcd_uts/blob/main/histoblue.png)
"Histogram hanya berada di 0, tetapi semakin tinggi ketika naik, itu berarti bahwa sebagian besar piksel dalam gambar memiliki intensitas yang rendah, mungkin mendekati nol, namun ada beberapa piksel yang memiliki intensitas yang tinggi.

Ini bisa menunjukkan bahwa gambar tersebut mungkin memiliki banyak area yang gelap atau mendekati hitam, tetapi ada beberapa titik terang yang memiliki intensitas yang cukup tinggi. Misalnya, ini bisa terjadi dalam gambar dengan latar belakang gelap di mana ada objek yang cukup terang atau terang. Histogram yang hanya berada di 0 menunjukkan bahwa gambar secara keseluruhan cenderung gelap atau memiliki intensitas rendah, sementara tingginya histogram ketika naik menunjukkan adanya area dalam gambar dengan intensitas yang lebih tinggi."


⁂ Pendeteksian Warna Merah
- Import Library yang akan digunakan.
```bash
import cv2
import matplotlib.pyplot as plt
import numpy as np
```
- Import image (nama file 'nm').
```bash
img=cv2.imread('nm.jpg')
```
- Ubah warna gambar dari format BGR (Blue-Green-Red) menjadi HSV(Hue-Saturation-Value)
```bash
hsv_img = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
```
- Deteksi warna merah yang telah dikonversi ke warna HSV. Lalu pada akhir kode gabungan dua mask yang telah dibuat sebelumnya untuk menambah elemen wise.
```bash
lower_red = np.array([0, 100, 100])
upper_red = np.array([10, 255, 255])
mask1 = cv2.inRange(hsv_img, lower_red, upper_red)

lower_red = np.array([160, 100, 100])
upper_red = np.array([179, 255, 255])
mask2 = cv2.inRange(hsv_img, lower_red, upper_red)

red_mask = mask1 + mask2
```
- Tampilkan gambar asli dan histogram menggunakan perintah berikut
```bash
plt.figure(figsize=(12, 6))
plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Gambar Asli')

plt.subplot(2, 2, 2)
plt.hist(img.ravel(), 256, [0, 256])
plt.title('Histogram Gambar Asli')
```
![hist](https://github.com/angelnatassya/pcd_uts/blob/main/histogramasli.png)
"Histogram pada gambar original menunjukkan distribusi intensitas piksel dari kiri ke kanan. Jika histogram lebih tinggi dari 200 hingga 250, itu menandakan bahwa ada banyak piksel dalam gambar yang memiliki intensitas tinggi dalam rentang tersebut. Hal ini mengindikasikan adanya area dalam gambar dengan intensitas yang signifikan di antara 200 dan 250."
- Mask deteksi merah dan histogram
```bash
fig, axs = plt.subplots(1, 2, figsize=(12, 6))

axs[0].imshow(red_mask, cmap='gray')
axs[0].set_title('Deteksi Warna Merah')

red_hist = cv2.calcHist([img], [0], red_mask, [256], [0, 256])
axs[1].plot(red_hist, color='r')
axs[1].set_title('Histogram Deteksi Warna Merah')

plt.show()
```
![hist](https://github.com/angelnatassya/pcd_uts/blob/main/histored.png)
"Histogram tersebut mengindikasikan bahwa sebagian besar piksel dalam gambar memiliki intensitas vertikal di sekitar 100, yang menandakan adanya garis vertikal atau struktur tegak lurus. Di sisi lain, intensitas horizontal di sekitar 250 menunjukkan adanya struktur horizontal atau tinggi tertentu dalam gambar. Dengan demikian, histogram tersebut memberikan gambaran tentang pola dan orientasi garis-garis dalam gambar, dengan garis vertikal mendominasi dalam hal intensitas vertikal dan struktur horizontal mendominasi dalam hal intensitas horizontal."


⁂ Pendeteksian Warna Hijau
- Import Library yang akan digunakan.
```bash
import cv2
import matplotlib.pyplot as plt
import numpy as np
```
- Import image (nama file 'nm').
```bash
img=cv2.imread('nm.jpg')
```
- Ubah warna gambar dari format BGR (Blue-Green-Red) menjadi HSV(Hue-Saturation-Value)
```bash
hsv_img = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
```
- Deteksi warna hijau yang telah dikonversi ke warna HSV.
```bash
lower_green = np.array([35, 100, 100])
upper_green = np.array([90, 255, 255])
green_mask = cv2.inRange(hsv_img, lower_green, upper_green)
```
- Tampilkan gambar asli dan histogram menggunakan perintah berikut
```bash
plt.figure(figsize=(12, 6))
plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Gambar Asli')

plt.subplot(2, 2, 2)
plt.hist(img.ravel(), 256, [0, 256])
plt.title('Histogram Gambar Asli')
```
![hist](https://github.com/angelnatassya/pcd_uts/blob/main/histogramasli.png)
"Histogram pada gambar original menunjukkan distribusi intensitas piksel dari kiri ke kanan. Jika histogram lebih tinggi dari 200 hingga 250, itu menandakan bahwa ada banyak piksel dalam gambar yang memiliki intensitas tinggi dalam rentang tersebut. Hal ini mengindikasikan adanya area dalam gambar dengan intensitas yang signifikan di antara 200 dan 250."
- Mask deteksi hijau dan histogram
```bash
fig, axs = plt.subplots(1, 2, figsize=(12, 6))
axs[0].imshow(green_mask, cmap='gray')
axs[0].set_title('Deteksi Warna Hijau')

green_hist = cv2.calcHist([img], [1], green_mask, [256], [0, 256])
axs[1].plot(green_hist, color='g')
axs[1].set_title('Histogram Deteksi Warna Hijau')

plt.show()
```
![hist](https://github.com/angelnatassya/pcd_uts/blob/main/histogreen.png)
"Histogram tersebut menunjukkan bahwa sebagian besar piksel dalam gambar memiliki intensitas vertikal yang cukup tinggi, mendekati nilai 80, yang menunjukkan adanya fitur vertikal yang dominan atau mungkin ada area dengan intensitas yang tinggi pada bagian vertikal gambar. Di sisi lain, intensitas horizontal di sekitar 250 menunjukkan adanya struktur horizontal yang signifikan dalam gambar. Namun, area dengan intensitas di rentang 0-50 yang datar menandakan bahwa ada sedikit perubahan intensitas di sepanjang sumbu horizontal dalam rentang tersebut."


2. Ambang Batas
   
⁂ Ambang batas biru
- - Import Library yang akan digunakan.
```bash
import cv2
import matplotlib.pyplot as plt
import numpy as np
```
- Import image (nama file 'nm').
```bash
img=cv2.imread('nm.jpg')
```
- Ubah warna gambar dari format BGR (Blue-Green-Red) menjadi HSV (Hue-Saturation-Value)
```bash
hsv_img = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
```
- Deteksi ambang batas bawah dan atas warna menggunakan HSV
```bash
lower_blue = np.array([90, 50, 50])
upper_blue = np.array([130, 255, 255])
```
- Penerapan masker biru pada gambar
```bash
blue_mask = cv2.inRange(hsv_img, lower_blue, upper_blue)
blue_image = cv2.bitwise_and(img, img, mask=blue_mask)
```
- Menampilkan gambar original dan deteksi biru
```bash
plt.figure(figsize=(12, 6))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(blue_image, cv2.COLOR_BGR2RGB))
plt.title('Blue Image')
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Original Image')
plt.axis('off')

plt.show()
```
![hist](https://github.com/angelnatassya/pcd_uts/blob/main/blue.png)

⁂ Pendeteksian Warna Merah-Biru
- Import Library yang akan digunakan.
```bash
import cv2
import matplotlib.pyplot as plt
import numpy as np
```
- Import image (nama file 'nm').
```bash
img=cv2.imread('nm.jpg')
```
- Ubah warna gambar dari format BGR (Blue-Green-Red) menjadi HSV(Hue-Saturation-Value)
```bash
hsv_img = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
```
- Deteksi warna merah yang telah dikonversi ke warna HSV. Lalu pada akhir kode gabungan dua mask yang telah dibuat sebelumnya untuk menambah elemen wise.
```bash
lower_red = np.array([0, 100, 100])
upper_red = np.array([10, 255, 255])
mask1 = cv2.inRange(hsv_img, lower_red, upper_red)

lower_red = np.array([160, 100, 100])
upper_red = np.array([179, 255, 255])
mask2 = cv2.inRange(hsv_img, lower_red, upper_red)

red_mask = mask1 + mask2
```
- Deteksi ambang batas bawah dan atas warna menggunakan HSV
```bash
lower_blue = np.array([90, 50, 50])
upper_blue = np.array([130, 255, 255])
```
- Penerapan masker biru pada gambar
```bash
blue_mask = cv2.inRange(hsv_img, lower_blue, upper_blue)
```
- Menampilkan dua gambar secara berdampingan: gambar asli dan hasil deteksi warna merah dan biru yang digabungkan.
```bash
fig, axs = plt.subplots(1, 2, figsize=(12, 6))
axs[0].imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
axs[0].set_title('Original Image')

result = cv2.bitwise_or(red_mask, blue_mask)
axs[1].imshow(result, cmap='gray')
axs[1].set_title('Red and Blue Detection')

plt.show()
```
![hist](https://github.com/angelnatassya/pcd_uts/blob/main/rb.png)

⁂ Pendeteksian Warna Merah-Biru-Hijau
- Import Library yang akan digunakan.
```bash
import cv2
import matplotlib.pyplot as plt
import numpy as np
```
- Import image (nama file 'nm').
```bash
img=cv2.imread('nm.jpg')
```
- Ubah warna gambar dari format BGR (Blue-Green-Red) menjadi HSV(Hue-Saturation-Value)
```bash
hsv_img = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
```
- Deteksi warna merah yang telah dikonversi ke warna HSV. Lalu pada akhir kode gabungan dua mask yang telah dibuat sebelumnya untuk menambah elemen wise.
```bash
lower_red = np.array([0, 100, 100])
upper_red = np.array([10, 255, 255])
mask1 = cv2.inRange(hsv_img, lower_red, upper_red)

lower_red = np.array([160, 100, 100])
upper_red = np.array([179, 255, 255])
mask2 = cv2.inRange(hsv_img, lower_red, upper_red)

red_mask = mask1 + mask2
```
- Deteksi ambang batas bawah dan atas warna menggunakan HSV
```bash
lower_blue = np.array([90, 50, 50])
upper_blue = np.array([130, 255, 255])
```
- Penerapan masker biru pada gambar
```bash
blue_mask = cv2.inRange(hsv_img, lower_blue, upper_blue)
```
- Deteksi warna hijau yang telah dikonversi ke warna HSV.
```bash
lower_green = np.array([35, 100, 100])
upper_green = np.array([90, 255, 255])
green_mask = cv2.inRange(hsv_img, lower_green, upper_green)
result = cv2.bitwise_or(red_mask, blue_mask, green_mask)
```
- Menampilkan dua gambar secara berdampingan: gambar asli dan hasil deteksi gabungan warna merah, biru, dan hijau.
```bash
fig, axs = plt.subplots(1, 2, figsize=(12, 6))
axs[0].imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
axs[0].set_title('Original Image')

axs[1].imshow(result, cmap='gray')
axs[1].set_title('Red, Blue, and Green Detection')

plt.show()
```
![hist](https://github.com/angelnatassya/pcd_uts/blob/main/rgb.png)

## Penjelasan Rinci
1. Deteksi warna pada Citra
   
   ⁂ Deteksi Biru
   
   ![hist](https://github.com/angelnatassya/pcd_uts/blob/main/detblue.png)

   ![hist](https://github.com/angelnatassya/pcd_uts/blob/main/subblue.png)
   
- Mengimpor library yang diperlukan:
  ▸ cv2: Digunakan untuk membaca gambar dan melakukan konversi warna.
  ▸ matplotlib.pyplot as plt: Digunakan untuk membuat plot dan menampilkan gambar.
  ▸ numpy as np: Digunakan untuk operasi numerik.
- Membaca gambar 'nm.jpg' menggunakan cv2.imread() dan menyimpannya dalam variabel img.
- Mengonversi gambar dari format BGR menjadi format HSV menggunakan cv2.cvtColor() dan menyimpannya dalam variabel hsv_img.
- Mendefinisikan rentang warna biru dalam format HSV dengan lower_blue dan upper_blue.
- Membuat masker (mask) untuk deteksi warna biru menggunakan cv2.inRange() dan menyimpannya dalam variabel mask.
- Membuat sebuah gambar subplot dengan ukuran 2x2 menggunakan plt.figure(figsize=(12, 6)).
- Menampilkan gambar asli di subplot (2, 2, 1) menggunakan plt.subplot() dan plt.imshow().
- Membuat histogram dari gambar asli di subplot (2, 2, 2) menggunakan plt.hist().
- Menampilkan masker deteksi warna biru di subplot (2, 2, 3) menggunakan plt.imshow() dengan cmap='gray' untuk menampilkan dalam skala abu-abu.
- Membuat histogram dari masker deteksi warna biru di subplot (2, 2, 4) menggunakan plt.hist().
- Menampilkan keseluruhan gambar subplot menggunakan plt.show().

   ⁂ Deteksi Merah
  
   ![hist](https://github.com/angelnatassya/pcd_uts/blob/main/detred.png)
  
   ![hist](https://github.com/angelnatassya/pcd_uts/blob/main/subred.png)
  
- Mengimpor library yang diperlukan:
  ▸ cv2: Digunakan untuk membaca gambar dan melakukan konversi warna.
  ▸ matplotlib.pyplot as plt: Digunakan untuk membuat plot dan menampilkan gambar.
  ▸ numpy as np: Digunakan untuk operasi numerik.
- Membaca gambar 'nm.jpg' menggunakan cv2.imread() dan menyimpannya dalam variabel img.
- Mengonversi gambar dari format BGR menjadi format HSV menggunakan cv2.cvtColor() dan menyimpannya dalam variabel hsv_img.
- Mendefinisikan dua rentang warna merah dalam format HSV menggunakan lower_red dan upper_red. Karena warna merah melintasi batas 0 dan 179 dalam skala Hue, dua rentang digunakan untuk menangkap seluruh rentang warna merah.
- Membuat dua masker (mask1 dan mask2) untuk setiap rentang warna merah menggunakan cv2.inRange().
- Menggabungkan dua masker menggunakan operasi penjumlahan elemen-wise (+) dan menyimpannya dalam variabel red_mask.
- Membuat gambar subplot dengan ukuran 2x2 menggunakan plt.figure(figsize=(12, 6)).
- Menampilkan gambar asli di subplot (2, 2, 1) menggunakan plt.subplot() dan plt.imshow().
- Membuat histogram dari gambar asli di subplot (2, 2, 2) menggunakan plt.hist().
- Membuat subplot tambahan untuk menampilkan hasil deteksi warna merah dan histogram deteksi warna merah di samping gambar asli dan histogramnya. Ini dilakukan dengan membuat sebuah gambar subplot baru menggunakan plt.subplots() dengan 1 baris dan 2 kolom.
- Menampilkan hasil deteksi warna merah di subplot pertama menggunakan axs[0].imshow() dan axs[0].set_title(). Ini menampilkan red_mask dalam skala abu-abu.
- Menghitung histogram dari hasil deteksi warna merah menggunakan cv2.calcHist() dan menampilkannya di subplot kedua sebagai plot garis menggunakan axs[1].plot().
- Menetapkan judul untuk subplot kedua menggunakan axs[1].set_title().
- Terakhir, menampilkan gambar subplot keseluruhan menggunakan plt.show().

   ⁂ Deteksi Hijau
  
   ![hist](https://github.com/angelnatassya/pcd_uts/blob/main/detgreen.png)
  
   ![hist](https://github.com/angelnatassya/pcd_uts/blob/main/subgreen.png)
  
- Mengimpor library yang diperlukan:
  ▸ cv2: Digunakan untuk membaca gambar dan melakukan konversi warna.
  ▸ matplotlib.pyplot as plt: Digunakan untuk membuat plot dan menampilkan gambar.
  ▸ numpy as np: Digunakan untuk operasi numerik.
- Membaca gambar 'nm.jpg' menggunakan cv2.imread() dan menyimpannya dalam variabel img.
- Mengonversi gambar dari format BGR menjadi format HSV menggunakan cv2.cvtColor() dan menyimpannya dalam variabel hsv_img.
- Mendefinisikan rentang warna hijau dalam format HSV dengan lower_green dan upper_green.
- Membuat masker (mask) untuk deteksi warna hijau menggunakan cv2.inRange() dan menyimpannya dalam variabel green_mask.
- Membuat sebuah gambar subplot dengan ukuran 2x2 menggunakan plt.figure(figsize=(12, 6)).
- Menampilkan gambar asli di subplot (2, 2, 1) menggunakan plt.subplot() dan plt.imshow().
- Membuat histogram dari gambar asli di subplot (2, 2, 2) menggunakan plt.hist().
- Membuat subplot tambahan untuk menampilkan hasil deteksi warna hijau dan histogram deteksi warna hijau di samping gambar asli dan histogramnya. Ini dilakukan dengan membuat sebuah gambar subplot baru menggunakan plt.subplots() dengan 1 baris dan 2 kolom.
- Menampilkan hasil deteksi warna hijau di subplot pertama menggunakan axs[0].imshow() dan axs[0].set_title(). Ini menampilkan green_mask dalam skala abu-abu.
- Menghitung histogram dari hasil deteksi warna hijau menggunakan cv2.calcHist() dan menampilkannya di subplot kedua sebagai plot garis menggunakan axs[1].plot().
- Menetapkan judul untuk subplot kedua menggunakan axs[1].set_title().
- Terakhir, menampilkan gambar subplot keseluruhan menggunakan plt.show().

2. Ambang Batas

   ⁂ Ambang Batas Biru
   
   ![hist](https://github.com/angelnatassya/pcd_uts/blob/main/batblue.png)
   
- Mengimpor library yang diperlukan:
  ▸ cv2: Digunakan untuk membaca gambar dan melakukan konversi warna.
  ▸ matplotlib.pyplot as plt: Digunakan untuk membuat plot dan menampilkan gambar.
  ▸ numpy as np: Digunakan untuk operasi numerik.
- Membaca gambar 'nm.jpg' menggunakan cv2.imread() dan menyimpannya dalam variabel img.
- Mengonversi gambar dari format BGR menjadi format HSV menggunakan cv2.cvtColor() dan menyimpannya dalam variabel hsv_img.
- Menggunakan fungsi cv2.bitwise_and() untuk menerapkan masker warna biru (blue_mask) pada gambar asli (img). Ini akan menghasilkan gambar yang hanya menampilkan area berwarna biru dari gambar asli.
- Membuat sebuah gambar subplot dengan ukuran 1x2 menggunakan plt.figure(figsize=(12, 6)).
- Menampilkan gambar dengan area berwarna biru yang telah dideteksi di subplot pertama (1, 2, 1) menggunakan plt.subplot() dan plt.imshow(). Gambar yang telah diterapkan masker warna biru diubah ke format RGB sebelum ditampilkan.
- Menampilkan gambar asli di subplot kedua (1, 2, 2) menggunakan plt.subplot() dan plt.imshow().
- Memberikan judul untuk setiap subplot menggunakan plt.title().
- Menonaktifkan penanda sumbu pada kedua subplot menggunakan plt.axis('off').
- Terakhir, menampilkan gambar subplot keseluruhan menggunakan plt.show().

  ⁂ Ambang Batas Merah-Biru
  
  ![hist](https://github.com/angelnatassya/pcd_uts/blob/main/batrb.png)
  
 - Mengimpor library yang diperlukan:
  ▸ cv2: Digunakan untuk membaca gambar dan melakukan konversi warna.
  ▸ matplotlib.pyplot as plt: Digunakan untuk membuat plot dan menampilkan gambar.
  ▸ numpy as np: Digunakan untuk operasi numerik.
- Membaca gambar 'nm.jpg' menggunakan cv2.imread() dan menyimpannya dalam variabel img.
- Mengonversi gambar dari format BGR menjadi format HSV menggunakan cv2.cvtColor() dan menyimpannya dalam variabel hsv_img.
- Mendefinisikan dua rentang warna merah dalam format HSV menggunakan nilai-nilai yang ditentukan dalam array lower_red1, upper_red1, lower_red2, dan upper_red2.
- Menggunakan fungsi cv2.inRange() untuk membuat dua masker (mask1 dan mask2) yang menandai area gambar yang memiliki warna dalam rentang warna merah yang ditentukan.
- Menggabungkan dua masker merah menggunakan operasi penjumlahan elemen-wise (+) dan menyimpannya dalam variabel red_mask.
- Mendefinisikan rentang warna biru dalam format HSV menggunakan nilai-nilai yang ditentukan dalam array lower_blue dan upper_blue.
- Menggunakan fungsi cv2.inRange() untuk membuat masker (blue_mask) yang menandai area gambar yang memiliki warna dalam rentang warna biru yang ditentukan.
- Membuat sebuah gambar subplot dengan ukuran 1x2 menggunakan plt.subplots() dan menampilkan gambar asli di subplot pertama. Kemudian, menggunakan operasi bitwise OR (cv2.bitwise_or()) untuk menggabungkan masker merah dan biru, dan menampilkan hasil deteksi warna merah dan biru di subplot kedua.
- Menambahkan judul untuk setiap subplot menggunakan axs[0].set_title() dan axs[1].set_title().
- Terakhir, menampilkan gambar subplot menggunakan plt.show().

  ⁂ Ambang Batas Merah-Biru-Hijau
  
  ![hist](https://github.com/angelnatassya/pcd_uts/blob/main/batgrb.png)
  
- Mengimpor library yang diperlukan:
  ▸ cv2: Digunakan untuk membaca gambar dan melakukan konversi warna.
  ▸ matplotlib.pyplot as plt: Digunakan untuk membuat plot dan menampilkan gambar.
  ▸ numpy as np: Digunakan untuk operasi numerik.
- Membaca gambar 'nm.jpg' menggunakan cv2.imread() dan menyimpannya dalam variabel img.
- Mengonversi gambar dari format BGR menjadi format HSV menggunakan cv2.cvtColor() dan menyimpannya dalam variabel hsv_img.
- Rentang warna untuk setiap warna (merah, biru, hijau) ditentukan dalam format HSV menggunakan nilai-nilai tertentu untuk lower dan upper.
- Setiap rentang warna digunakan untuk membuat masker menggunakan fungsi cv2.inRange() yang menandai area gambar yang memiliki warna dalam rentang yang ditentukan.
- Masker untuk setiap warna digabungkan menggunakan operasi penjumlahan elemen-wise (+). Ini dilakukan untuk mendapatkan satu masker yang menandai area gambar yang memiliki warna merah, biru, atau hijau.
- Gambar asli dan hasil deteksi warna digambarkan dalam subplot menggunakan plt.subplots(). Gambar asli ditampilkan di subplot pertama dan hasil deteksi warna digunakan untuk menghasilkan gambar biner yang menunjukkan area dengan warna merah, biru, atau hijau di subplot kedua.
- Terakhir, gambar subplot keseluruhan ditampilkan menggunakan plt.show().
