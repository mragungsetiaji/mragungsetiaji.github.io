---
layout: post
title: "Deep Learning - Activation Function"
comment: true
categories:
  - Deep Learning
tags:
  - Deep Learning
---

## Into tentang Sigmoid, Tanh, Softmax, ReLU, dan Leaky ReLU

![](https://cdn-images-1.medium.com/max/2000/1*GIPiAdQyOa8wUOkHaL-MJg.gif)

## Activation Function?

Hanya salah satu node yang ditambahkan ke output si NN, atau juga dikenal sebagai Transfer Function. Atau bisa di attach diantara layer si NN.

### Kenapa harus menggunakan Activation Function pada NN?

Sebenarnya digunakan untuk menentukan ouput dari si NN seperti yes or no. Fungsi yang memetakan input menjadi 0 sampai 1 atau -1 sampai 1 (tergantung fungsinya).

Pada dasarnya Activation Function dibedakan menjadi 2 tipe:

1. Linear Activation Function
2. Non-linear Activation Functions

## Linear atau Identity Activation Function
Terlihat bahwa functionnya berbentuk line atau linear. Sehingga, output dari si function tidak terbentuk menjadi sebuah range.

![](https://cdn-images-1.medium.com/max/800/1*tldIgyDQWqm-sMwP7m3Bww.png)

**Persamaan** : f(x) = x

**Range** : (-tak hingga ke tak hingga)

Ga banyaknya membantu untuk parameter yang complex.

## Non-linear Activation Function
Function yang paling sering digunakan. Nonlinearity akan terlihat seperti ini

![](https://cdn-images-1.medium.com/max/800/1*cxNqE_CMez7vUIkcLUH8PA.png)

Dengan non linear lebih mudah bagi si model untuk beradaptasi dengan data yang vary. Hal yang perlu untuk dipahami pada nonlinear function adalah:

- **Derivative** atau **Differential**: Berubah pada y-axis, dan berubah juga pada x-axis nya.I Seperti sebuah slope.
- **Monotonic function**: Sebuah function yang secara keseluruhan ga menaik atau ga menurun.

Nonlinear Activation Functions secara umum dibagi berdasarkan basis dari rangenya atau curvanya.

1. Sigmoid atau Logistic Activation Function
Sigmoid Function terlihat seperti S-shape.

![](https://cdn-images-1.medium.com/max/800/1*Xu7B5y9gp0iL5ooBj7LtWw.png)

Alasan utama kenapa menggunakan function sigmoid adalah karena nilainya ada di range (0 sampai 1). Sehingga, bisa digunakan oleh model untuk memprediksi probability sebagai output. Karena probability juga nilainya ada di range (0 sampai 1).

Sigmoid termasuk function yang **differentiable**. Yang artinya, kita bisa mendapatkan slope dari kurva simoid dari dua titik sembarang.

Sigmoid juga termasuk monotonic tapi turunannya enggak.

Sigmoid logistik dapat mengakibatkan si NN stuck saat waktu training.

Sigmoid lebih generalisasi logistik sehingga bisa digunakan untuk multiclass classification.

2. Tanh atau hyperbolic tangent Activation Function