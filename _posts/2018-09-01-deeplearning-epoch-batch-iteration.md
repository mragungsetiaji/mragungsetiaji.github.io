---
layout: post
title:  "Deep Learning : Epoch, Batch dan Iteration"
date:   2018-09-01 18:34:10 +0700
categories: [python, machine learning]
---


Kita pasti pernah mengalami saat-saat ketika melihat codingan dan menggaruk kepala bertanya-tanya *“Ngapain gue mengetik ketiga istilah ini sebagai parameter dan apa bedanya”*.

Untuk menemukan perbedaan istilah tersebut, coba kita flashback ke istilah machine learning seperti **Gradient Descent** agar lebih mudah untuk dipahami.

### Berikut adalah summary singkat dari Gradient Descent

## Gradient Descent
Algoritma optimasi yang iterative (berulang-ulang) yang digunakan pada machine learning untuk menemukan result terbaik dari modelnya (kurva minimal). **Gradient** artinya rate dari inclination atau declination pada sebuah lereng kurva. **Descent** artinya level dari descending (penurunan).

Algoritmanya sendiri dikatakan iterative yang berarti ketika kita ingin mendapatkan hasilnya kita perlu mengulangi berkali-kali hingga mendapatkan hasil yang optimal. Iterative dari gradient descent membantu grafik yang under-fitted untuk membuat grafik fit dengan data secara optimal.

![](https://cdn-images-1.medium.com/max/800/1*pwPIG-GWHyaPVMVGG5OhAQ.gif)

Parameter pada Gradient Descent salah satunya adalah **learning rate**. Seperti yang kita lihat diatas (kiri). Awalnya step yang dibentuk besar yang berarti learning ratenya lebih tinggi. Semakin menuruni kurva step semakin kecil yang artinya learning rate juga semakin rendah. Dan juga Cost Function menurun yang artinya costnya juga menurun. Kadang beberapa orang dalam blognya mengatakan Lost Function nya menurun atau Lossnya menurun, keduanya Cost dan Loss sebenarnya merepresentasikan hal yang sama (hal yang bagus juga kalau loss functionya menurun)

----

Kita perlu paham dan menggunakan term seperti **epoch**, **batch size**, **iterasi** hanya ketika datanya terlalu gede dan kita tidak bisa memasukan semuanya kedalam komputer sekaligus dalam satu waktu (berbeda dengan machine learning general dimana kita fit(X_train, y_train) kita memasukan semua datanya dalam satu proses). Jadi karena hal itulah kita perlu membagi data ke dalam ukuran yang lebih kecil dengan memberikan hal itu ke komputer satu demi satu dan update weight pada si neural network pada akhir setiap step ketika data itu mengalir melewati bukit dan lembah.

## Epochs
> Satu kali Epoch adalah ketika SEMUA dataset melewati satu kali proses forward dan backward melewati semua node neural network 1 KALI.

Karena setiap satu epoch terlalu besar untuk memasukan semua data kedalam komputer sekaligus, maka kita membaginya jadi beberapa batch yang lebih kecil.

### Kenapa kita menggunakan lebih dari satu Epoch?
Memasukkan semua dataset ke dalam neural network ternyata ga cukup, kita perlu memasukkan semua dataset itu beberapa kali kedalam neural network yang sama. Perlu diperhatikan bahwa kita menggunakan dataset yang terbatas dan mengoptimalkan learning graph kita menggunakan Gradient Descent yang processnya iterative. Jadi mengupdate weight hanya dengan single process atau satu kali epoch itu ga cukup.

> Satu kali epoch akan membawa kita ke model yang underfitting

Semakin banyaknya epoch yang bertambah, semakin sering weight yang ada pada si neural diubah (diupdate) dan kurva akan berubah dari underfitting ke kurva optimal lanjut ke kurva overfitting.

### Jadi berapa banyak epoch yang seharusnya?
Sayangnya ga ada jawaban yang benar untuk ini, jawabannya adalah beda, beda epochnya untuk dataset yang beda tapi kita bisa mengasumsikan banyaknya epoch akan linear dengan banyaknya variance dalam dataset. Misalkan kita ingin menggunakan computer vision pada image kucing, seberapa banyak kucing yang belang2, hitam, kuning atau mata biru? padahal semua itu hanya menunjukkan satu class yaitu si kucing.

## Batch Size
Total jumlah training dataset yang digunakan pada satu batch. Perhatikan bahwa Batch size dan banyaknya batch adalah dua hal yang berbeda.

### Tapi apa itu Batch?
Seperti yang kita pelajari bahwa, kita tidak bisa memasukan semua dataset sekaligus ke dalam si NN. Jadi kita perlu membagi si dataset ke banyaknya batch.

Jadi kek ketika kita membagi artikel yang besar ke beberapa bagian. seperti intro, inti, summary biar lebih mudah untuk dibaca dan dipahami.

## Iterasi
> Iterasi adalah banyaknya batch yang dibutuhkan untuk menyelesaikan satu kali epoch. 

Banyaknya batch sama dengan banyaknya iterasi untuk satu kali epoch

## Summary

Misalnya kita punya 2000 data training.

Kita membagi 2000 dataset tersebut ke dalam 500 batch yang mana akan melakukan 4 kali iterasi untuk menyelesaikan 1 kali epoch, dengan kata lain 500nya sebagai Batch Size.
