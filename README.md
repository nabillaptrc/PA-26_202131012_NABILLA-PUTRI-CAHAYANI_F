
# Teori

### A. HSV
HSV (Hue, Saturation, Value) adalah sebuah model warna yang digunakan untuk menggambarkan warna berdasarkan tiga komponen utama yaitu hue, saturation, dan value. Model warna HSV juga memungkinkan pemisahan warna dari faktor kecerahan, sehingga hasil deteksi lebih stabil terhadap perubahan kondisi pencahayaan.

### B. Batas Bawah & Batas Atas Warna HSV 
Merah [136, 87, 111] & [180, 255, 255]
Hijau [25, 52, 72] & [102, 255, 255]
Biru [94, 80, 2] & [120, 255, 255]
Coklat [5, 164, 61] & [25, 184, 141]
Kuning [25, 70, 120] & [30, 255, 255]
Oranye [10, 100, 20] & [25, 255, 255]
Cyan [85, 100, 20] & [95, 255, 255]
Black [0, 0, 0] & [50, 50, 50]

### C. Mask
Masking dalam pengolahan citra melibatkan penggunaan suatu matriks (maska) yang memiliki ukuran yang sama dengan citra yang akan dimaskakan. Setiap elemen dalam maska berisi nilai 0 atau 1, yang menentukan bagian mana dari citra yang akan diproses atau ditampilkan.

Penggunaan Mask
Mask digunakan untuk berbagai tujuan dalam pengolahan citra, antara lain:

Filtering: Maska dapat digunakan untuk menerapkan filter spasial pada citra, seperti filter blur, sharpening, atau edge detection, dengan memperhitungkan hanya piksel-piksel yang termasuk dalam maska.

Segmentasi: Maska dapat digunakan untuk memisahkan atau mengisolasi objek tertentu dalam citra berdasarkan fitur atau ciri khas tertentu, seperti warna, tekstur, atau bentuk.

Region of Interest (ROI): Maska dapat digunakan untuk menentukan wilayah tertentu (ROI) dalam citra yang akan diproses secara terpisah dari wilayah lainnya. Hal ini memungkinkan pengolahan atau analisis lebih fokus pada area yang diinginkan.

### D. Dilasi pada citra
Dilasi (dilation) adalah salah satu operasi dasar dalam pengolahan citra yang digunakan untuk memperluas atau memperbesar wilayah objek dalam citra. Operasi dilasi memungkinkan kita untuk mengisi celah atau retakan kecil dalam objek dan menghubungkan bagian-bagian objek yang berdekatan.

Proses Dilasi
Proses dilasi dapat dijelaskan sebagai berikut:

Letakkan kernel di atas setiap piksel dalam citra.
Jika terdapat setidaknya satu piksel dengan nilai non-nol dalam kernel yang berada di atas piksel objek, maka piksel tersebut akan ditandai sebagai piksel objek pada citra hasil dilasi.
Iterasikan proses di atas ke seluruh piksel dalam citra.
Efek Dilasi: Operasi dilasi pada dasarnya memperbesar wilayah objek dengan cara mengisi celah atau retakan kecil dalam objek dan menghubungkan bagian-bagian objek yang berdekatan. 

Hal ini berguna dalam berbagai aplikasi pengolahan citra, seperti:

Mengisi lubang: Dilasi dapat mengisi lubang kecil dalam objek, sehingga objek tampak lebih solid dan tidak terputus-putus.
Menghubungkan komponen: Dilasi dapat menghubungkan komponen atau bagian-bagian objek yang berdekatan, sehingga objek terlihat lebih terhubung atau utuh.

Memperbesar objek: Dilasi dapat memperbesar ukuran objek dengan jumlah iterasi yang lebih banyak, tergantung pada ukuran kernel yang digunakan.

### E. Bitwise Citra & Mask
Operasi Bitwise: Operasi bitwise melibatkan penggunaan operasi logika seperti AND, OR, XOR, dan NOT pada level bit. Dalam konteks maska citra, operasi bitwise yang umum digunakan adalah AND dan NOT. Operasi bitwise AND digunakan untuk menerapkan maska pada citra dengan mempertahankan piksel di mana maska bernilai 1, sedangkan operasi bitwise NOT digunakan untuk mengubah nilai piksel dalam maska.

