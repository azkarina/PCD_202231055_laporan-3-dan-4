# Laporan Praktikum 

Repository ini dibuat untuk menyelesaikan tugas laporan praktikum yang membahas mengenai **edge detection** dan **ekstraksi fitur**

## Edge Detection

Edge Detection yang kita kenal juga dengan deteksi tepi adalah cara-cara matematis untuk mengenali titik-titik dalam citra digital yang kecerahannya berubah drastis atau, secara formal, memiliki diskontinuitas. 

### Tahapan program
1. Import library
library yang digunakan adalah cv2, numpy, dan matplotlib
    
* **cv2** digunakan untuk memproses gambar
* **numpy** digunakan untuk melakukan operasi matematika, mengubah bentuk array, dan menghitung statistik
* **matplotlib** digunakan untuk memvisualisasi data 

2. Memanggil gambar
Dengan menggunakan fungsi imread yang ada di library cv2 kita bisa memanggil gambar dari device.

3. Konversi citra dari RGB ke GRAY
Dengan memanfaatkan fungsi cvtColor yang dimiliki cv2 kita bisa mengubah citra yang awalnya bermodel RGB (memiliki 3 saluran warna) dikonversi ke GRAY yang hanya memiliki 1 saluran warna. Konversi citra ini dilakukan agar mendapatkan hasil yang baik.

4. Mendeteksi ambang batas dari tepi
Dengan menggunakan fungsi canny yang dimiliki cv2 kita bisa mendeteksi ambang batas tepi dari sebuah citra.
Paramater yang ada dalam fungsi canny
    
    cv2.Canny(image,100,150) 
* **image** yang merupakan citra yang ingin di deteksi tepinya
* **100** yang merupakan ambang bawah sebuah piksel dianggap sebagai tepi. Semakin rendah nilainya semakin banyak tepi yang terdeteksi.
* **150** yang merupakan ambang atas yang menghubungkan piksel piksel yang membentuk tepi. Semakin besar nilainya semakin sedikit tepi yang terhubung.

Fungsi ini akan menghasilkan citra biner, dimana piksel yang dianggap tepi akan diberi nilai 255(putih) dan yang lainnya 0(hitam)

5. Transformasi hough
Transformasi Hough merupakan salah satu metode pengolahan citra yang dapat digunakan untuk mendeteksi garis dan lingkaran pada suatu citra digital. Metode ini bekerja dengan cara mencari hubungan ketetanggaan antar piksel menggunakan persamaan garis lurus untuk mendeteksi garis dan persamaan lingkaran untuk mendeteksi lingkaran.

    cv2.HoughLinesP(edges, 1, np.pi/180, 225, maxLineGap=65)

Fungsi ini menghitung garis-garis yang terdeteksi dalam citra menggunakan Transformasi Hough Probabilistik. Paramater dalam fungsi ini antara lain:
* **edges** yang merupakan hasil deteksi tepi menggunakan fungsi canny
* **1** adalah resolusi jarak dari titik ke garis yang akan dihitung dalam piksel. 
* **np.pi/180** adalah resolusi sudut dalam radian antara garis yang terdeteksi. Nilai ini umum dipakai untuk mendeteksi garis lurus.
* **225** merupakan ambang batas (threshold) untuk menganggap suatu garis terdeteksi. Semakin besar nilainya mengakibatkan semakin sedikit garis yang terdeteksi.

* **maxLineGap=65** merupajan jarak maksimum antara dua titik yang dianggap sebagai bagian dari garis yang sama.  Semakin besar nilainya memungkinkan semakin banyak garis yang lebih terputus-putus untuk dideteksi.

6. Menggambar garis
Dengan menggunakan looping kita akan mengiterasi  setiap garis yang terdeteksi oleh metode Hough Probabilistik untuk digambarkan garis. Setiap garis ini direpresentasikan oleh x1,y1 sebagai titik awal dan x2,y2 sebagai titik akhir

    cv2.line(image_line, (x1, y1), (x2, y2), (255,0,0), 4)

Dengan menggunakan fungsi line kita akan menggambar garis. Paramaternya antara lain:
* **image_line** yang merupakan salinan citra asli yang berformat rgb, kalau kita salin citra yang berformat gray maka garisnya nanti ikutan gray
* **x1,y1** titik awal garis
* **x2,y2** titik akhir garis
* **(255, 0, 0)** warna garis merah (dalam format RGB), kita bisa ganti dengan warna lain tinggal menyesuaikan saja.
* **4** ini adalah ketebalan garisnya, bisa diubah sesuai dengan keinginan kita 

