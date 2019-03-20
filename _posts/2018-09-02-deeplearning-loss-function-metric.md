---
layout: post
title:  "Deep Learning : Loss Function, Metric"
date:   2018-09-02 18:34:10 +0700
categories: [python, machine learning]
---

Mas, sebenarnya saya masih bingung nih kenapa metricnya lebih dari satu. Lalu kenapa ada loss dan metric dimana keduanya terlihat sama (MSE), dan apa bedanya dari dua hal itu?

```python
model.compile(loss='mean_squared_error',
              optimizer='sgd',
              metrics=['mae', 'acc'])
```

Jadi untuk memahami apa yang dimaksud dengan metric, ada baiknya untuk mulai dari pemahaman tentang apa itu `Loss Function`. Neural Network sebagian besar dilatih menggunakan metode gradien dengan proses iteratif untuk mengurangi Loss Function. Function tersebut memiliki dua properti penting, semakin sedikit nilainya maka semakin baik si model sesuai dengan data dan itu harus terdiferensiasi. Dan metric adalah fungsi yang memberikan nilai prediksi dan dibandingkan dengan data sesungguhnya. Mungkin kita melihat Loss Function adalah metric tetapi hal yang sebaliknya tidak selalu berlaku. Untuk memahami perbedaan ini, mari kita lihat contoh penggunaan metric yang paling umum:

1. Ukur kinerja model menggunakan fungsi yang tidak terdiferensiasi: misalkan, akurasi tidak terdiferensiasi (bahkan tidak continuous) sehingga kita tidak bisa secara langsung mengoptimalkan si NN dengan si akurasi. Namun kita bisa menggunakannya untuk memilih model dengan akurasi terbaik.

2. Dapatkan nilai dari Loss Function yang berbeda ketika final lossnya adalah kombinasi dari beberapa Loss Function: Mari kita asumsikan bahwa Loss Function memiliki istilah regularisasi yang mengukur bagaimana weight model berbeda dari titik 0 dan istilah yang mengukur kesesuaian model. Dalam hal ini, Kita bisa menggunakan metric untuk mengukur secara terpisah tentang bagaimana fitness dari model berubah di semua epoch.

3. Track ukuran yang tidak kita inginkan untuk langsung mengoptimalkan model: Anggaplah kita akan memecahkan masalah regresi multidimensi di mana kita lebih mengkhawatirkan tentang MSE tetapi pada saat yang sama kita tertarik pada bagaimana cosinus-distance dari model berubah sepanjang t (waktu). Jadi itu perlu dijadikan sebagai metric terbaik dalam pengukuran.

Saya harap penjelasan yang disajikan di atas membuat jelas apa itu metric dan mengapa kita bisa menggunakan banyak metric dalam satu model. Sekarang bagaimana secara teknis hal itu dilakukan menggunakan keras. Ada dua cara untuk menghitungnya saat training:

1. Menggunakan metric yang ditentukan saat compile. Sama seperti code yang dipertanyakan diatas. Dalam hal ini, keras mendefinisikan tensor terpisah untuk setiap metric yang kita definisikan untuk dihitung saat training. Ini biasanya membuat komputasi lebih cepat tapi hal tersebut datang dengan cost untuk compile dan metric harus didefinisikan didalam fungsi `keras.backend`.

2. Menggunakan `keras.callback`. apa bagusnya kita bisa menggunakan Callback untuk menghitung metric. Karena setiap callback memiliki atribut model secara default, kita dapat menghitung berbagai metric menggunakan `model.predict` atau parameter model saat training. Selain itu memungkinkan untuk menghitungnya tidak hanya dari segi waktu tetapi juga training yang lebih efisien. Sekali lagi hal ini datang dengan cost yaitu komputasi yang lebih lambat dan logika yang lebih rumit, karena kita mendefinisikan metric sendiri.

## Perbedaan Metric dengan Loss
Sekarang kita ambil sederhananya saja menggunakan binary classification, berikut adalah persamaan lossnya:

