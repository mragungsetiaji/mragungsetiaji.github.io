# Data Visualization - The Right Chart!

Menjadi sekumpulan angka menjadi bermakna adalah sebuah seni, seni dari data visualization. Dengan data tersedia yang penuh dengan `noise`, untuk mengolahnya menjadi sebuah insight, kerjaan kita ga hanya misahin `noise` itu dari data, tapi juga me-represent-kannya dengan cara yang benar.

Perhatikan contoh chart berikut:

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/3d-powerpoint-chart.png)

Dan ini yang akan terjadi kita me-present-kannya:

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/tufte-wallpaper.png)

Dengan beberapa audience didepan lu, CMO sibuk telpon, CTO sibuk mainan laptop, dan CEO malah bobo! Akhirnya lu keluar nyari kucing atu-atu!

Untuk mencegah kegagalan dari presentasi kita, mari coba belajar basic dari data visualization. Semoga setelah ini kita bisa menyelamatkan populasi anak-anak kucing yang jadi korban.

> Save kitten, Save the World!

## Data Visualization - Basic

Pada dasarnya adalah empat dasar tipe presentasi yang bisa lu gunakan untuk presentasi dari data lu.

    - Comparison
    - Composition
    - Distribution
    - Relationship

Bisanya yang paling sering dipakai adalah Comparison dan Composition. Kecual lu sesorang statistician atau data analyst yang bisa pakai semuanya.

## Pemilihan Chart yang sesuai
Untuk mendefisinikan chart yang paling sesuai untuk setiap jenis presentasi, pertama lu harus jawab setiap pertanyaan berikut:

- Berapa banyak variable yang ingin ditunjukan dalam sebuah single chart? atu, dua, tiga, banyak?
- Berapa banyak item (data points) yang akan di display untuk setiap variable? cuma sedikit atau banyak?
- Mau display data berdasarkan periode waktu, atau dari compare item atau group?

Bar chart bagus untuk perbandingan antara item, sementara line chart untuk trend. Scatter plot chart bagus untuk relationships dan distributions, tetapi pie chart lebih baik untuk simple compositions jangan untuk comparison atau distributions.

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/chart-selection-diagram.png)

Sumber: http://extremepresentation.typepad.com/files/choosing-a-good-chart-09.pdf

Ayo kita coba review lebih dalam tipe chart yang paling sering digunakan, sama contohnya dan pro-con setiap tipe chartnya.

# Table

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_table_chart.png)

Table adalah source penting dari semua chart. Digunakan paling baik untuk comparison, composition atau relationship ketika hanya ada sedikit variable atau data point. Jadi jangan membuat chart kalau datanya aja bisa dengan mudah di interpret dari table.

Gunakan table ketika:

- Lu butuh compare atau look up value secara individu
- Lu butuh value yang tepat
- Value yang didapat dari multiple measurement unit
- Data harus diinformasikan secara kuantitatif bukan secara tren

Gunakan chart ketika:

- Apakah ada story atau message yang tersirat dari pattern datanya
- Apakah digunakan untuk menujukkan relasi dari beberapa value

**Contoh:** jika lu mau menunjukkan `rate of change`, seperti perubahan tiba-tiba dari temperature, lebih bagus gunakan chart seperti line karena `rate of change` tersebut sulit untuk dilihat dari table.

## Column
![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_column_chart.png)

Column mungkin jadi chart yang paling sering digunakan. Chart ini jadi pilihan terbaik untuk compare value yang berbeda ketika value yang spesifik sangatlah penting, dan diexpectasikan bahwa user akan look up dan compare value individual diantara setiap column.

Dengan column lu bisa compare value untuk setiap kategori yang berbeda atau compare value yang berganti setiap periode waktu untuk single kategori.

Tips untuk penggunaan column:
- Gunakan column untuk comparison jika banyaknya category cukup kecil sampai lima, tapi jangan untuk lebih dari tujuh category.
- Jika salah satu dimensinya adalah waktu (tahun, kuatral, bulan, minggu, hari, jam), lu harus selalu gunakan waktu di axis-x
- Di chart, waktu harus selalu dari kiri ke kanan, jangan pernah dari atas ke bawah
- Numerical axis harus mulai dari nol. Mata kita sangat sensitif pada tingginya sebuah column, dan kita bisa mengarah ke kesimpulan yang salah ketika bar-nya dipotong
- Hindari penggunaan pattern line atau fill. Hanya gunakan border untuk highlight
- Hanya gunakan column untuk menunjukkan tren yang beralasan dengan sedikit banyaknya data point (kurang dari 20) jika setiap data point punya value yang clear dan jelas

## Column Histogram
![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_analytics_histogram_chart.png)

Histogram adalah variasi yang sering ada dari column dan digunakan untuk present distribusi dan relationships dari single variable dalam sekumpulan kategori. Contoh yang bagus dari sebuah histogram bisa berupa distribusi dari hasil ujian sekolah atau sejenisnya, dibagi dengan ukuran kelasnya.

## Stacked Column
![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_stacked_column_chart.png)