## Ekstraksi Fitur

### Apa itu ekstraksi fitur?
Ekstraksi fitur adalah proses untuk mengambil informasi penting dari gambar atau data lain yang dapat digunakan untuk analisis lebih lanjut. Dalam konteks gambar, fitur bisa berupa warna, tekstur, bentuk, atau tepi objek dalam gambar. Tujuan utama dari ekstraksi fitur adalah untuk mereduksi data yang besar menjadi representasi yang lebih kecil dan informatif yang dapat digunakan untuk tugas-tugas seperti pengenalan pola, klasifikasi, atau deteksi objek.

### Apa itu GLCM?
GLCM (Grey-Level Co-Occurrence Matrix) adalah metode statistik untuk menganalisis tekstur dalam gambar. GLCM mengukur frekuensi pasangan piksel dengan nilai-nilai intensitas tertentu yang terjadi pada jarak tertentu satu sama lain. Dari GLCM, kita bisa menghitung berbagai fitur tekstur seperti kontras, homogenitas, energi, dan korelasi. GLCM dapat diartikan sebagai matriks yang menggambarkan hubungan antara intensitas piksel yang berdekatan dalam gambar.

### Apa itu HSV?
HSV adalah representasi warna yang lebih mendekati persepsi manusia dibandingkan dengan ruang warna RGB. Dalam HSV, fitur warna dapat diekstraksi dengan lebih mudah karena nilai Hue (H) mewakili jenis warna, Saturation (S) mewakili intensitas atau kejenuhan warna, dan Value (V) mewakili kecerahan.
* **Hue(H) - Warna**
    - Hue mewakili jenis warna dan dinyatakan sebagai sudut dalam derajat pada roda warna (color wheel).
    - Hue memberikan informasi tentang panjang gelombang dominan warna
    - Sudut 0° dan 360° adalah merah, 120° adalah hijau, dan 240° adalah biru.

* **Saturation (S) - Kejenuhan:**
    - Saturation menunjukkan seberapa murni atau intens warna tersebut.
    - Nilai saturasi berkisar dari 0 hingga 1.
    - Saturation 0 berarti warna tersebut adalah abu-abu (tidak ada kejenuhan), sedangkan saturasi 1 berarti warna tersebut sangat jenuh (murni).

* **Value (V) - Kecerahan:**

    - Value menunjukkan seberapa terang atau gelap warna tersebut.
    - Nilai value berkisar dari 0 hingga 1.
    - Value 0 berarti warna tersebut sepenuhnya hitam (tidak ada kecerahan), sedangkan value 1 berarti warna tersebut sepenuhnya terang.

Keuntungan dari penggunaan HSV :
* Lebih Mendekati Persepsi Manusia:
Ruang warna HSV lebih mendekati cara mata manusia dan otak kita memandang warna. Ini membuatnya lebih intuitif untuk tugas-tugas seperti penyesuaian warna dan pengenalan warna.

* Kegunaan dalam Pengolahan Citra:
HSV sering digunakan dalam pengolahan citra untuk tugas-tugas seperti deteksi objek, segmentasi warna, dan penyesuaian warna karena komponen Hue memberikan informasi warna yang lebih stabil di bawah variasi pencahayaan.

### Bagaimana menghubungkan ekstraksi fitur dengan GLCM
Ekstraksi fitur dengan GLCM melibatkan langkah-langkah berikut:
* Menghitung GLCM untuk gambar pada jarak dan sudut tertentu.
* Menghitung fitur tekstur dari GLCM, seperti kontras, homogenitas, energi, dan korelasi.
* Menggunakan fitur-fitur ini untuk analisis lebih lanjut atau klasifikasi.

### Tahapan Program
1. Import library

library yang digunakan adalah cv2, numpy, matplotlib, dan skimage.

    import cv2
    import numpy as np
    import matplotlib.pyplot as plt
    %matplotlib inline

    from skimage.color import rgb2hsv
    from skimage.feature import graycomatrix, graycoprops 
    
