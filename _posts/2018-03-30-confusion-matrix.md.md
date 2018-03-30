---
layout: post
title: "Machine Learning : Metrics - Confusion Matrix!"
image: https://preview.ibb.co/j1frjn/Untitled_1.jpg
categories:
  - Machine Learning
tags:
  - Machine Learning
  - Metric
  - Accuracy
  - Recall
  - Precision
  - ROC
  - Confusion Matrix
  - F1 Score
---

# Terminology tentang "Confusion Matrix"

> Confusion matrix adalah sebuah tabel yang sering digunakan untuk **mendeskripsikan performa dari sebuah model classification** pada sebuah set dari data test dimana true values diketahui. CM sendiri cukup mudah untuk dipahami namun untuk terminologynya agak cukup "confuse".

Kita mulai dengan contoh "**confusion matrix untuk binary classifier**" (namanya binary berarti 2 class, tapi bisa nantinya diperluas lagi lebih dari 2 class):

<a href="http://imgbb.com/"><img src="http://image.ibb.co/gdjwn7/confusion_matrix_simple2.png" alt="confusion_matrix_simple2" border="0"></a>

 Apa yang bisa kita pelajari dari matrix ini?

 - Ada dua kelas yang diprediksi: "yes" dan "no". Jika kita memprediksi adanya sebuah penyakit, "yes" mengartikan bahwa kita mempunyai penyakit tersebut dan "no" artinya kita tidak mempunyai penyakit tersebut.
 - Classifier model membuat 165 prediksi (artinya, ada 165 pasien yang diprediksi apakah mereka mempunyai penyakit yang kita maksud)
 - Dari 165 kasus tersebut, model classifier memprediksi "ya" sebanyak 110 kali dan "no" sebanyak 55 kali.
 - Pada kenyataannya, 105 pasien pada sampel mempunyai penyakit dan 60nya tidak.

 Istilah-istilah pada CM:

 - **True Positives (TP)**: Pada kasus ini kita memprediksi "yes" (mereka mempunyai penyakit) dan mereka memang benar memiliki penyakit tersebut.
 - **True Negatives (TN)**: Terprediksi "no" dan memang tidak ada penyakit.
 - **False Positives (FP)**: Kita prediksi "yes", tapi sebenarnya mereka tidak memiliki penyakit.
 - **False Negatives (FN)**: Kita prediksi "no", tapi sebenarnya mereka memiliki penyakit.

Kita coba tambahkan total dari masing-masing baris dan kolom pada CM diatas:

<a href="http://imgbb.com/"><img src="http://image.ibb.co/kdh5fS/confusion_matrix2.png" alt="confusion_matrix2" border="0"></a>

Berikut adalah daftar dari rate yang sering dihitung pada CM untuk sebuah binary classifier:

- **Accuracy:** Overall, seberapa sering classifier bernilai benar?
    - (TP + TN)/ Total = (100 + 50)/165 = 0.91
- **Misclassification Rate:** Overall, seberapa sering salah?
    - (FP + FN)/ Total = (10 + 5)/165 = 0.09
    - equivalent dengan (Accuracy - 1)
    - disebut juga sebagai "Error rate"
- **True Positive Rate (TPR):** Ketika actual bernilai "yes", seberapa sering diprediksi "yes"?
    - TP / actual yes = 100/105 = 0.95
    - disebut juga sebagai "Sensitivity" atau "Recall"
- **False Positive Rate (FPR):** Ketika actual bernilai "no", seberapa sering diprediksi "yes"?
    - FP/ actual no = 10/60 = 0.17
- **Specificity:** Ketika actual bernilai "no", seberapa sering diprediksi "no"?
    - TN /actual no = 50/60 = 0.83
    - equivalent dengan (FPR - 1)
- **Precision:** Ketika diprediksi "yes" seberapa sendiri benar?
    - TP/ predicted yes = 100/110 = 0.91
- **Prevalence:** Seberapa sering "yes" muncul pada sample?
    - actual yes/total = 105/165 = 0.64

Daan, berikut summary ketika CM dihubungkan dengan Bayesian statistic:

> Untuk hubungan dengan Bayesian Statistics, **sensitivity** dan **specificity** adalah conditional probabilities sebagai prior, dan positive/negative values yang diprediksi sebagai posterior probabilities.