Dilasi adalah teknik untuk memfilter noise yang berwarna hitam (0) menjadi warna putih (1) dan memperbesar segmen pada objek citra.

## Penjelasan Project
cv2: Library OpenCV (Open Source Computer Vision) digunakan untuk melakukan berbagai operasi pengolahan citra, seperti membaca citra, manipulasi citra, deteksi objek, dll.

numpy: Library NumPy (Numerical Python) digunakan untuk melakukan operasi matematika dan manipulasi array secara efisien.

matplotlib.pyplot: Library matplotlib digunakan untuk membuat visualisasi grafik dan plot, seperti menampilkan citra atau histogram.

cv2.imread('uas_buah1.jpg') adalah untuk menyimpan citra 'uas_buah1.jpg dalam variabel image. 

### Konversi Gambar ke HSV
hsv_image = cv2.cvtColor(image, cv2.COLOR_BGR2HSV) digunakan untuk mengubah citra dalam format BGR menjadi format HSV. Hasil konversi ini akan disimpan dalam variabel hsv_image.

### Menentukan Batas Atas & Bawah HSV
red_low: Array numpy dengan nilai [136, 87, 111]. Rentang ini menentukan batas bawah untuk komponen HSV, yaitu Hue = 136, Saturation = 87, dan Value = 111.
red_high: Array numpy dengan nilai [180, 255, 255]. Rentang ini menentukan batas atas untuk komponen HSV, yaitu Hue = 180, Saturation = 255, dan Value = 255. Rentang ini mencakup warna merah dalam spektrum HSV.

green_low: Array numpy dengan nilai [25, 52, 72]. Rentang ini menentukan batas bawah untuk komponen HSV, yaitu Hue = 25, Saturation = 52, dan Value = 72.
green_high: Array numpy dengan nilai [102, 255, 255]. Rentang ini menentukan batas atas untuk komponen HSV, yaitu Hue = 102, Saturation = 255, dan Value = 255. Rentang ini mencakup warna hijau dalam spektrum HSV.


orange_low: Array numpy dengan nilai [10, 100, 20]. Rentang ini menentukan batas bawah untuk komponen HSV, yaitu Hue = 10, Saturation = 100, dan Value = 20.
orange_high: Array numpy dengan nilai [25, 255, 255]. Rentang ini menentukan batas atas untuk komponen HSV, yaitu Hue = 25, Saturation = 255, dan Value = 255. Rentang ini mencakup warna oranye dalam spektrum HSV.

### Membuat Mask untuk Setiap Warna
red_mask: Menggunakan cv2.inRange() untuk membuat mask dari citra hsv_image dengan batas bawah red_low dan batas atas red_high. Hasilnya adalah sebuah citra biner (hitam-putih), di mana piksel yang termasuk dalam rentang warna merah akan menjadi putih (255), sedangkan piksel yang tidak termasuk dalam rentang tersebut akan menjadi hitam (0).

green_mask: Menggunakan cv2.inRange() untuk membuat mask dari citra hsv_image dengan batas bawah green_low dan batas atas green_high. Hasilnya adalah sebuah citra biner (hitam-putih), di mana piksel yang termasuk dalam rentang warna hijau akan menjadi putih (255), sedangkan piksel yang tidak termasuk dalam rentang tersebut akan menjadi hitam (0).

orange_mask: Menggunakan cv2.inRange() untuk membuat mask dari citra hsv_image dengan batas bawah orange_low dan batas atas orange_high. Hasilnya adalah sebuah citra biner (hitam-putih), di mana piksel yang termasuk dalam rentang warna oranye akan menjadi putih (255), sedangkan piksel yang tidak termasuk dalam rentang tersebut akan menjadi hitam (0).

### Proses Dilasi
Operasi dilasi berfungsi untuk memperluas wilayah piksel putih dalam mask dengan menggunakan kernel yang telah ditentukan.

dilated_red_mask: Menggunakan cv2.dilate() untuk melakukan dilasi pada red_mask dengan menggunakan kernel berukuran (70, 80) yang terdiri dari nilai 1. Operasi dilasi dilakukan sebanyak 1 iterasi. Dengan melakukan dilasi, wilayah piksel putih pada red_mask akan diperluas dan menghasilkan dilated_red_mask.