* **cv2** digunakan untuk memproses gambar
* **numpy** digunakan untuk melakukan operasi matematika, mengubah bentuk array, dan menghitung statistik
* **matplotlib** digunakan untuk memvisualisasi data 
* **skimage** dari library ini kita akan mengambil beberapa fungsi, yaitu:
    * **rgb2hsv** fungsi ini berada dalam modul color. Fungsi ini digunakan untuk mengonversi gambar dari ruang warna RGB ke HSV (Hue, Saturation, Value)
    * **graycomatrix** fungsi ini berada dalam modul feature. Fungsi ini digunakan untuk menghitung GLCM dari citra. 
    * **graycoprops** fungsi ini berada dalam modul feature. Fungsi ini digunakan untuk menghitung properti dari GLCM yang dihasilkan oleh graycomatrix. Properti ini mencakup fitur-fitur seperti energi, kontras, homogenitas, korelasi, dan entropy.

2. Import gambar
Dengan menggunakan fungsi imread yang ada di library cv2 kita bisa memanggil gambar dari device.

3. Konversi RGB ke HSV
Karena kita sudah mengimport rgb2hsv dari library skimage. Kita bisa langsung mengonversi dari rgb2hsv. 

4. Memisahkan Hue, Saturation, dan Value
Dikarenakan citra ini memiliki 3 saluran warna, sedangkan ekstraksi fitur tidak bisa memproses 3 saluran warna secara sekaligus. Untuk itu kita akan memisahkan semua saluran warna yang ada, yaitu H, S, dan V. 
    * Hue ada di index ke 0
    * Saturation ada di index ke 1
    * Value ada di index ke 2

Saat menampilkan gambarnya:
    * Hue menggunakan cmap hsv karena dapat memvisualisasikan perbedaan warna dengan lebih baik, karena mode warna HSV memperhitungkan komponen Hue
    * Saturation menggunakan cmap gray agar kita mengonversi nilai saturasi menjadi skala keabuan, sehingga kita dapat melihat perbedaan intensitas warna dengan lebih jelas.
    * Value menggunakan cmap gray karena untuk menampilkan kecerahan piksel dalam gambar dengan jelas 

5. Menghitung mean dan standar deviasi
Dalam konteks GLCM :
    * Menghitung rata-rata intensitas piksel pada gambar memberikan informasi tentang kecerahan keseluruhan gambar.
    * Nilai standar deviasi yang tinggi menunjukkan variasi yang besar dalam intensitas piksel.

6. Konversi HSV channels
Karena citra ini awalnya menyimpan data dalam bentuk float disebabkan nilai dalam mode HSV biasanya dalam rentang 0 - 1. Sehingga kita perlu mengubahnya ke bentuk int dengan cara mengalikan setiap komponen dengan 255 dan mengonversi hasilnya ke tipe data uint8. Tipe data ini hanya bisa menyimpan nilai non negatif dari 0 sampai 255.

7. Fungsi untuk menghitung GLCM
Agar kita tidak perlu melakukan perhitungan glcm untuk setiap saluran. Kita bisa membuat fungsi dengan paramater yang diberi nama channel yang di dalamnya terdapat perhitungan GLCM. Sehingga nantinya jika kita ingin menghitung fitur GLCM pada channel lain, kita hanya perlu memanggil fungsi ini dengan channel yang berbeda. Fungsi ini menghitung fitur GLCM seperti kontras, dissimilarity, homogenitas, energi, dan korelasi.

8. Menampilkan nilai yang ada di hue_channel
Kita bisa panggil fungsi yang udah kita buat tadi dan masukkan hue_channel sebagai paramater dan program akan langsung memprosesnya. 
Setelah menghitung fitur GLCM, kita ingin menampilkan nilai-nilai fitur tersebut.
Baris-baris berikutnya mencetak nilai kontras, dissimilarity, homogenitas, energi, dan korelasi pada channel Hue.

9. Menampilkan nilai yang ada di saturation_channel
Kita bisa panggil fungsi yang udah kita buat tadi dan masukkan saturation_channel sebagai paramater dan program akan langsung memprosesnya. 
Setelah menghitung fitur GLCM, kita ingin menampilkan nilai-nilai fitur tersebut.
Baris-baris berikutnya mencetak nilai kontras, dissimilarity, homogenitas, energi, dan korelasi pada channel Saturation.

10. Menampilkan nilai yang ada di value_channel
Kita bisa panggil fungsi yang udah kita buat tadi dan masukkan value_channel sebagai paramater dan program akan langsung memprosesnya. 
Setelah menghitung fitur GLCM, kita ingin menampilkan nilai-nilai fitur tersebut.
Baris-baris berikutnya mencetak nilai kontras, dissimilarity, homogenitas, energi, dan korelasi pada channel Value.



