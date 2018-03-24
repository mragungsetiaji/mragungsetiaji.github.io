---
layout: post
title: "Gentlemen Introduction Series : Docker, Container dan Virtual Machine!"
categories:
  - Docker
tags:
  - Docker
  - Container
  - Virtual Machine
---

# Docker, Container dan VM

>Docker: sebuah tools untuk packing, shipping dan running suatu program dengan menggunakan `"Containers"`.

Sebelum memahami bagaimana itu Docker, lebih dahulu memahami konsep fundamental dari sebuah "Container" dan dibandingkan dengan `"Virtual Machine (VM)"`. Di google banyak mengenai penjelasan hal tersebut namun tidak ada yang cukup mudah untuk dipahami oleh beginner (seperti saya).

## Container dan VM?

Container dan VM mempunyai tujuan yang sama, untuk mengisolasi sebuah program dan `dependency`-nya kedalam sebuah `self-contained unit` yang dapat running dimana saja.

Container dan VM menghilangkan kebutuhan tentang physical hardware, mengijinkan kita untuk lebih efisien menggunakan resource dari sebuah komputer, dari segi konsumsi energi dan penggunaan cost secara efektif.

Perbedaan yang jelas terlihat dari containers dan VMs adalah arsitekturalnya. coba kita lihat lebih jauh.

## Virtual Machines

VM pada dasarnya adalah emulasi (tiruan) dari komputer yang sesungguhnya yang mengeksekusi program seperti komputer sungguhan. VM running di atas physical machine menggunakan "hypervisor". Hypervisor berjalan pada host machine atau "bare-metal"

> **Hypervisor** adalah potongan dari sebuah software, firmware atau hardware dimana VM berjalan diatasnya. Hypervisor sendiri berjalan diatas physical computer, mengacu pada "host machine". Host machine menyediakan VM dengan resourcenya, termasuk RAM dan CPU. Resource trsebut dibagi diantara VM, dan dapat didistribusikan sesuai yang kita tentukan. Jadi jika satu VM berjalan dengan alokasi resource yang cukup banyak, kita bisa mengalokasikan resource lebih pada satu VM dibandingkan dengan VM yang lain di host machine yang sama.

VM yang sedang berjalan pada host machine (menggunakan sebuah hypervisor) dan juga dikenal dengan "guest machine". Guest Machine ini berisi dua program tersebut dan bagaimanapun GM dibutuhkan untuk menjalan program (misalkan, system binary dan library). GM juga membawa sebuah `virualized hardware stack` padanya, termasuk `virtualized network adapters`, `storage` dan CPU yang mengandung arti `full-fledged guest operating system`. Didalamnya, GM memiliki unit sendiri dan dedicated resources sendiri.

Seperti yang disebutkan diatas, GM dapat berjalan di `hosted hypervisor` ataupun pada sebuah `bare-metal hypervisor`. Ada beberapa bagian penting berbeda diantara keduanya.

