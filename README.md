a. What is amqp?
AMQP adalah singkatan dari Advanced Message Queuing Protocol. Secara sederhana, ini adalah sebuah protokol standar yang digunakan untuk pengiriman pesan antar sistem atau aplikasi. Dalam tugas ini, AMQP berfungsi sebagai bahasa komunikasi yang memungkinkan aplikasi kita (publisher dan subscriber) untuk saling mengirim dan menerima event melalui perantara message broker (RabbitMQ) dengan aman dan terstruktur.


b. What does it mean? guest:guest@localhost:5672 , what is the first guest, and what
is the second guest, and what is localhost:5672 is for?
URL tersebut adalah jalur koneksi (connection string) yang digunakan oleh program Rust kita untuk bisa masuk dan terhubung ke server RabbitMQ. Berikut adalah rinciannya:

- guest yang pertama adalah username bawaan (default) dari RabbitMQ.

- guest yang kedua adalah password bawaan (default) dari RabbitMQ.

- localhost:5672 menunjukkan lokasi server beroperasi. localhost artinya RabbitMQ tersebut sedang berjalan di komputer lokal kita sendiri (lewat Docker), sedangkan 5672 adalah port standar yang dibuka oleh RabbitMQ khusus untuk menerima koneksi dari protokol AMQP.