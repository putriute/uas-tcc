Perintah yang digunakan untuk mengkloning repo lab dari GitHub, ini akan membuat salinan repo laboratorium di sub-direktori baru bernama linux_tweet_app.

git clone https://github.com/dockersamples/linux_tweet_app

#1 Run some simple Docker containers

1.Pada langkah ini akan dimulai sebuah wadah baru dan memintanya untuk menjalankan perintah nama host. Kontainer akan mulai, jalankan perintah hostname, lalu keluar.

$ docker container run alpine hostname

2. Docker menjaga wadah berjalan selama proses itu dimulai di dalam wadah masih berjalan. Dalam hal ini proses nama host keluar segera setelah output ditulis. Ini artinya wadah berhenti. Namun, Docker tidak menghapus sumber daya secara default, sehingga wadah masih ada dalam status Keluar.

$ docker container ls --all

	1.1 disini menjalankan wadah Ubuntu Linux di atas host Alpine Linux Docker (Play With Docker menggunakan Alpine Linux untuk node-node-nya) dengan perintah :
$ docker container run --interactive --tty --rm ubuntu bash

	1.2 perintah ls / akan mencantumkan isi direktur root dalam wadah, ps aux akan menunjukkan proses yang berjalan dalam wadah, cat / etc / issue akan menunjukkan distro Linux mana wadah berjalan, dalam hal ini Ubuntu 18.04.3 LTS.
$ ls /
> ps aux
$ cat /etc/issue

	1.3 Ketik exit untuk keluar dari sesi shell. Ini akan menghentikan proses bash, menyebabkan wadah untuk keluar.
> exit

	1.4 perhatikan bahwa host VM menjalankan Alpine Linux, namun dapat menjalankan wadah Ubuntu. Seperti disebutkan sebelumnya, distribusi Linux di dalam wadah tidak perlu cocok dengan distribusi Linux yang berjalan di host Docker.

1.1.1 penjelasan perintah :
--detach akan menjalankan kontainer di latar belakang.
--name akan menamainya mydb.
-e akan menggunakan variabel lingkungan untuk menentukan kata sandi root (
Karena gambar MySQL tidak tersedia secara lokal, maka Docker secara otomatis menariknya dari Docker Hub.

1.1.2
$ docker container ls

1.1.3
periksa apa yang terjadi di wadah dengan menggunakan beberapa perintah Docker bawaan: log kontainer buruh pelabuhan dan bagian atas wadah buruh pelabuhan.

$ docker container logs mydb

$ docker container top mydb

1.1.4
Daftar versi MySQL menggunakan exec kontainer buruh pelabuhan.
exec buruh pelabuhan memungkinkan untuk menjalankan perintah di dalam wadah. 

$ docker exec -it mydb \
> mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version

1.1.5 gunakan exec container docker untuk terhubung ke proses shell baru di dalam wadah yang sudah berjalan. Menjalankan perintah di bawah ini akan memberi shell interaktif (sh) di dalam wadah MySQL.

$ docker exec -it mydb sh
Perhatikan bahwa prompt shell telah berubah. Ini karena sekarang terhubung ke proses sh yang berjalan di dalam wadah.

1.1.6
$ mysql --user = root --password = $ MYSQL_ROOT_PASSWORD --version
Perhatikan outputnya sama seperti sebelumnya.

1.1.7
$ exit 