Pertama, `hosted virtualization hypervisor` berjalan diatas OS dari host machine. Sebagai contoh, sebuah komputer menjalan OSX bisa mempunyai VM (VirtualBox atau VMWare Workstation 8) terinstall diatas OS tersebut. VM tidak memiliki direct access ke hardware, jadi VM mengakses melalui host operating system (dalam kasus ini, Mac's OSX).

Keuntungan dari sebuah `hosted hypervisor` adalah hardware yang melekat menjadi kurang penting. OS host memiliki kewajiban untuk menjalankan dirver hardware bukan hypervisor-nya sendiri, sehingga disinilah `hardware compatibility` dipertimbangkan. Disisi lain, tambahan layer ini diantara hardware dan hypervisor menciptakan kebutuhan resources yang berlebih, sehingga akan mengecilkan performance dari si VM nya.

Environment dari `bare mental hypervisor` mengatasi issu performance dengan menginstall dan menjalankannya dari hardware si host machine. Karena interfacenya langsung menanggani hardware yang bersangkutan, hal ini menjadikan dirinya tidak membutuhkan host OS untuk menjalankannya. Pada kasus ini, petama dengan menginstallnyua pada server host machine sebagai OS yang akan menjadi hypervisor. Tidak seperti host yang menjadi hypervisor, `bare metal hypervisor` mempunyai driver device sendiri dan berinteraksi langsung dengan setiap komponen untuk I/O, processing, atau OS task tertentu. Hal ini menghasilkan performance yang lebih baik, scalability dan stability. Ada tradeoff disini dimana hardware compatibilitynya terbatas karena hypervisor hanya dapat mempunyai banyak drivers built in didalamnya.

Hal yang bicarakan ini semua tentang hypervisors, kita mungkin akan menduga mengapa kita butuh tambahan layer hypervisor ini diantara VM dan host machine.

Jadi, karena VM mempunyai sebauh virtual operating system sendiri, hypervisor menjalankan aturan penting yang menyediakan VM dengan sebuah platform untuk memanage dan mengeksekusi OS guest ini. Dan mengijinkan host computer untuk share resource mereka kepada VM yang berjalan sebagai guest diatasnya.

{gambar}

Seperti yang kita lihat pada gambar tersebut, VM mengemas virtual hardware, sebuah kernel (OS) dan space untuk user pada setiap VM yang baru.

## Container

Tidak seperti VM yang menyediakan hardware virtualization, sebuah container menyediakan operating-system-level virtualization dengan mengabstraksi user space. Kita akan paham apa yang dimaksud ketika mendefinisikan lebih jauh tentang container.

Maksud dan tujuan dari container terlihat seperti VM. Sebagai contoh, keduanya mempunyai private space untuk processing, dan mengeksekusi commands sebagai root, mempunyai sebuah private network interface dan IP address, mengijinkan custom routes dan iptable rules, dapat mount file systems, dan sebagainya.

Perbedaan besar antara containers dan VM adalah containers men-share host system kernel dengan containers yang lain.

{gambar}

Gambar ini menunjukkan bahwa container hanya mengemas user space, dan bukan kernel atau virtual hardware seperti yang dilakukan oleh VM. Setiap container mendapatkan user space yang terisolasi sendiri untuk mengijinkan beberapa container berjalan pada satu host machine. Kita bisa melihat bahwa semua OS system level dishare across containers. Bagian yang hanya dibuat dari scratch adalah bin dan libs. Ini yang menjadikan container sangat lightweight (ringa).

## Lalu apa sebenarnya Docker itu?

Docker adalah sebuah open-source project based on Linux containners. Docker menggunakan feature dari linux kernel seperti namespace dan mengontrol group untuk membuat container diatas sebuah OS.

Google sudah menggunakan container mereka selama bertahun-tahun. Linux container yang lain seperti Solaris Zones, BSD jails dan LXC juga sudah digunakan selama bertahun-tahun.

Lalu kenapa Docker cepat berkembang?

1. **Ease of Use:** Docker dibuat untuk mudah digunakan setiap orang, developers, system admis, architects dan lainnya untuk memanfaatkan keuntungan dari container dalam hal build dan test portable application. Docker mengijinkan setiap orang untuk mengemas sebuah aplikasi pada laptop mereka, dimana bisa menjalankannya tanpa perlu memodifikasi pada public cloud manapun, private cloud, atau bahkan `bare metal`. Mantra ajaibnya adalah `"build once, run anywhere"`.

2. **Speed**: Docker containers sangat ringan dan cepat. karena container adalah sebuah sandboxed environment yang berjalan diatas kernel, mereka hanya mengambil sedikit resource. Kita bisa membuat dan menjalan Docker dalam hitungan detik, dibandingkan dengan VM akan memakan waktu yang cukup lama karena VM harus boot up seluruh virtual OS setiap waktu.

3. **Docker Hub**: Docker users juga mendapatkan keuntungan dari berkembangkan ecosystem dari Docker Hub, dimana kita bisa membuat "app store dari Docker Image". Docker Hub mempunya puluihan ribu public images yang disediakan oleh community yang sudah tersedia untuk digunakan. Sangat mudah untuk mencari images yang sesuai dengan apa yang kita butuhkan, siap untuk di pull down dan digunakan dengan sedikit atau tanpa modifikasi.

4. **Modularity dan Scalability**: Docker membuat hall mudah untuk di aplikasikan ke maasing-masing container. Contoh, kita ingin Postgres Database running pada sebuah container dan Redis server dilain sisi Node.js app juga. Dengan Docker hal ini akan menjadi lebih mudah untuk menghubungkan container tersebut secara bersamaan untuk membuat sebuah program, membuat hal ini mudah untuk scale atau update component secara indepeden dimana datang.

{gambar}

## Fundamental dari konsep Docker

{gambar}

### Docker Engine
Docker engine adalah layer dimana Docker berjalan. Runtime yang ringan dan tooling yang memanage containers, image, build dan lebih dari itu. DE berjalan secara native pada Linux System dan dibuat berdasarkan:

1. A Docker Daemon yang berjalan pada host computer.
2. A Docker Client yang berkomunikasi dengan Docker Daemon untuk mengeksekusi command.
3. A REST API untuk berinteraksi dengan Docker Daemon secara remote.

### Docker Client

Docker Client adalah kita sebagai end-user dari Docker yang berkomunikasi dengannya. Bisa sebagai UI dari Docker, sebagai contoh ketika mengeksekusi:

{gist}

Kita yang berkomunikasi dengan Docker Client dan kemudian instruksi tersebut di teruskan ke Docker Daemon.

### Docker Daemon

Docker daemon adalah yang sebenarnya mengeksekusi command yang dikirimkan oleh Docker Client, seperti building, running dan distributing container kita. Docker Daemon berjalan pada  host machine, tapi sebagai seorang user kita tidak pernah berkomunikasi langsung dengan Daemon. Docker Client dapat berjalan pada host machine dengan baik, tapi bukan hal yang diperlukan. DC dapat berjalan pada machine yang berbeda dan berkomunikasi dengan DD yang berjalan pada host machine.

### Dockerfile

Dockerfile dimana kita menuliskan intruksi untuk membuat sebuah Docker Image. Instruksi tersebut dapat berupa:

- **RUN apt-get y install some-package**: untuk menginstall sebuah package software
- **EXPOSE 8000:** port
- **ENV ANT_HOME /usr/local/apache-ant**: untuk menentukan environment variable

dan lain sebagainya. Contoh Dockerfile:

{gist}

### Docker Image

Docker Image adalah template read-only yang dibuat dari sebuah intruksi yang tertulis pada Dockerfile. Image tertulis aplikasi yang ingin kita package beserta dengan dependencies nya yang terlihat seperti '*and*' yang di process dan dirunning ketika launched.

Docker Image dibangu menggunakan sebuah Dockerfile. Setiap instruksi pada Dockerfile menambahkan layer baru kepada image, dengan layer yang merepresentasikan sebuah bagian dari image file system yang menambahkan atau mengganti layer dibawahnya. Layer adalah kunci dimana structure Docker sangat ringan. Docker menggunakan Unioon File System untuk meng-achieve ini:

### Union File Systems

Docker menggunakan Union File Systems untuk membangung sebuah Image. Kita dapat mengira bahwa Union File System adalah sebuah stackable file system, berarti file dan direktori dari separate file system (dikenal sebagai branches) dapat menjadi overlaid yang transparant ke bentuk sebuah single file system.

Contents dari direktori yang mempunyai path yang sama bersamaan dengan overlaid braches terlihat sebagai direktori yang single merged, yang menghindari kebutuhan untuk membuat copy dari setiap layer secara terpisah. Disamping, UNF bisa memberikan pointers dengan resource yang sama, ketika layer yang dimaksud perlu dimodifikasi, hal ini akan membuat sebuah copy dan modifikasi sebuah local copy, meninggalkan yang original dengan tidak ada yang diganti. Itu adalah bagaimana file system dapat muncul writeable tanpa mengijinkan writes mode (dengan kata lain, "copy-on-write" system)

Layers systems, ada dua keuntungan dari hal tersebut:

1. **Duplication-free**: layers membantu menghindari duplicating sebuah complete set dari files setiap waktu kita menggunakan sebuah image untuk create dan menjalankan sebuah container baru, membuat instantiation dari docker container sangat cepat dan murah.

2. **Layer segregation**: membuat pergantian menjadi lebih cepat, ketika kita mneganti image, Docker hanya menyebarkan untuk mengupdate layer yang sudah diganti.

### Volumes

Volumes adalah part of data dari sebuah container, menginialisasi ketika sebuah container dibuat. Volumes mengijinkan kita untuk share data dari container. Data Volume secara terpisah dari Union File System secara default dan ada secara direktori normal dan files pada host filesystem. Jadi, bahkan ketika kita destroy, update atau membangun lagi container, volumes data akan kembali tak tersentuh. Ketika kita ingin update sebuah volume, kita membuat sebuah pergantian kepadanya secara langsung (sebagai bonus yang ditambahkan, data volume dapat dishare dan digunakan oleh multiple container, yang lumayan rapi)

### Docker Containers

Sebuah Docker Container seperti yang didiskusikan diatas, 

