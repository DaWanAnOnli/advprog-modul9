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
Masalah yang dapat timbul: race condition dan information loss, karena bisa saja beberapa client mengirim message ke server pada waktu yang sama persis. jadi perlu dilakukan skema synchronization yang teliti, seperti bagaimana menghadle data yang datang dan pergi (menggunakan buffer). Selain itu, pengelolaan memori juga penting, karena aliran data yang cepat dalam chatting aplication dapat meng-overload memory server.

No 4