Gunakan stacked column untuk menunjukkan composition. Jangan menggunakan terlalu banyak item untuk composition (tidak boleh lebih dari 3 atau 4) dan pastikan composition partsnya relatif sama sesuai ukurannya.

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_data_ink_ratio.gif)

## Bar Charts

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_bar_chart.png)

Bar Chart juga horizontal column charts yang cukup penting.

Jika lu punya nama kategori yang panjang, bagus kalau menggunakan bar charts karena ini memberikan space lebih buat text panjang. lu juga perlu menggunakan bar chart daripada column chart ketika banyaknya kategori lebih banyak dari 7 (tetapi tidak lebih dari 15) atau untuk display himpunan dengan bilangan negative.

- Pengunaan bar chart biasanya terdapat pada traffic pengunjung dari referral websites teratas. Referre sites juga biasanya lebih dari 5 sampai 7 sites dan nama website yang cukup panjang, jadi lebih baik menggunakan grafik secara horizontal.
- Contoh yang lain bisa berupa sales perfomance. Lagi, karena namanya yang cukup panjang dan mungkin lebih dari 7 orang sales.

## Bar Histograms

Sama seperti column, bar chart juga bisa digunakan untuk present histogram. Contoh histogram adalah distribusi populasi antara umur dan gender.

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/Population_pyramid_for_the_United_Kingdom_using_2011_census_data.png)

## Stacked Bar Charts

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_stacked_columns.png)

Stacked bars are not good for comparison or relationship analysis. The only common baseline is along the left axis of the chart, so you can only reliably compare values in the first series and for the sum of all series.

Stacked Bar ga bagus buat comparison atau analisa relationship. Yang menjadi dasarnya adalah sepanjang axis-y, jadi lu hanya bisa compare value pada series pertama untuk semua agregate dari setiap series.

## Line Charts
![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_line_charts.png)

Sopo seng ga suka pake line? Line chart adalah chart yang sering banget digunakan. Gunakan line ketika lu punya dataset continus. Line sangat bagus untuk visualisasi tren dari data yang berbasis waktu, ketika banyaknya data point cukup banyak (lebih dari 20).

Dengan line, penekannya ada pada continunya atau flow dari valuenya (tren), tetap masih bisa mendukung untuk value comparison, menggunakan data marker (untuk kurang dari 20 data points).

Line chart juga bagus sebagai alternatif pengganti column chart, jika chart terlalu kecil.

## Timeline Chart
![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_timeline_charts.png)

Timeline chart adalah variasi dari line chart. Sebenarnya, semua line chart yang menampilkan `values` berdasarkan periode waktu adalah timeline chart. Yang membedakan hanya difungsionalitas, sebagian besar timeline chart boleh di zoom in dan zoom out dan dicompress atau distretch berdasarkan axis waktu untuk melihat lebih detail atau tren secara menyeluruh.

Contoh bentuk timeline chart seperti:
- Harga saham
- Pengunjuang website perhari selama 30 hari belakang
- Banyaknya sales per hari selama kuarter terakhir

### Hal yang perlu dilakukan dan tidak untuk line chart:
- Gunakan line untuk menunjukkan data continus dalam sebuah skala interval, dimana interval adalah sama secara ukurannya.
- Untuk line chart, axis boleh tidak berawal dari 0 jika pesan yang dimaksudkan pada chart adalah rate dari perubahan atau keseluruhan trend, bukan value secara exact atau comparison. Lebih baik mulai axis dengan 0 untuk audience yang banyak karena beberapa orang mungkin bisa aja menginterpretkan chart jadi ga benar. 
- Axis waktu harus mulai dari kiri sampai kanan. Jangan skip values untuk data yang intervalnya konsisten present informasi tentang trend, contoh, hari tertentu dengan nilai nol. 
- Hapus guidelines untuk menekankan trend, rate of change dan untuk ngurangin distraction.
- Gunakan aspect rasio yang sesuai untuk menunjukan pentingnya sebuah informasi dan hindari effect miring yang banyak dramanya. Contoh presepsi yang bagus untuk kemiringan 45 derajat. (https://eagereyes.org/basics/banking-45-degrees)


## Area Chart
![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_area_charts.png)

Area chart pada dasarnya adalah sebuah line chart, bagus buat trend dan comparison. Area chart akan mengisi area dibawah line, jadi yang paling bagus adalah nge-present akumulasi value yang berubah berdasarkan waktu, seperti stok barang, banyaknya employee atau account (rekening).

Jangan gunakan Area chart untuk present value yang fluktuatif, seperti saham atau perubahan harga.

## Stacked Area
![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_stacked_area_charts.png)

Stacked area paling bagus digunakan untuk menunjukkan perubahan composition berdasarkan waktu. Contoh, perubahan market share dari beberapa top player atau revenue share dari beberapa produk berdasarkan waktu.

Stacked area boleh colorful, tapi lu perlu gunain dengan penjelasan, karena hal tersebut bisa jadi sebuah masalah. Jangan gunakan hal tersebut jika lu butuh exact comparison dan jangan stack bersamaan lebih dari tiga atau lima kategori.