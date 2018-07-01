---
layout: post
title: "Data Visualization - The Right Chart!"
image: https://preview.ibb.co/jEm4NJ/Charts_and_Graphs_image_1080x675.jpg
comment: true
categories:
  - Data Visualization
tags:
  - Chart
  - Data Visualization
  - Business Intelligence
---

Menjadi sekumpulan angka menjadi bermakna adalah sebuah seni, seni dari data visualization. Dengan data tersedia yang penuh dengan `noise`, untuk mengolahnya menjadi sebuah insight, kerjaan kita ga hanya misahin `noise` itu dari data, tapi juga me-represent-kannya dengan cara yang benar.

Perhatikan contoh chart berikut:

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/3d-powerpoint-chart.png)

Dan ini yang akan terjadi kita me-present-kannya:

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/tufte-wallpaper.png)

Dengan beberapa audience didepan lu, CMO sibuk telpon, CTO sibuk mainan laptop, dan CEO malah bobo! Akhirnya lu keluar nyari kucing atu-atu buat dicekik!

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

## Pie Chart

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_pie_chart.png)

Pie chart merupakan chart yang paling sering digunakan dimana-mana dan cukup banyak kesalahan dalam penggunaannya, contoh penggunakan chart dari gambar adalah penggunaan yang kurang tepat, terlalu banyak component, dengan value ga jauh beda.

Pie chart bagusnya nge-present value dalam bentuk percentage, digunakan untuk visualisasi sebagai bagian dari keseluruhan relationship atau composition. Pie chart bukan digunakan untuk comparison, gunakan bar chart untuk hal itu.

Kalau memungkinkan, hindari pie chart. Karena kebanyakan orang berpikir linear, tapi ketika melihat dengan ukuran sudut atau area, kebanyakan dari user ga bisa cepat memahaminya dengan baik.

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_pie_chart_angles.png)

Kalo yang gambar diatas akan terlihat lebih baik ketika digunakan untuk comparation dalam menggunakan bar chart.

## Stacked Pie Chart
![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_donut_chart.png)

Seperti sangat tidak disarankan menggunakan chart ini, sangat sulit untuk dipahami, gunakan bar chart dengan mode stacked saja.

Ini ada contoh penggunakan pie chart yang efisien.

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_pie_to_bar.gif)

Eh ternyata malah ga jadi Pie yak. lol.

### Hal yang perlu dan tidak perlu dilakukan ketika menggunakan Pie Chart!
Buat lu ngerasa sentimental buat Pie Chart di PowerPoint, dan ingin tetap menggunakannya, ini ada beberapa tips yang perlu diperhatikan.

- Pastikan untuk total sum dari semua segment berjumlah 100 percent.
- Gunakan Pie Chart hanya jika lu mempunyai sedikit kategori kurang dari enam, atau ada beberapa segment yang lu pengin user focus kesitu (beberapa segment yang terlihat jelas daripada segment yang lain).
- Idealnya, kategori hanya ada dua, seperti pria dan wanita. Jadi user focus dengan cepat untuk mencari nilai yang lebih dari 50 percent, atau hanya satu kategori terbesar, seperti market share yang dicompare dengan keseluruhan market (keseluruhan ya bukan tiap item)
- Jangan gunakan pie chart ketika value dari kategorinya hampir sama.
- Jangan gunakan effect 3D atau effect2 alay yang lain, hal tersebut menggurasi proporsi yang sebenarnya.

## Scatter Plots

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_scatter_plot_chart.png)

Scatter chart secara harfiah digunakan untuk correlation dan distribution. Bagus untuk menunjukkan relationship antara dua variable dimana yang satu berkorelasi dengan yang lain (atau tidak).

Scatter chart juga bisa digunakan untuk data disribution atau clustring trend dan membantu untuk menemukan anomali atau outlier.

Contoh, correlation antara marketing spending vs revenue.

## Bubble Chart

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_bubble_chart.png)


Bubble Chart adalah pilihan yang bagus jika lu butuh untuk menambahkan dimensi lain pada scatter plot chart. Scatter Plot meng-compare dua value, tapi lu dapat menambahkan ukuran bubble sebagai axis ketiga serta digunakan sebagai comparation. Jika bubble sangat mirip secara ukuran, gunakan label.

Kita bisa menambahkan axis keempat dengan menjadikan setiap buble sebagai pie chart, tapi keknya itu terlalu complex. lol.

Contoh, bubble chart untuk marketing expenditure vs revenue vs profit. Standar scatter plot bisa menunjukkan correlation antara marketing cost dan revenue (secara jelas), ketika si bubble menunjukkan bertambahnya cost untuk marketing hal tersebut memberikan pengaruh yang signifikan terhadap profit.

