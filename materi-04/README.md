Penjelasan materi-04 Docker Orchestration Hands-on Lab

# 1: What is Orchestration
Jadi, apa itu orkestrasi?
Orkestrasi mungkin paling baik digambarkan menggunakan contoh. Katakanlah Anda memiliki aplikasi yang memiliki lalu lintas tinggi bersama dengan persyaratan ketersediaan tinggi. Karena persyaratan ini, Anda biasanya ingin menggunakan setidaknya 3+ mesin, sehingga jika tuan rumah gagal, aplikasi Anda masih dapat diakses dari setidaknya dua lainnya. Jelas, ini hanya sebuah contoh dan kasus penggunaan Anda kemungkinan akan memiliki persyaratan sendiri, tetapi Anda mendapatkan idenya.

Menyebarkan aplikasi Anda tanpa Orkestrasi biasanya sangat memakan waktu dan rawan kesalahan, karena Anda harus secara manual SSH ke setiap mesin, mulai aplikasi Anda, dan kemudian terus mengawasi hal-hal untuk memastikan itu berjalan seperti yang Anda harapkan.

Tetapi, dengan Perkakas orkestrasi, Anda biasanya dapat melepas sebagian besar pekerjaan manual ini dan membiarkan otomatisasi melakukan pekerjaan berat. Salah satu fitur keren Orkestrasi dengan Docker Swarm, adalah Anda dapat menggunakan aplikasi di banyak host dengan hanya satu perintah (setelah mode Swarm diaktifkan). Plus, jika salah satu node pendukung mati di Docker Swarm Anda, node lain akan secara otomatis mengambil beban, dan aplikasi Anda akan terus bersenandung seperti biasa.

Jika Anda biasanya hanya menggunakan docker run untuk menyebarkan aplikasi Anda, maka kemungkinan besar Anda akan mendapat manfaat dari menggunakan Docker Compose, Docker Swarm mode, atau keduanya Docker Compose dan Swarm.


# 2: Configure Swarm Mode
$ docker run -dt ubuntu sleep infinity

Perintah ini akan membuat wadah baru berdasarkan ubuntu: gambar terbaru dan akan menjalankan perintah tidur untuk menjaga wadah tetap berjalan di latar belakang. Anda dapat memverifikasi wadah contoh kami sudah habis dengan menjalankan buruh pelabuhan ps pada node1.

$ docker ps

Perintah ini akan membuat wadah baru berdasarkan ubuntu: gambar terbaru dan akan menjalankan perintah tidur untuk menjaga wadah tetap berjalan di latar belakang. Anda dapat memverifikasi wadah contoh kami sudah habis dengan menjalankan buruh pelabuhan ps pada node1....

$ docker swarm init --advertise-addr $(hostname -i)

$ docker info

$ docker node ls

Perintah docker node ls menunjukkan bahwa semua node yang ada di swarm serta perannya di swarm, mengidentifikasi node dari mana perintah dikeluarkan.


# 3.1 - Deploy the application components as Docker services

$ docker service create --name sleep-app ubuntu sleep infinity

$ docker service ls

Status layanan dapat berubah beberapa kali hingga berjalan. Gambar sedang diunduh dari Docker Store ke mesin lain di Swarm. Setelah gambar diunduh, wadah masuk ke keadaan berjalan di salah satu dari tiga node.

Pada titik ini mungkin tidak terlihat bahwa kami telah melakukan sesuatu yang sangat berbeda dari hanya menjalankan buruh pelabuhan .... Kami telah lagi menggunakan satu kontainer pada satu host. Perbedaannya di sini adalah bahwa wadah telah dijadwalkan pada gugus gerombolan.


# 4: Scale the application

$ docker service update --replicas 7 sleep-app

Manajer Swarm menjadwalkan sehingga ada 7 wadah aplikasi tidur di kluster. Ini akan dijadwalkan secara merata di seluruh anggota Swarm.

Kita akan menggunakan perintah docker layanan aplikasi sleep-app. Jika Anda melakukan ini cukup cepat setelah menggunakan opsi --replicas Anda dapat melihat wadah muncul secara real time.

$ docker service ps sleep-app

$ docker service update --replicas 4 sleep-app

$ docker service ps sleep-app


# 5: Drain a node and reschedule the containers
$ docker node ls

$ docker ps

$ docker node ls

$ docker service ps sleep-app


Jalankan perintah docker service rm sleep-app pada node1 untuk menghapus layanan yang disebut myservice.

$ docker service rm sleep-app

$ docker ps

$ docker swarm leave --force

$ docker swarm leave --force

$ docker swarm leave --force
