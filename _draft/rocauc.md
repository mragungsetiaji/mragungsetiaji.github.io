Dalam Machine Learning, pengukuran bagus tidaknya suatu model merupakan hal yang penting. Dan jika diklasifikasi, kita bisa mengandalkan Kurva AUC-ROC. Ketika kita perlu memvisualisasikan kinerja siatu model pada multi-class klasifikasi, kita menggunakan kurva AUC (**Area Under The Curve**) dan ROC (**Receiver Operating Characteristics**). Salah satu metrik evaluasi terpenting untuk memeriksa kinerja model klasifikasi apa pun itu. Atau dikenal juga AUCROC (**Area Under the Receiver Operating Characteristics**

This blog aims to answer following questions:

1. What is AUC - ROC Curve?
2. Defining terms used in AUC and ROC Curve.
3. How to speculate the performance of the model?
4. Relation between Sensitivity, Specificity, FPR and Threshold.
5. How to use AUC - ROC curve for multiclass model?)

## Apa itu kurva AUC-ROC?
AUC - ROC curve adalah pengukuran kinerja untuk model klasifikasi pada berbagai threshold tertentu. ROC adalah kurva probabilitas dan AUC mewakili derajat atau ukuran keterpisahan. Berapa banyak model mampu membedakan antar kelas. Semakin tinggi AUC, semakin baik modelnya memprediksi 0 sebagai 0 dan 1 sebagai 1. Dengan analogi, Semakin tinggi AUC, semakin baik modelnya membedakan antara pasien dengan penyakit dan tidak ada penyakit.

