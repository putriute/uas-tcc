Penjelasan materi "Application Containerization and Microservice Orchestration"

# 1: Containerized Link Extractor Script
-> melakukan pengecekan pada branch dan list file

$ git checkout step1
$ tree

-> menambahkan satu file baru (misal Dockerfile) pada langkah ini dengan perintah
$ cat Dockerfile

Dengan menggunakan Dockerfile ini, kita dapat menyiapkan gambar Docker untuk skrip ini. Mulai dari gambar Python Docker resmi yang berisi lingkungan run-time Python serta alat yang diperlukan untuk menginstal paket dan dependensi Python, kemudian menambahkan beberapa metadata sebagai label (langkah ini tidak penting, tetapi merupakan praktik yang baik). 
Berikutnya dua instruksi jalankan perintah install pip untuk menginstal dua paket pihak ketiga yang diperlukan agar script berfungsi dengan baik. Kami kemudian membuat direktori / aplikasi yang berfungsi, menyalin file linkextractor.py di dalamnya, dan mengubah izinnya untuk membuatnya menjadi skrip yang dapat dieksekusi.
Sejauh ini, kami baru saja menggambarkan bagaimana kami ingin seperti gambar Docker, tetapi tidak benar-benar membangun satu.

$ build gambar docker -t linkextractor: step1.
Perintah ini harus menghasilkan output seperti pada gambar 1.3

Kami telah membuat gambar Docker bernama linkextractor: step1 berdasarkan Dockerfile yang diilustrasikan di atas. Jika build berhasil, kita harus dapat melihatnya di daftar gambar:

$ docker image ls

Gambar ini harus memiliki semua bahan yang diperlukan yang dikemas di dalamnya untuk menjalankan skrip di mana saja pada mesin yang mendukung Docker.

$ docker container run -it --rm linkextractor:step1 http://example.com/


# 2: Link Extractor Module with Full URI and Anchor Text
Pada langkah ini skrip linkextractor.py diperbarui dengan perubahan fungsional berikut:

- Jalur dinormalisasi ke URL lengkap
- Melaporkan tautan dan teks jangkar
- Dapat digunakan sebagai modul di skrip lain

$ cat linkextractor.py

Logika ekstraksi tautan diabstraksi menjadi fungsi extract_links yang menerima URL sebagai parameter dan mengembalikan daftar objek yang berisi teks jangkar dan hyperlink yang dinormalisasi. Fungsi ini sekarang dapat diimpor ke skrip lain sebagai modul.

$ docker image build -t linkextractor:step2 .

$ docker container run -it --rm linkextractor:step2 https://training.play-with-docker.com/

$ docker container run -it --rm linkextractor:step1 https://training.play-with-docker.com/

Pada langkah berikutnya akan dilakukan pembangunan layanan web yang akan memanfaatkan skrip ini dan akan membuat layanan berjalan di dalam wadah Docker.

# 3: Link Extractor API Service

ketikkan perintah dibawah ini :
$ git checkout step3
$ tree

maka akan muncul 
.
├── Dockerfile
├── README.md
├── linkextractor.py
├── main.py
└── requirements.txt

0 directories, 5 files

Karena kita sudah mulai menggunakan requirement.txt untuk dependensi, kita tidak perlu lagi menjalankan perintah install pip untuk masing-masing paket. Arahan ENTRYPOINT diganti dengan CMD dan mengacu pada skrip main.py yang memiliki kode server itu karena kami tidak ingin menggunakan gambar ini untuk perintah satu kali sekarang.

Modul linkextractor.py tetap tidak berubah dalam langkah ini, jadi mari kita lihat main.py yang baru ditambahkan.

$ cat main.py

Di sini, kita mengimpor fungsi extract_links dari modul linkextractor dan mengubah daftar objek yang dikembalikan menjadi respons JSON.

$  docker image build -t linkextractor:step3 .

Kemudian jalankan wadah dalam mode terlepas (-d flag) sehingga terminal tersedia untuk perintah lain saat wadah masih berjalan. Perhatikan bahwa kami memetakan port 5000 dari wadah dengan 5000 host (menggunakan argumen -p 5000: 5000) agar dapat diakses dari host,  juga menetapkan nama (--name = linkextractor) ke wadah untuk membuatnya lebih mudah untuk melihat log dan membunuh atau menghapus wadah.

$ docker container run -d -p 5000:5000 --name=linkextractor linkextractor:step3

$ docker container ls

$ curl -i http://localhost:5000/api/http://example.com/

$ docker container logs linkextractor