dilated_green_mask: Menggunakan cv2.dilate() untuk melakukan dilasi pada green_mask dengan menggunakan kernel berukuran (5, 5) yang terdiri dari nilai 1. Operasi dilasi dilakukan sebanyak 1 iterasi. Dengan melakukan dilasi, wilayah piksel putih pada green_mask akan diperluas dan menghasilkan dilated_green_mask.

dilated_orange_mask: Menggunakan cv2.dilate() untuk melakukan dilasi pada orange_mask dengan menggunakan kernel berukuran (5, 5) yang terdiri dari nilai 1. Operasi dilasi dilakukan sebanyak 1 iterasi. Dengan melakukan dilasi, wilayah piksel putih pada orange_mask akan diperluas dan menghasilkan dilated_orange_mask.

### Bitwise_and Antara Citra & Mask
fungsi cv2.bitwise_and() untuk menerapkan operasi bitwise AND antara citra asli (image) dan mask yang telah di-dilasi. Hasilnya adalah citra-citra yang hanya menampilkan bagian yang sesuai dengan mask yang di-dilasi.

apel_red: Menggunakan cv2.bitwise_and() untuk mengaplikasikan operasi bitwise AND antara image dan dilated_red_mask. Hasilnya adalah citra apel_red yang hanya menampilkan bagian dari image yang berada di dalam wilayah yang sesuai dengan dilated_red_mask. Dengan demikian, hanya bagian apel yang memiliki warna merah yang ditampilkan dalam citra apel_red.

mangga_green: Menggunakan cv2.bitwise_and() untuk mengaplikasikan operasi bitwise AND antara image dan dilated_green_mask. Hasilnya adalah citra mangga_green yang hanya menampilkan bagian dari image yang berada di dalam wilayah yang sesuai dengan dilated_green_mask. Dengan demikian, hanya bagian mangga yang memiliki warna hijau yang ditampilkan dalam citra mangga_green.

jeruk_orange: Menggunakan cv2.bitwise_and() untuk mengaplikasikan operasi bitwise AND antara image dan dilated_orange_mask. Hasilnya adalah citra jeruk_orange yang hanya menampilkan bagian dari image yang berada di dalam wilayah yang sesuai dengan dilated_orange_mask. Dengan demikian, hanya bagian jeruk yang memiliki warna oranye yang ditampilkan dalam citra jeruk_orange.

### Menampilkan Gambar Asli & Output Identifikasi Antar Warna
image: Menggunakan cv2.cvtColor() dengan parameter cv2.COLOR_BGR2RGB untuk mengonversi citra image dari format BGR menjadi RGB. Ini dilakukan agar citra dapat ditampilkan dengan warna yang benar saat menggunakan matplotlib.

apel_red, mangga_green, jeruk_orange: Menggunakan cv2.cvtColor() dengan parameter cv2.COLOR_RGB2BGR untuk mengonversi citra apel_red, mangga_green, dan jeruk_orange dari format RGB menjadi BGR. Ini dilakukan agar citra-citra tersebut sesuai dengan format warna yang diperlukan oleh OpenCV.

plt.subplots() untuk membuat subplot dengan 1 baris dan 4 kolom, dan menentukan ukuran figur menggunakan figsize=(16,8). 

Selanjutnya, Akan ditampilkan masing-masing citra pada subplot yang sesuai dengan judul yang ditentukan.

ax[0]: Menampilkan citra asli (image) dengan judul "Gambar Asli".
ax[1]: Menampilkan citra hasil segmentasi apel (apel_red) dengan judul "Apel".
ax[2]: Menampilkan citra hasil segmentasi mangga (mangga_green) dengan judul "Mangga".
ax[3]: Menampilkan citra hasil segmentasi jeruk (jeruk_orange) dengan judul "Jeruk".

# Sumber Jurnal Terkait

https://conference.upnvj.ac.id/index.php/senamika/article/download/2011/1588

https://jurnal.ugp.ac.id/index.php/JURTIE/article/view/430

https://ejournal.unp.ac.id/index.php/voteknika/article/view/114251
