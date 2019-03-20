---
layout: post
title:  "Machine Learning : AOC & ROC"
date:   2018-08-27 18:34:10 +0700
categories: [python, machine learning]
---

> Updated v1.2 : Recontruct (7 September 2018)

## Abbreviations
- **AUC** = Area Under the Curve.
- **AUROC** = Area Under the Receiver Operating Characteristic curve.

AUC lebih sering digunakan untuk mengartikan AUROC, walaupun ini hal yang keliru karena AUC bisa berbentuk kurva sementara AUROC nggak.

## Interpretasi dari AUROC
AUROC punya beberapa interpretasi yang equivalent:

- The expectation that a uniformly drawn random positive is ranked before a uniformly drawn random negative.
- The expected proportion of positives ranked before a uniformly drawn random negative.
- The expected true positive rate if the ranking is split just before a uniformly drawn random negative.
- The expected proportion of negatives ranked after a uniformly drawn random positive.
- The expected false positive rate if the ranking is split just after a uniformly drawn random positive.

## Contoh Kasus
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

## Perhitungan AUROC

Assume we have a probabilistic, binary classifier such as logistic regression.

Before presenting the ROC curve (= Receiver Operating Characteristic curve), the concept of confusion matrix must be understood. When we make a binary prediction, there can be 4 types of outcomes:

- We predict 0 while we should have the class is actually 0: this is called a True Negative, i.e. we correctly predict that the class is negative (0). For example, an antivirus did not detect a harmless file as a virus .
- We predict 0 while we should have the class is actually 1: this is called a False Negative, i.e. we incorrectly predict that the class is negative (0). For example, an antivirus failed to detect a virus.
- We predict 1 while we should have the class is actually 0: this is called a False Positive, i.e. we incorrectly predict that the class is positive (1). For example, an antivirus considered a harmless file to be a virus.
- We predict 1 while we should have the class is actually 1: this is called a True Positive, i.e. we correctly predict that the class is positive (1). For example, an antivirus rightfully detected a virus.

To get the confusion matrix, we go over all the predictions made by the model, and count how many times each of those 4 types of outcomes occur:

![](https://i.stack.imgur.com/lQ12T.png)


Abbreviations
AUC = Area Under the Curve.
AUROC = Area Under the Receiver Operating Characteristic curve.
AUC is used most of the time to mean AUROC, which is a bad practice since as Marc Claesen pointed out AUC is ambiguous (could be any curve) while AUROC is not.

Interpreting the AUROC
The AUROC has several equivalent interpretations:

The expectation that a uniformly drawn random positive is ranked before a uniformly drawn random negative.
The expected proportion of positives ranked before a uniformly drawn random negative.
The expected true positive rate if the ranking is split just before a uniformly drawn random negative.
The expected proportion of negatives ranked after a uniformly drawn random positive.
The expected false positive rate if the ranking is split just after a uniformly drawn random positive.
Going further: How to derive the probabilistic interpretation of the AUROC?

Computing the AUROC
Assume we have a probabilistic, binary classifier such as logistic regression.

Before presenting the ROC curve (= Receiver Operating Characteristic curve), the concept of confusion matrix must be understood. When we make a binary prediction, there can be 4 types of outcomes:

We predict 0 while we should have the class is actually 0: this is called a True Negative, i.e. we correctly predict that the class is negative (0). For example, an antivirus did not detect a harmless file as a virus .
We predict 0 while we should have the class is actually 1: this is called a False Negative, i.e. we incorrectly predict that the class is negative (0). For example, an antivirus failed to detect a virus.
We predict 1 while we should have the class is actually 0: this is called a False Positive, i.e. we incorrectly predict that the class is positive (1). For example, an antivirus considered a harmless file to be a virus.
We predict 1 while we should have the class is actually 1: this is called a True Positive, i.e. we correctly predict that the class is positive (1). For example, an antivirus rightfully detected a virus.
To get the confusion matrix, we go over all the predictions made by the model, and count how many times each of those 4 types of outcomes occur:

enter image description here

In this example of a confusion matrix, among the 50 data points that are classified, 45 are correctly classified and the 5 are misclassified.

Since to compare two different models it is often more convenient to have a single metric rather than several ones, we compute two metrics from the confusion matrix, which we will later combine into one:

- True positive rate (TPR), aka. sensitivity, hit rate, and recall, which is defined as TPTP+FN. Intuitively this metric corresponds to the proportion of positive data points that are correctly considered as positive, with respect to all positive data points. In other words, the higher TPR, the fewer positive data points we will miss.
- False positive rate (FPR), aka. fall-out, which is defined as FPFP+TN. Intuitively this metric corresponds to the proportion of negative data points that are mistakenly considered as positive, with respect to all negative data points. In other words, the higher FPR, the more negative data points will be missclassified.

To combine the FPR and the TPR into one single metric, we first compute the two former metrics with many different threshold (for example 0.00;0.01,0.02,…,1.00) for the logistic regression, then plot them on a single graph, with the FPR values on the abscissa and the TPR values on the ordinate. The resulting curve is called ROC curve, and the metric we consider is the AUC of this curve, which we call AUROC.

The following figure shows the AUROC graphically:

![](https://i.stack.imgur.com/9NpXJ.png)

In this figure, the blue area corresponds to the Area Under the curve of the Receiver Operating Characteristic (AUROC). The dashed line in the diagonal we present the ROC curve of a random predictor: it has an AUROC of 0.5. The random predictor is commonly used as a baseline to see whether the model is useful.

the AUC of a classifier is equal to the probability that the classifier will rank a randomly chosen positive example higher than a randomly chosen negative example, i.e. 

> `P(score(x+)>score(x−))`

## Technical Example

Consider this example (auc=0.68):

![](https://i.stack.imgur.com/QY5BJ.png)

Let's try to simulate it: draw random positive and negative examples and then calculate the proportion of cases when positives have greater score than negatives

```R
cls = c('P', 'P', 'N', 'P', 'P', 'P', 'N', 'N', 'P', 'N', 'P',
        'N', 'P', 'N', 'N', 'N', 'P', 'N', 'P', 'N')
score = c(0.9, 0.8, 0.7, 0.6, 0.55, 0.51, 0.49, 0.43, 0.42, 0.39, 0.33, 0.31, 0.23, 0.22, 0.19, 0.15, 0.12, 0.11, 0.04, 0.01)

pos = score[cls == 'P']
neg = score[cls == 'N']

set.seed(14)
p = replicate(50000, sample(pos, size=1) > sample(neg, size=1))
mean(p)
```
And we get 0.67926. Quite close, isn't it?

By the way, in R I typically use ROCR package for drawing ROC curves and calculating AUC.

```R
library('ROCR')

pred = prediction(score, cls)
roc = performance(pred, "tpr", "fpr")

plot(roc, lwd=2, colorize=TRUE)
lines(x=c(0, 1), y=c(0, 1), col="black", lwd=1)

auc = performance(pred, "auc")
auc = unlist(auc@y.values)
auc
```

![](https://i.stack.imgur.com/Zw4Yw.png)

Link: [**Paper**](http://people.inf.elte.hu/kiss/13dwhdm/roc.pdf)
