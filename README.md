a. What is amqp?
AMQP adalah singkatan dari Advanced Message Queuing Protocol. Secara sederhana, ini adalah sebuah protokol standar yang digunakan untuk pengiriman pesan antar sistem atau aplikasi. Dalam tugas ini, AMQP berfungsi sebagai bahasa komunikasi yang memungkinkan aplikasi kita (publisher dan subscriber) untuk saling mengirim dan menerima event melalui perantara message broker (RabbitMQ) dengan aman dan terstruktur.


b. What does it mean? guest:guest@localhost:5672 , what is the first guest, and what
is the second guest, and what is localhost:5672 is for?
URL tersebut adalah jalur koneksi (connection string) yang digunakan oleh program Rust kita untuk bisa masuk dan terhubung ke server RabbitMQ. Berikut adalah rinciannya:

- guest yang pertama adalah username bawaan (default) dari RabbitMQ.

- guest yang kedua adalah password bawaan (default) dari RabbitMQ.

- localhost:5672 menunjukkan lokasi server beroperasi. localhost artinya RabbitMQ tersebut sedang berjalan di komputer lokal kita sendiri (lewat Docker), sedangkan 5672 adalah port standar yang dibuka oleh RabbitMQ khusus untuk menerima koneksi dari protokol AMQP.


### Simulating Slow Subscriber
![Slow Subscriber Queue](images/slow_subs.png)

**Penjelasan:**
Pada grafik *Queued messages* di atas, terlihat ada *spike* (lonjakan) pada garis merah. Lonjakan ini terjadi karena program *publisher* dijalankan beberapa kali secara cepat berturut-turut, sehingga pesan sempat menumpuk di dalam antrean (*queue*).

Pada percobaan yang saya lakukan, jumlah antrean pesan memuncak di angka 10. Hal ini disebabkan oleh kecepatan *publisher* dalam mempublikasikan *event* ke RabbitMQ yang jauh melebihi kecepatan *subscriber* dalam memprosesnya (karena adanya simulasi *delay* sistem pada *subscriber*).

Seiring berjalannya waktu, *subscriber* terus memproses pesan tersebut satu per satu dan mengirimkan *acknowledgement* kembali ke *broker*. Hasilnya, grafik jumlah antrean perlahan-lahan menurun miring hingga kembali ke angka 0, yang menandakan bahwa seluruh pesan yang sempat *bottleneck* tersebut sudah berhasil dikonsumsi dengan tuntas.