---
layout: post
title: "Machine Learning - AUC-ROC! (Version 1.2)"
comment: true
categories:
  - Machine Learning
tags:
  - Machine Learning
  - ROC
  - AUC
  - Metric
---

> Updated v1.2 : Recontruct (7 September 2018)

Katakan kita ingin membuat suatu model untuk test suatu penyakit tertentu. Ada beberapa data tentang pengajuan paper untuk dipublikasikan, tujuan si model untuk memprediksi status paper dari beberapa rangkaian variabel tentang si paper dan penulisnya. Fiturnya mungkin bisa jadi panjang kertas, jumlah penulis, jumlah makalah yang telah diserahkan penulis sebelumnya ke jurnal, dan sebagainya. True Positive Rate adalah suatu paper diidentifikasi secara tepat sebagai paper yang diterima untuk publikasi, dan False Positive Rate adalah paper yang ditolak, tetapi diidentifikasi sebagai paper yang diterima (berdasarkan model).

Ada beberapa threshold untuk menunjukan bahwa sebuah paper akan diterima. Katakanlah lebih dari atau sama dengan 0.5, kita menganggap bahwa nilai tersebut cukup untuk menunjukkan si paper akan diterima atau tidak. Saat kita memvariasikan treshold ini, TPR dan FPR akan berubah. Ini adalah kurva ROC.

Kurva ROC adalah cara yang umum digunakan untuk memvisualisasikan kinerja **biner classifier**, yang berarti classifier dengan dua kelas output.

