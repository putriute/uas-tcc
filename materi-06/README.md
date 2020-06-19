Penjelasan materi-06 Kubernetes for Beginners

1. letak umum dari kode sumber:

ada file Tulis docker-compose.yml…

… Dan 4 layanan lainnya, masing-masing dalam direktori sendiri:

rng = layanan web menghasilkan byte acak

hasher = hash komputasi layanan web dari data POSTed

pekerja = proses latar belakang menggunakan rng dan hasher

webui = antarmuka web untuk melihat kemajuan


2. Menjalankan aplikasi
Buka direktori dockercoins, di repo hasil kloning:

cd ~ / dockercoins
Gunakan Tulisan untuk membuat dan menjalankan semua wadah:

docker-compose up
Compose memberi tahu Docker untuk membuat semua gambar kontainer (menarik gambar dasar yang sesuai), lalu memulai semua kontainer, dan menampilkan log agregat.

3. Konsep Kubernetes
- Kubernetes adalah sistem manajemen wadah, berjalan dan mengelola aplikasi kemas pada sebuah cluster

4. Hal-hal dasar yang dapat kita minta dari Kubernet
- Mulai 5 kontainer menggunakan image atseashop / api: v1.3
- Tempatkan penyeimbang beban internal di depan wadah ini
- Mulai 10 wadah menggunakan gambar atseashop / webfront: v1.3
- Tempatkan penyeimbang beban publik di depan wadah ini
- Ini Black Friday (atau Natal), lonjakan lalu lintas, tumbuhkan cluster kami dan tambahkan kontainer
- Rilis baru! Ganti wadah saya dengan gambar baru atseashop / webfront: v1.4
- Pertahankan permintaan pemrosesan selama peningkatan; perbarui wadah saya satu per satu

5. Hal-hal lain yang bisa dilakukan Kubernet untuk kita
- Autoscaling dasar
- Layanan berjalan lama, tetapi juga pekerjaan batch (sekali saja)
- Komitmen berlebihan pada kluster kami dan usir pekerjaan prioritas rendah
- Jalankan layanan dengan data stateful (database dll.)
- Kontrol akses berbutir halus menentukan apa yang dapat dilakukan oleh siapa pada sumber daya mana
- Mengintegrasikan layanan pihak ketiga (katalog layanan)
- Mengotomatiskan tugas-tugas kompleks (operator)

6. Arsitektur Kubernetes
	Arsitektur Kubernetes: master

* Logika Kubernetes ("otak" -nya) adalah kumpulan layanan:
	-server API (titik masuk kami ke semuanya!)
	-layanan inti seperti manajer penjadwal dan pengontrol
	-etcd (toko kunci / nilai yang sangat tersedia; "database" Kubernetes)

* Bersama-sama, layanan ini membentuk apa yang disebut "master"
	-Layanan ini dapat berjalan langsung pada host, atau dalam wadah (itu detail implementasi)
	-etcd dapat dijalankan pada mesin yang terpisah (skema pertama) atau co-located (skema kedua)
	-Kami membutuhkan setidaknya satu master, tetapi kami dapat memiliki lebih banyak (untuk ketersediaan tinggi)

7. Kontak pertama dengan kubectl
- kubectl adalah (hampir) satu-satunya alat yang kita perlukan untuk berbicara dengan Kubernetes