![](https://i.stack.imgur.com/ganiv.png)

- `y[i]` adalah `true label` (0 or 1)
- `p[i]` adalah prediction (real numbers diantara [0,1]), dan biasanya direpresentasikan sebagai probability
- `output[i]` (ga ada dipersamaan diatas) adalah hasil pembulatan dari p[i], untuk mengkonversi probability kedalam bentuk 0 atau 1; inilah nilai yang dipakai untuk menghitung akurasi, berdasarkan sebuah nilai threshold tertentu (biasanya 0.5 binary classification), jadi jika `p[i] > 0.5`, maka `output[i] = 1`, atau jika `p[i] <= 0.5`, `output[i] = 0`.

Sekarang kita asumsikan bahwa kita punya true label `y[k] = 1`, dan itu terjadi pada sesi awal process training yang mana hasil prediksinya sangat jelek, `p[k] = 0.1` lalu kita masukan hal itu kedalam loss function diatas:

- Kontribusi dari sample ini kedalam loss function, yaitu `loss[k] = -log(0.1) = 2.3`
- Karena `p[k] < 0.5`, kita akan punya `output[k] = 0`, disinilah kontribusi si sample ke accuracy dimana hasilnya nol (*wrong classification!*)

Oke sekarang misalkan kita lanjut ke training selanjutnya, kita dapet result lebih baik nih `p[k] = 0.22`; jadi sekarang kita punya:

- `loss[k] = -log(0.22) = 1.51`
- Tapi karena `p[k] < 0.5`, kita masih dapat *wrong classification* (`output[k] = 0`) dan kontribusi ke accuracynya masih 0

Semoga kita bisa mulai dapet idenya, sekarang coba lanjut lagi kita dapet `p[k] = 0.49`; maka:

- `loss[k] = -log(0.49) = 0.71`
- tapi masih juga `output[k] = 0`, yang mana *wrong classification* lagi dengan konribusi ke accuracy masih 0.

Seperti yang kita lihat bahwa si classifier menjadi lebih baik performanya dari setiap sample yang berjalan. Untuk lossnya sendiri dari 2.3 ke 1.5 dan ke 0.71, tapi improvement ini ga terlihat di accuracy, yang hanya peduli dengan classification yang benar: dari sisi accuracy sendiri, hal ini gak penting untuk mendapatkan estimasi dari `p[k]`, selama estimasi tersebut masih dibawah threshold yaitu 0.5.

Dan ketika `p[k]` melewati batas threshold di 0.5, Loss Function tetap melanjutkan pengurangannya secara perlahan sejauh ini, sekarang kita bisa melihat kontribusi model ke accuracy. Dengan kata lain ketika p[k] melewati batas threshold 0.5, model akan memberikan classification yang benar (dan sekarang accuracy akan bernilai positive). Improvement yang terus berjalan akan memberikan accuracy mendekati 1 disisi lain si Loss akan terus berlanjut memberikan penurunan tapi tidak memberikan impact lebih jauh ke accuracy.

Pendapat yang sama ketika true label `y[m] = 0` dan estimasi untuk `p[m]` mulai dari diatas threshold 0.5, dan bahkan jika `[pm]` mulai dari dibawah threshold 0.5 tapi sudah memberikan kontribusi positif ke accuracy. Proses convergen nya akan menuju 0.0 yang akan mengurangi loss function tanpa menambah accuracy lagi.

Dengan menggabungkan dua hal tersebut, semoga kita sekarang paham kalau mengurangi loss secara "bertahap" akan meningkatkan accuracy.

Secara general dari prespective matematika optimasi, tidak ada yang namanya "accuracy" yang ada adalah "loss", accuracy hanya muncul ketika kita melihatnya dari prespective bisnis (dan logika bisnis yang berbeda akan mengubah threshold default dari 0.5 ke angka tertentu).

## Summary

> Loss dan accuracy adalah hal yang berbeda; secara kasar, akurasi datang dari perspektif bisnis, sedangkan Loss adalah fungsi obyektif bahwa algoritma pembelajaran (pengoptimal) mencoba untuk meminimalkan dari perspektif matematika. Kita bisa menganggap loss sebagai "terjemahan" dari tujuan bisnis (akurasi) ke domain matematika, terjemahan yang diperlukan dalam masalah klasifikasi (di regresi, biasanya Loss dan tujuan bisnis adalah sama, atau setidaknya bisa sama pada prinsipnya, misalnya RMSE)

Jadi Loss Function itu diperlukan untuk proses training modelnya. Sementara Metric adalah ketika model dipakai untuk proses prediksi (menguji si model).