![](https://www.dataschool.io/content/images/2014/11/roc01.PNG)

Pertama mari kita lihat pada diagram, dan abaikan semuanya kecuali distribusi warna biru dan merah. Kita mengasumsikan bahwa setiap piksel warna biru dan merah mewakili paper yang kita inginkan untuk memprediksi status penerimaan. Bisa dikatakan ini adalah himpunan validasi (atau "hold-out"), jadi kita tahu status penerimaan sebenarnya dari setiap paper. 250 piksel warna merah adalah paper yang benar-benar diterima, dan 250 piksel warna biru adalah paper yang tidak diterima.

![](https://www.dataschool.io/content/images/2014/11/roc02.PNG)

Karena ini adalah himpunan validasi, kita ingin menilai seberapa baik model kita dengan membandingkan prediksi model dengan status penerimaan yang sebenarnya dari 500 paper tersebut. Kita akan berasumsi bahwa kita menggunakan metode klasifikasi seperti regresi logistik yang tidak hanya dapat membuat prediksi untuk setiap paper, tetapi juga dapat menghasilkan prediksi probability penerimaan untuk setiap paper. Distribusi warna biru dan merah ini adalah salah satu cara untuk memvisualisasikan bagaimana probabilitas yang diprediksi itu dibandingkan dengan status sebenarnya.

![](https://www.dataschool.io/content/images/2014/11/roc03.PNG)

Mari kita periksa plot ini lebih detail. Sumbu x mewakili probabilitas prediksi, dan sumbu y mewakili hitungan pengamatan, seperti histogram. Mari kita perkirakan bahwa tinggi pada 0,1 adalah 10 piksel. Plot ini memberitahu kita bahwa ada 10 paper yang kita prediksi dengan probabilitas penerimaan 0,1, dan status sebenarnya untuk semua 10 paper adalah negatif (artinya tidak diterima). Ada sekitar 50 paper yang kita prediksi probabilitas admittance 0,3, dan tidak satupun dari 50 yang diterima. Ada sekitar 20 paper yang kita prediksi kemungkinan 0,5, dan setengah dari yang diterima dan setengah lainnya tidak. Ada 50 paper yang kita perkirakan kemungkinan 0,7, dan semua itu diterima. Dan seterusnya.

![](https://www.dataschool.io/content/images/2014/11/roc04.PNG)

Berdasarkan plot ini, kita katakan bahwa classifier kita hasilnya cukup baik, karena ia berhasil memisahkan kelas. Untuk benar-benar membuat prediksi kelas, kita dapat menetapkan "threshold" di 0,5, dan mengklasifikasikan semua di atas 0,5 sebagai diterima dan  di bawah 0,5 tidak diterima, yang mana semua classifier secara default akan seperti itu. Dengan threshold itu, tingkat akurasi akan di atas 90%, yang mungkin sangat bagus.

![](https://www.dataschool.io/content/images/2014/11/roc05.PNG)

Sekarang kita berasumsi bahwa classifier ini tidak melakukan pekerjaanya dengan baik dengan memindahkan distribusi warna biru. Kita melihat bahwa ada lebih banyak overlap di sini, dan di mana pun kita atur threshold, akurasi dari classifier ini akan jauh lebih rendah dari sebelumnya.

![](https://www.dataschool.io/content/images/2014/11/roc06.PNG)

Sekarang tentang kurva ROC yang kita lihat di sini di kiri atas. Jadi, apa itu kurva ROC? Yaitu plot dari True Positive Rate (pada sumbu y) versus False Positif Rate (pada sumbu x) untuk setiap threshold klasifikasi yang diatur sebelumnya. As reminder, True Positive Rate menjawab pertanyaan, "Ketika data yang sesungguhnya adalah positif (yang berarti diterima), seberapa sering si classifier memprediksi positif?" False Positive Rate menjawab pertanyaan, "Ketika data yang sesungguhnya negatif (artinya tidak diterima), seberapa sering si classifier salah memprediksi positif?" Baik True Positive Rate dan False Positive Rate mulai dari 0 hingga 1.

![](https://www.dataschool.io/content/images/2014/11/roc07.PNG)

Untuk melihat bagaimana kurva ROC benar-benar dihasilkan, mari kita set contoh threshold untuk mengklasifikasi sebuah paper mana yang diterima.

Threshold bernilai 0.8 akan berarti mengklasifikasikan 50 paper sebagai diterima, dan 450 paper tidak diterima. True Positif Rate adalah piksel warna merah di sebelah kanan garis dibagi dengan semua piksel warna merah, atau 50 dibagi dengan 250, yaitu 0.2. False Positive Rate adalah piksel warna biru di sebelah kanan garis dibagi dengan semua piksel warna biru, atau 0 dibagi dengan 250, yaitu 0. Jadi, kita akan memplot titik 0 pada sumbu x, dan 0,2 pada sumbu y.

![](https://www.dataschool.io/content/images/2014/11/roc08.PNG)

Coba ubah threshold jadi 0,5. Sehingga akan mengklasifikasi 360 paper sebagai diterima, dan 140 paper tidak diterima. True Positif Rate akan bernilai 235 dibagi dengan 250, atau 0,94. False Positif Rate akan bernilai 125 dibagi dengan 250, atau 0,5. Jadi, kita akan memplot titik 0,5 pada sumbu x, dan 0,94 pada sumbu y.

![](https://www.dataschool.io/content/images/2014/11/roc09.PNG)

Kita telah mendapatkan dua point tersebut, tapi untuk menghasilkan seluruh kurva ROC, yang harus kita lakukan adalah memplot Laju True Positive versus Laju False Positive untuk semua threshold klasifikasi yang berkisar dari 0 hingga 1. **Manfaat besar dari penggunaan kurva ROC untuk mengevaluasi classifier bukan sekedar metrik sederhana seperti error rate classifier, karena kurva ROC memvisualisasikan semua threshold klasifikasi yang mungkin, sedangkan error rate classifier hanya mewakili tingkat kesalahan untuk satu threshold saja**. Perhatikan bahwa kita tidak bisa melihat threshold yang digunakan untuk menghasilkan kurva ROC dimanapun saja pada kurva itu sendiri.

Sekarang, mari kita coba pindahkan distribusi warna biru kembali ke tempat sebelumnya. Karena si classifier melakukan pekerjaannya dengan sangat baik dalam memisahkan warna biru dan warna merah, kita bisa menetapkan thresholdnya sebesar 0,6, memiliki True Positive Rate 0,8, dan masih memiliki Laju False Positive Rate sebesar 0.

![](https://www.dataschool.io/content/images/2014/11/roc10.PNG)

Oleh karena itu, classifier yang melakukan pekerjaan yang sangat baik dalam memisahkan kelas akan memiliki kurva ROC sepert pada sudut kiri atas plot. Sebaliknya, classifier yang melakukan pekerjaan yang sangat buruk yang memisahkan kelas akan memiliki kurva ROC yang dekat dengan garis diagonal hitam ini. Garis itu pada dasarnya merupakan calssifier yang tidak berbeda dengan random guessing.

![](https://www.dataschool.io/content/images/2014/11/roc11.PNG)

Tentu saja, Kita bisa menggunakan kurva ROC untuk mengukur kinerja si classifier, dan memberikan skor yang lebih tinggi untuk classifier ini dari classifier itu. Itulah tujuan AUC, yang merupakan singkatan dari Area Under the Curve. AUC secara harfiah hanyalah persentase luas di bawah kurva ROC. Classifier ini memiliki AUC sekitar 0.8, classifier terburuk memiliki AUC sekitar 0.5, dan classifier ini memiliki AUC yang mendekati 1.

![](https://www.dataschool.io/content/images/2014/11/roc12.PNG)

Ada dua hal catatan dari diagram tersebut. Pertama, diagram ini menunjukkan sebuah case dimana kelasnya balance, karena ukuran besarnya distribusi biru dan merah sama identik. Jika di dunia nyata hal seperti ini hampir tidak akan selalu terjadi. Contoh, hanya 10% dari paper yang disetujui, distribusi biru akan sembilan kali lebih besar dari distribusi berwarna merah. Tapi bagaimanapun juga hal itu ga akan mengubah bagaimana kurva ROC dibentuk.

Catatan kedua bahwa diagramnya membentuk normal distribusi yang sangat smooth. Ini hanya untuk contoh aja. Karena kenyataannya distribusi probabilitasnya ga akan se-smooth itu.

![](https://www.dataschool.io/content/images/2014/11/roc13.PNG)

Ada tambahan catatan lain. Pertama, kurva ROC dan AUC tidak sensitif terhadap apakah probabilitas prediksi si model dikalibrasi dengan tepat mewakili probabilitas keanggotaan setiap kelas. Dengan kata lain, kurva ROC dan AUC akan sama bahkan jika probabilitas yang diprediksi berkisar dari 0,9 hingga 1 bukannya 0 hingga 1, asalkan urutan observasi dengan probabilitas prediksi tetap sama. AUC hanya peduli tentang bagaimana si model mengklasifikasi untuk membedakan dua kelas, dan sensitive berdasarkan order rank. AUC merepresentasikan probability bahwa si model ranking observasi yang positif secara random lebih besar dari pada observasi yang negatif secara random, sehingga akan berguna ketika datasetnya sangat unbalance.

![](https://www.dataschool.io/content/images/2014/11/roc14.PNG)

Catatan yang kedua, kurva ROC bisa di extend ke lebih dari dua class atau disebut "**one versus all**". Jadi ketika kita punya 3 class, kita akan membuat 3 kurva ROC. Kurva yang pertama, kita memilih class pertama sebagai positive class, dan group kedua class yang lain sebagai negative class. Begitu juga dengan kurva kedua, class kedua sebagai positive class dst.

![](https://www.dataschool.io/content/images/2014/11/roc15.PNG)

Akhirnya, kita mungkin ada pertanyaan bagaimana kita harus menetapkan batas threshold si classifier, ketika kita akan menggunakannya untuk mempredict data diluar sample. Itu sebenarnya lebih merupakan keputusan bisnis, di mana kita harus memutuskan apakah prefer meminimalkan False Positive Rate atau memaksimalkan True Positive Rate. Dalam contoh kasus si paper, tidak jelas apa yang harus kita lakukan. Namun, katakanlah si model digunakan untuk memprediksi apakah transaksi kartu kredit tergolong fraud dan harus direview oleh pemegang kartu kredit. Keputusan bisnis mungkin menetapkan ambang batas sangat rendah. Itu akan menghasilkan banyak False Positive Rate, tetapi itu mungkin dianggap dapat diterima karena akan memaksimalkan True Positive Rate dan dengan demikian meminimalkan jumlah kasus di mana contoh nyata penipuan tidak ditandai untuk direview.

![](https://www.dataschool.io/content/images/2014/11/roc16.PNG)

Pada akhirnya, kita akan selalu harus memilih batas threshold klasifikasi, tetapi kurva ROC akan membantu kita untuk memahami secara visual dampak dari pilihan itu.

Link: [**Paper**](http://people.inf.elte.hu/kiss/13dwhdm/roc.pdf)
