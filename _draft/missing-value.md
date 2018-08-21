Salah satu masalah paling umum yang gue sering hadapi dalam Data Cleaning / Exploratory Analysis adalah mising value. Pertama, pahami bahwa TIDAK ada cara yang cukup bagus untuk menangani missing value. Gue udah menemukan solusi yang berbeda untuk imputasi data tergantung pada jenis masalahnya: Time series, ML, Regresi, dll. Dan sulit untuk diselesaikan secara general. Dalam blog ini, gue coba meringkas metode yang paling umum digunakan dan mencoba mencari solusi yang struktural. 

Imputasi atau Delete Data
Sebelum ke metode imputasi, kita harus memahami alasan mengapa data bisa missing.

1. Missing at Random (MAR): Hilang secara random berarti bahwa kecenderungan untuk sebuah data point yang missing terkait dengan masalah saat observasinya, bukan terkait dengan datanya.
2. Missing Completly at Random (MCAR): Sebuah data point tertentu yang missing tidak ada hubungannya dengan hipotetis value atau data point pada variable yang berbeda.
3. Missing not a Random (MNAR): Dua alasan yang mungkin bahwa nilai yang missing tergantung pada hipotetis value (misalnya Orang dengan gaji tinggi umumnya tidak ingin mengungkapkan pendapatan mereka dalam sebuah survey) atau nilai yang missing tergantung pada beberapa nilai variabel lain (misalnya asumsi bahwa wanita umumnya tidak ingin mengungkapkan usia mereka, semakin tua dan belum menikah. Di sini, nilai yang missing dalam variabel usia dan pernikahan dipengaruhi oleh variabel jenis kelamin).

Dalam dua kasus pertama, aman kok menghapus data dengan nilai-nilai yang missing tergantung pada kemunculannya, sementara pada kasus ketiga menghapus pengamatan dengan nilai yang missing dapat menghasilkan bias dalam model. Jadi kita harus berhati-hati sebelum delete data observasi. Perhatikan bahwa imputasi tidak selalu memberikan hasil yang lebih baik.

![](https://cdn-images-1.medium.com/max/800/1*_RA3mCS30Pr0vUxbp25Yxw.png)

Listwise
Listwise deletion: menghapus semua data untuk observasi yang memiliki satu atau lebih nilai yang missing. Khususnya jika data yang missing terbatas cukup kecil pada data observasi, kita bisa pilih untuk menghilangkan kasus-kasus tersebut dari analisis. Namun dalam banyak kasus, seringkali tidak menguntungkan untuk menggunakan listwise. Hal ini karena asumsi MCAR biasanya jarang didukung. Akibatnya, metode listwise menghasilkan parameter dan perkiraan yang bias.

Pairwise
Pairwise deletion: menganalisa semua kasus di mana variabel of interest ada disitu dengan demikian memaksimalkan semua data yang tersedia berdasarkan analisis. Kelebihan teknik ini, meningkatkan kekuatan dalam analisis tetapi memiliki banyak kerugian. Ini mengasumsikan bahwa data yang missing adalah MCAR. Jika kita menghapus secara pairwise maka kita akan menghasilkan sejumlah pengamatan berbeda yang berkontribusi pada berbagai bagian pada model nantinya, yang dapat membuat interpretasi menjadi susah.

Drop Variabel
Menurut gue, selalu lebih baik menyimpan data daripada membuangnya. Kadang-kadang kita boleh drop variabel, tetapi hanya jika variabel itu tidak signifikan. Karena itu, imputasi selalu menjadi pilihan yang lebih disukai daripada drop variabel.

Metode Time-Series
- Last Observation Carried Forward (LOCF) & Next Observation Carried Backward (NOCB)
Ini adalah pendekatan statistik umum untuk analisis data longitudinal yang berulang di mana beberapa pengamatan tindak lanjut mungkin hilang. Data longitudinal melacak sampel yang sama pada titik waktu yang berbeda. Kedua metode ini dapat memperkenalkan bias dalam analisis dan berkinerja buruk ketika data memiliki tren yang terlihat.
- Interpolasi Linear
Metode ini bagus untuk time series dengan beberapa tren tetapi tidak cocok untuk data musiman (seasonal)
- Seasonal + Linear Interpolation
Metode ini berfungsi baik untuk data dengan tren dan musim
