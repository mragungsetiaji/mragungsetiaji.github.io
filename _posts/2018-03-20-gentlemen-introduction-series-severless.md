---
layout: post
title: "Gentlemen Introduction Series : Severless!"
categories:
  - Data Science
tags:
  - Severless
  - cloud computing
---

# Apa itu : Severless?

Ketika pertama kali mendengar kata **"Severless Computing"**, saya berpikir bahwa ada teknologi yang tidak menggunakan sebuah server? atau mungkin sejenis client based, yang tidak menggunakan server sama sekali. Tapi sepertinya dugaan itu salah. Server adalah komputer yang didesign untuk menanggani request dan mengirimkan data dalam suatu network. Contoh **"Web Servers"** digunakan untuk mengakses web pages dalam jaringan internet. Ketika sebuah web browser mengirimkan request ke web server, si server akan memproses request tersebut dan mengirimkan web pages yang direquestnya. Ada beberapa jenis dari server yang tersedia dengan jenis service yang berbeda seperti:

1. Web Servers
2. Email Servers
3. FTP Servers

Sebenarnya kata **"Severless Computing"** kurang pas. Karena teknologi ini masih membutuhkan sebuah server. Yang membedakan adalah, kita tidak membutuhkan maintenance sebuah physical server. Server dimaintenance dalam sebuah cloud dan kita hanya menyediakan perintah yang dibutuhkan ke cloud untuk memastikan bahwa server bekerja sesuai dengan apa yang kita mau. Biasanya, intruksi2 tersebut dikirimkan dengan menggunakan sebuah function.

 **AWS Lambda** dikenalkan oleh Amazon pada tahun 2014, yaitu public cloud pertama yang memperkenalkan teknologi severless computing. Awalnya, hanya disupport menggunakan Node.js. Dan untuk saat ini sudah disupport bahasa pemrograman lain termasuk Java dan Python.

 **Google Firebase**, juga memperkenalkan fasilitas serverless menggunakan Cloud Function. Developers mengupload backend code mereka dalam sebuah function ke cloud dan cloud akan secara otomatis mengeksekusi logic yang bersangkutan berdasarkan event triggers dan HTTP requests.

 Sekarang pastinya kita akan berpikir sebenarnya ini hanya jenis lain dari cloud computing. Sebenarnya, serverless computing didasarkan oleh FaaS (Functions As A Service). Terdapat beberapa keuntungan menggunakan architecture ini dikarenakan ada di environment cloud:

1. Process deployment yang simple
2. Tidak membutuhkan infrastructure dan administrasi yang complex
3. Mendukung architecture microservices
4. Dynamic resource Allocation
5. Cost yang lebih hemat (berdasarkan pemakaian)
6. Scalability

Sekarang kita akan coba experiment pada serverless computing menggunakan Google Firebase yang dibisa digunakan gratis untuk belajar.

Kita akan membuat 2 buah functions dan upload ke dalam firebase. Function pertama menggunakan HTTP request untuk menyimpan input kedalam database. Yang kedua berdasarkan Firebase event triggers yang akan secara otomatis mengeksekusi setiap request yang tersimpan pada database untuk mengconverst input menjadi Uppercase. Referensi https://firebase.google.com/docs/functions/get-started.

> *Pastikan kita sudah mempunyai node.js yang sudah terinstall*

1. Pertama, install Firebase CLI menggunakan command:

    `npm install -g firebase-tools`

2. Authentication dan Initialization

    Run command berikut untuk menjalankan authentifikasi dan initialize project. Kita akan membutuhkan sebuah google account untuk proses authetifikasi.

    `firebase login`

    Ketika command ini dieksekusi, browser akan diredirect ke login page. Masukan credetials dan ketika semuanya berjalan dengan lancar, kembali lagi ke console di firebase dan buatlah sebuah project baru. Local project akan di synced up ketika menginitiating project tersebut.

    `firebase init functions`

    `Functions` disini adalah nama projectnya. Ketika perintah ini dieksekusi kita akan ditanya untuk memilih default project dan kita akan diberikan project yang sudah di create di Firebase. Pilih project yang sesuai dan process, process akan berjalan dengan menginstall semua dependencies yang dibutuhkan.

3. Import Modules

    Ketika setup sudah selesai, pada project folder kita akan melihat file `index.js`. File ini digunakan untuk koding functions kita yang akan digunakan untuk upload ke Firebase.

    Pertama, kita butuh untuk import Cloud Function untuk membuat functions dan setup triggers. Kemudian Admin SDK dibutuhkan untuk mengakses Database Firebase secara Real-Time untuk save dioutput kita.

    ```Javascript
    // File: loading_modules.js
    // Load the Cloud Functions
    const functions = require('firebase-functions');

    // Load firebase admin to access the firebase realtime database.
    const admin = require('firebase-admin');
    admin.initializeApp(functions.config().firebase);
    ```

4. Tambahkan function pertama kita

   Code function untuk menyimpan input kedalam database
    
    ```Javascript
    // File:save_input.js
    exports.saveInput = functions.https.onRequest((req, res) => {
        // Get the text parameter.
        const original = req.query.text;
        // Save the text
        return admin.database().ref('/messages').push({original: original}).then((snapshot) => {
            // Redirect with 303 SEE OTHER to the URL of the pushed object in the Firebase console.
            return res.redirect(303, snapshot.ref);
        });
    });    
    ```

    Jika cukup familiar dengan Node.js tidak banyak yang berbeda disini. Pada dasarnya, kita mengcapture input dari sebuah request dan disimpan dalam database via admin module pada path `/message`. Setiap text kita akan menyimpannya dibawah messages dalam real-time database. Kita bisa melihat bentuk ini pada dashboard Firebase ketika mengeksekusi sebuah function.

5. Menambkan Function kedua

    ```Javascript
    // File: uppercase_function.js
    exports.convertUppercase = functions.database.ref('/messages/{pushId}/original').onWrite((event) => {
        // Capture the original value
        const original = event.data.val();
        const uppercase = original.toUpperCase();
        // writing new value.
        return event.data.ref.parent.child('uppercase').set(uppercase);
    });
    ```

    Karena ini adalah sebuah `event triggered function` kita dapat mengcapture original value dari sebuah event. Kemudian mengconvert nya kedalam uppercase dan menyimpannya dalam "uppercase". Hasilnya akan terlihat pada dashboard Firebase ketika mengeksekusi.

6. Deploy Functions

    Pada tahapan ini kita sudah mengimplementasikan function kita dan sekarang waktunya untuk mendeploy mereka kedalam cloud, Jalankan command dibawah ini untuk mendeploy functions:

    `$ firebase deploy --only functions`

    Kita akan melihat process ini mendeploy semua functions kita langkah demi langkah dan akan memberikan sebuah URL untuk trigger `HTTP triggered function`. Kita dapat menggunakannya untuk melewati sebuah text dengan URL parameter (`xyz.com/saveInput?input=test`). Ketika process completed untuk proses check real-time database menggunakan Firebase dashboard. Kita akan melihat section yang di create sebagai sebuah "messages" dan text yang kita pass akan tersimpan disana sebagai "original". Text ini berisi uppercase test sebagai "uppercase". Coba balik lagi ke code diatas untuk dipahami.

