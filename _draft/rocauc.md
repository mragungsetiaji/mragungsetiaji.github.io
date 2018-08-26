Dalam Machine Learning, pengukuran bagus tidaknya suatu model merupakan hal yang penting. Dan jika diklasifikasi, kita bisa mengandalkan Kurva AUC-ROC. Ketika kita perlu memvisualisasikan kinerja siatu model pada multi-class klasifikasi, kita menggunakan kurva AUC (**Area Under The Curve**) dan ROC (**Receiver Operating Characteristics**). Salah satu metrik evaluasi terpenting untuk memeriksa kinerja model klasifikasi apa pun itu. Atau dikenal juga AUCROC (**Area Under the Receiver Operating Characteristics**

This blog aims to answer following questions:

1. What is AUC - ROC Curve?
2. Defining terms used in AUC and ROC Curve.
3. How to speculate the performance of the model?
4. Relation between Sensitivity, Specificity, FPR and Threshold.
5. How to use AUC - ROC curve for multiclass model?)

## Apa itu kurva AUC-ROC?
AUC - ROC curve adalah pengukuran kinerja untuk model klasifikasi pada berbagai threshold tertentu. ROC adalah kurva probabilitas dan AUC mewakili derajat atau ukuran keterpisahan. Berapa banyak model mampu membedakan antar kelas. Semakin tinggi AUC, semakin baik modelnya memprediksi 0 sebagai 0 dan 1 sebagai 1. Dengan analogi, Semakin tinggi AUC, semakin baik modelnya membedakan antara pasien dengan penyakit dan tidak ada penyakit.

ROC Curve di plot dengan TPR (True positive rate) sebagai y-axis dan FPR (False positive rate) sebagai x-axis.

![](https://cdn-images-1.medium.com/max/800/1*pk05QGzoWhCgRiiFbz-oKQ.png)

## Definisi terms yang digunakan dalam AUC dan ROC Curve.

### TPR (True Positive Rate) / Recall /Sensitivity

![](https://cdn-images-1.medium.com/max/800/1*HgxNKuUwXk9JHYBCt_KZNw.png)

### Specificity

![](https://cdn-images-1.medium.com/max/800/1*f7NmMcQtfes1ng7jtjNtHQ.png)

### False Positive Rate

![](https://cdn-images-1.medium.com/max/800/1*3GhDfiuhvINF5-9eL8g6Pw.png)

## Bagaimana cara menilai kinerja sebuah model?
Model yang sangat baik memiliki AUC dekat dengan 1 yang berarti mampu mengklasifikasikan secara sempurna. Model yang buruk memiliki AUC dekat dengan 0 yaitu memprediksi 0 sebagai 1 dan 1 sebagai 0. Dan ketika AUC bernilai 0.5, itu berarti model tidak memiliki kapasitas untuk memisahan kelas sama sekali.

Mari tafsirkan pernyataan di atas.

Seperti yang kita ketahui, ROC adalah kurva probabilitas. Jadi mari kita plot distribusi probabilitas tersebut:

Catatan: Kurva distribusi merah adalah kelas positif (pasien dengan penyakit) dan kurva distribusi hijau adalah kelas negatif (pasien tanpa penyakit).

![](https://cdn-images-1.medium.com/max/800/1*Uu-t4pOotRQFoyrfqEvIEg.png)
![](https://cdn-images-1.medium.com/max/400/1*HmVIhSKznoW8tFsCLeQjRw.png)

Situasi yang ideal. Ketika dua kurva tidak tumpang tindih sama sekali berarti model memiliki ukuran keterpisahan yang ideal. Sangat mampu membedakan antara kelas positif dan kelas negatif.

![](https://cdn-images-1.medium.com/max/800/1*yF8hvKR9eNfqqej2JnVKzg.png)
![](https://cdn-images-1.medium.com/max/400/1*-tPXUvvNIZDbqXP0qqYNuQ.png)

Ketika dua distribusi berisisan (overlap), kita mendapatkan kesalahan tipe 1 dan tipe 2. Tergantung pada thresholdnya, kita dapat meminimalkan atau memaksimalkannya. Ketika AUC adalah 0.7, itu berarti ada kemungkinan 70% bahwa model akan dapat membedakan antara kelas positif dan kelas negatif.

![](https://cdn-images-1.medium.com/max/800/1*iLW_BrJZRI0UZSflfMrmZQ.png)

Situasi terburuk. Ketika AUC sekitar 0.5, model tidak memiliki kapasitas diskriminasi untuk membedakan antara kelas positif dan kelas negatif.

![](https://cdn-images-1.medium.com/max/800/1*aUZ7H-Lw74KSucoLlj1pgw.png)
![](https://cdn-images-1.medium.com/max/400/1*k_MPO2Q9bLNH9k4Wlk6v_g.png)

Ketika AUC kira-kira 0, model sebenarnya adalah reciprocating the classes. Artinya, model memprediksi kelas negatif sebagai kelas positif dan sebaliknya.

## Bagaimana cara menggunakan kurva AUC ROC untuk model multi-class?
Dalam model multi-class, kita bisa memplot jumlah N dari AUC-ROC Curves untuk kelas N dengan menggunakan metodologi One vs ALL. Contoh, Jika kita memiliki tiga kelas bernama X, Y dan Z, kita akan memiliki satu ROC untuk X yang diklasifikasikan terhadap Y dan Z, ROC lain untuk Y yang diklasifikasikan terhadap X dan Z, dan yang ketiga dari Z yang diklasifikasikan terhadap Y dan X .