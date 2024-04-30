Refleksi

No 1:

Unary RPC:
- komunikasi bersifat one-to-one: klien mengirim request, server menerima request.
- Cocok untuk interaksi sederhana seperti authentication

Server Streaming
- Klien mengirim request, server mengirim banyak respons
- Cocok untuk interaksi request data yang banyak, seperti query dari database.

Bi-Directional
- Klien dan server dapat mengirim pesan satu dengan yang lain.
- Cocok untuk interaksi terus menerus antar client & server seperti aplikasi chatting, 

No 2:
Untuk authorization, harus dipastikan identitas klien sudah sesuai dengan permission akses server. Selain itu, ada baiknya menggunakan certificates agar server dan client dapat memverifikasi satu sama lain. Untuk authentication data password  perlu dienkripsi sebelum di-kirim.

No 3:
Masalah yang dapat timbul: race condition dan information loss, karena bisa saja beberapa client mengirim message ke server pada waktu yang sama persis. jadi perlu dilakukan skema synchronization yang teliti, seperti bagaimana menghadle data yang datang dan pergi (menggunakan buffer). Untungnya, Rust sudah memfasilitasi sebagian solusi dengan mmenerapkan immutable variables. Selain itu, pengelolaan memori juga penting, karena aliran data yang cepat dalam chatting aplication dapat meng-overload memory server. Jadi, perlu dipastikan semua data yang dikirim tersimpan di suatu tempat, atau jika belum ada tempatnya, delay pengiriman data.

No 4:
Kelebihan:
- integrasi dengan tokio, sehingga dapat membuat aplikasi yang asinkronus dan non-bloking.
- kemampuan membuat jenis/tipe receiver sendiri yang sesuai kebutuhan, contohnya melakukan pemrosesan data yang diterima sebelum dilanjutkan.

Kekurangan:
- menimbulkan masalah-masalah yang terkait dengan asynchronous programming, seperti output yang non-deterministic.
- learning curve yang tinggi karena harus mempelajari asynchronous programming.


No 5:
- Memisahkan fungsi-fungsi, menerapkan Single-Responsibility Principle. Mempengaruhi readibility juga.
- Menggunakan file .proto (Protocol Buffers) untuk mendefinisikan interface service untuk gRPC. File .proto dibuat terpisah dari code Rust untuk memastikan SRP.
- Menggunakan prost agar Rust dapat membuat code dari file .proto secara otomatis.

No 6:
- Hal paling mudah yang dapat dilakukan adalah memisahkan implementasi dari fungsi process_payment. Karena bisa saja (dalam kasus ini hampir pasti), akan terjadi penambahan code yang berhubungan dengan business logic yang akan dimasukkan dalam fungsi process_payment, sehingga jika dibuat terpisah programmer dapat lebih berkonsentrasi terhadap business logic tanpa harus berurusan dengan code untuk send-receive, dan sebaliknya. Selain itu, mungkin akan ada kasus di mana jenis payment yang berbeda akan dihandle secara berbeda pula, sehingga perlu dilakukan penambahan code. Maka kita harus memastikan bahwa kita tetap menerapkan Open-Closed Principle.


No 7:
- Penggunakan Protocol Buffers memungkinkan implementasi fitur dalam bahasa-bahasa pemrograman yang berbeda tanpa mengubah interface pada file proto.
- gRPC mengenerate code dari protobuf yang strongly-type, sehingga memastikan konsistensi tipe data.
- gRPC menggunakan binary serialization untuk mentrasfer data, sehingga lebih efisien dibandingkan JSON atau XML.
- gRPC support Bidirectional communication secara asynchronous, sehingga dapat membuat aplikasi-aplikasi seperti aplikasi chatting yang bersifat kolaboratif.


No 8:

Kelebihan:
- HTTP/2  memiliki binary framing layer yang dapat menghandle banyak request dan respons dalam 1 koneksi TCP, sehingga lebih efisien daripada HTTP/1.1
- HTTP/2 meng-compress headers sebelum pengiriman, sehingga mengurangi data yang dikirim. Hal ini sangat berpengaruh untuk request yang kecil (data sedikit) atau frekuensi pengiriman yang besar (sering), karena mengurangi overhead
- HTTP/2 support multiplexing: pengiriman banyak request dan respons secara concurrent dalam satu koneksi yang sama. Hal ini mengurangi jumlah koneksi yang dibutuhkan.

Kekurangan:
- HTTP/2 lebih kompleks dari HTTP/1.1, dan akan mengalami masalah backward compatibility terhadap sistem-sistem yang lebih lama.
- Multiplexing dan header compression memerlukan sumber daya CPU yang lebih besar, karena harus mengatur alur pengiriman data yang banyak, concurrent, dan dua arah.
- Kompleksitas dari HTTP/2 menyebabkan debugging yang lebih sulit karena harus mengerti konsep multiplexing dan concurrency.

No 9:

REST API
- bersifat request-response: client mengirim 1 request, server mengirim 1 response
- bersifat synchronous: client harus menunggu response sebelum melanjutkan proses.

gRPC
- bersifat bidirectional streaming: client dan server dapat mengirim banyak data dalam waktu yang sama
- bersifat asynchronous: tidak perlu saling tunggu response.

Secara umum gRPC lebih responsive dan lebih cocok untuk real-time communications, karena support pengiriman banyak data secara dua arah. Selain itu, sifat asynchronousnya memungkinkan pengiriman request tanpa menggangu proses yang lain.


No 10:

gRPC lebih cocok digunakan untuk sistem yang membutuhkan high-performance dan distributed, karena lebih efisien (transfer data yang cepat), aman (strongly typed) dan compatible terhadap banyak bahasa pemrograman (protobuf).JSON lebih baik digunakan untuk sistem yang lebih sederhana dan tidak membutuhkan performance yang sangat tinggi. JSON lebih mudah dibaca dan dipelajari, dan cocok untuk programmer pemula, dan sudah disupport oleh banyak platform pengembangan web. 




