---
layout: post
title: "Deep Learning - Activation Function"
comment: true
categories:
  - Deep Learning
tags:
  - Deep Learning
---

## Intro tentang Sigmoid, Tanh, Softmax, ReLU, dan Leaky ReLU

![](https://cdn-images-1.medium.com/max/2000/1*GIPiAdQyOa8wUOkHaL-MJg.gif)

## Activation Function?

Hanya salah satu node yang ditambahkan ke output si Neural Network, atau juga dikenal sebagai `Transfer Function`. Atau bisa di attach diantara layer si Neural Network.

### Kenapa harus menggunakan Activation Function pada NN?

Sebenarnya digunakan untuk menentukan ouput dari si NN seperti yes or no. Fungsi yang memetakan input menjadi 0 sampai 1 atau -1 sampai 1 (tergantung fungsinya).

Pada dasarnya Activation Function dibedakan menjadi 2 tipe:

1. `Linear Activation Function`
2. `Non-linear Activation Function`

## Linear atau Identity Activation Function
Terlihat bahwa functionnya berbentuk line atau linear. Sehingga, output dari si function tidak terbentuk menjadi sebuah range.

![](https://cdn-images-1.medium.com/max/800/1*tldIgyDQWqm-sMwP7m3Bww.png)

- **Persamaan** : f(x) = x
- **Range** : (-tak hingga ke tak hingga)

Ga banyak membantu untuk parameter yang complex.

## Non-linear Activation Function
Function yang paling sering digunakan. Nonlinearity akan terlihat seperti ini

![](https://cdn-images-1.medium.com/max/800/1*cxNqE_CMez7vUIkcLUH8PA.png)

Dengan non linear lebih mudah bagi si model untuk beradaptasi dengan data yang vary. Hal yang perlu untuk dipahami pada nonlinear function adalah:

- **Derivative** atau **Differential**: Berubah pada y-axis, dan berubah juga pada x-axis nya.I Seperti sebuah slope.
- **Monotonic function**: Sebuah function yang secara keseluruhan ga menaik atau ga menurun.

Nonlinear Activation Functions secara umum dibagi berdasarkan basis dari rangenya atau curvanya.

1. **Sigmoid atau Logistic Activation Function**

    Sigmoid Function terlihat seperti S-shape.

    ![](https://cdn-images-1.medium.com/max/800/1*Xu7B5y9gp0iL5ooBj7LtWw.png)

    Alasan utama kenapa menggunakan function sigmoid adalah karena nilainya ada di range (0 sampai 1). Sehingga, bisa digunakan oleh model untuk memprediksi probability sebagai output. Karena probability juga nilainya ada di range (0 sampai 1).

    - Sigmoid termasuk function yang terdifferensiasi. Yang artinya, kita bisa mendapatkan slope dari kurva simoid dari dua titik sembarang.
    - Sigmoid juga termasuk monotonic tapi turunannya enggak.
    - Sigmoid logistik dapat mengakibatkan si NN stuck saat waktu training.
    - Sigmoid lebih generalisasi logistik sehingga bisa digunakan untuk multiclass classification.

2. **Tanh atau hyperbolic tangent Activation Function**

    Tanh juga seperti logistic sigmoid tapi lebih bagus. Range dari tanh function berasal dari (-1 sampai 1). Tanh juga berbentuk sigmoidal (s).

    ![](https://cdn-images-1.medium.com/max/800/1*f9erByySVjTjohfFdNkJYQ.jpeg)

    The advantage is that the negative inputs will be mapped strongly negative and the zero inputs will be mapped near zero in the tanh graph.

    - Keuntungannya adalah input yang negative akan di mapping ke negative dan input nl akan dimapping ke dekat dengan nol pada tanh. 
    - Function-nya terdifferensiasi.
    - Function-nya monotonix walaupun derivativenya tidak monotonic. 
    - Tanh Function paling sering digunakan untuk classifikasi diantara dua class.

    Tanh dan logistic sigmoid keduanya dalah activation function yang digunakan pada feed-forward. 

3. **ReLU (Rectified Linear Unit) Activation Function**

    ReLU merupakan function yang paling digunakan sampai sekarang, ini digunakan di hampir semua convex atau deep learning lainnya.

    ![](https://cdn-images-1.medium.com/max/800/1*XxxiA0jJvPrHEJHD4z893g.png)

    f(z) bernilai nol ketika z kurang dari nol atau sama dengan nol, dan f(z) sama dengan z adalah ketika z lebih dari atau sama dengan nol.

    Range: [ 0 sampai takhingga)

    - Function dan derivativenya keduanya adalah monotonic.

    Tapi masalahnya adalah semua nilai negatif menjadi nol hal tersebut yang menurunkan kemampuan model untuk menyesuaikan atau melatih dari data dengan benar. Itu berarti setiap masukan negatif yang diberikan kepada fungsi aktivasi ReLU mengubah nilai menjadi nol dalam grafik, yang pada gilirannya mempengaruhi grafik yang dihasilkan dengan tidak memetakan nilai negatif secara tepat.

4. **Leaky ReLU**

    Nah si Leaky datang untuk menyelesaikan masalah di ReLU

    ![](https://cdn-images-1.medium.com/max/800/1*A_Bzn0CjUgOXtPCJKnKLqA.jpeg)

    Leaky membantu untuk menambah range dari ReLU. Biasanya nilai dari `a` adalah 0.01.

    - Ketika `a` tidak bernilai 0.01 maka kita menamakannya sebagai Randomized ReLU.
    - Range: (-takhingga sampai takhingga)

    Leaky dan Randomized ReLU keduanya adalah monotonic. Jadi derivative keduanya juga monotonic.

## Lalu kenapa kita menggunakan derivativenya?
Ketika mengupdate kurva, untuk mengetahui ke arah mana dan berapa banyak untuk mengubah atau memperbarui kurva tergantung pada slope. Pada prose forward kita akan menggunakan si function tersebut dan sebaliknya ketika proses backward, derivativenya yang dibutuhkan. 

## Cheatsheet Activation Function
![](https://cdn-images-1.medium.com/max/800/1*p_hyqAtyI8pbt2kEl6siOQ.png)


![](https://cdn-images-1.medium.com/max/800/1*n1HFBpwv21FCAzGjmWt1sg.png)