Gunakan Scatter dan Bubble chart untuk:
- Menunjukkan relationship antara dua variable (scatter) atau antara tiga variable (bubble).
- Plot dua atau tiga himpunan variable kedalam satu x-y koordinat.
- Jadikan horizontal axis kedalam skala logarithmic, hal tersebut akan menunjukkan relationship antara element yang dengan semua distribusinya
- Gunakan untuk mencari pattern dalam himpunan data yang besar, trend yang linear atau gak linear, correlation, cluster atau outlier.
- Gunakan data point yang tidak didasarkan variable waktu.
- Gunakan untuk relationship dan bukan untuk comparison.

## Map Chart
![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_map_chart.png)

Map chart bagus untuk memberikan value secara geographical context untuk cepat menemukan spot terbaik dan terburuk dari suatu area secara performance, trend dan outlier. Jika lu mempunyai banyak data tetang lokasi berbentuk koordinat, nama negara, atau alamat, lu dapat plot data tersebut pada map chart.

Maps tidak cukup bagus untuk comparison, karena map biasanya menggunakan color yang ter-scale dan kebanyakan user cukup susah untuk membedakan warna yan ter-scale. Kadang lebih mudah dengan menggunakan bubble jika ingin menyertakan value yang exact untuk menjelaskan comparison.

Contoh, pengunjung website berdasarkan negara, kota atau sales berdasarkan kota.

Tapi jangan gunakan map untuk semua jenis data yang ada variable geographicnya. Sekarang sudah banyak data yang mempunyai variable geographic, tapi bukan berarti harus plot data tersebut dengan map.

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/to_much_data_on_map.jpg)

When to use map charts?

If you want to display quantitative information on a map.
To present spatial relationships and patterns.
When a regional context for your data is important.
To get an overview of the distribution across geographic locations.
Only if your data is standardized (that is, it has the same data format and scale for the whole set).

### Kapan menggunakan Map?
- Jika lu ingin display informasi kuantitatif pada map.
- Untuk menunjukkan relationship dan pattern secara spartial.
- Ketika context untuk region itu penting.
- Untuk menunjukkan overview pada distribusi secara geographic.
- Jika dan hanya jika datanya udah standar (sama formatnya dan skalanya)

## Gantt Chart
![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_gantt_chart.png)

Sesuai nama orang yang menggunakannya pada tahun 1910an, Henry Gantt.

Gantt bagus untuk planning dan project timeline. Karena sebenarnya dibuat untuk project maps, mengilustrasikan apa yang perlu dikerjakan, urutannya, dan deadlinenya. Lu bisa memvisualisasikan total waktu yang perlu diambil dalam sebuah project, resource yang terlibat, dan dependencynya dengan tugas yang lain.

Tapi project planning bukan satu2nya aplikasi dari Gantt. Gantt juga bisa digunakan untuk bisnis rental, menunjukkan list item untuk dirental (mobil, kamar) dan periode rental dari item tersebut.

![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_map_chart_example.png)

Variable yang dibutuhkan untuk menggunakan Gantt, setidaknya hal yang dibutuhkan adalah percentase penyelesaian suatu tugas dan dependency dengan tugas yang lain.

## Gauge Chart
![](https://eazybi.com/static/img/blog_page/posts/2016_03_01/data_visualization_guage_chart.png)

Gauge keknya nama orang juga tapi gue ga tahu siapa. Gauge cocok untuk digunakan untuk menunjukkan KPI (Key Performance Indicator). Gauge biasanya digunakan untuk single key value, comparing nya dengan color-coded sebagai level indicator, biasanya hijau untuk yang bagus dan merah untuk yang bermasalah.

Dashboard akan jadi tempat yang bagus untuk penggunaan Gauge. Semua KPI akan ada disatu tempat dan cepat dalam penyampaian "Heath Check" dari suatu project atau perusahaan.

Gauge bagus untuk digunakan sebagai:
- Untuk menunjukkan suatu progress dalam sebuah goal.
- Untuk menunjukkan pengukuran secara percentile dalam sebuah KPI.
- Untuk menunjukkan exact value dan meaning dari single measure.
- Menunjukkan sedikit informasi yang secara cepat bisa dipahami.
- Kebalikannya, Gauge membutuhkan banyak space dan biasanya hanya menunjukkan single point dari sebuah data. Jika ada banyak Gauge yang dicompare, lebih baik gunakan column dengan indikator tambahan sebagai threshold mungkin akan lebih sederhana dan efektif.
