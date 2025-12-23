[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/DGhYuEuO)

| Name                  | NRP        | Class |
|-----------------------|------------|-------|
| Angela Vania Sugiyono | 5025241226 | A     |


## Task 1

- Flag

  `JARKOM25{Ja0G_Bbbb4ng3t_S1_P4YVWL6MRC2ZVF7XIJP3XOI1UQ0U310xlovellj3rz1pffok9c6gvqfsc5bb1_f6f82decb468d621f1f112c2699ad548}`

> a. Berapa banyak packet yang terekam pada file pcapng?

> _a. How many packets are recorded in the pcapng file?_

**Answer:** `9596`

- Explanation

  `Jumlah total paket bisa langsung dilihat di status bar Wireshark atau bisa melalui menu Statistics → Capture File Properties.`

- Output result
  
![1.1](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal1/1.1.jpg?raw=true)

<br>
<br>

> b. Ada berapa jenis protocol (total) yang terekam pada traffic?

> _b. How many types of protocol (totals) are recorded in the traffic?_

**Answer:** `12`

- Explanation

  `Bisa menggunakan Statistics → Protocol Hierarchy untuk melihat daftar semua protokol yang terekam. `

- Output result
  
![1.2 & 1.3](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal1/1.2&1.3.jpg?raw=true)

<br>
<br>

> c. Ada berapa jenis protocol berbasis TCP yang terekam pada traffic?

> _c. How many types of TCP-based applications protocol are recorded in the traffic?_

**Answer:** `8`

- Explanation

  `Setelah menggunakan **Statistics → Protocol Hierarchy** untuk melihat daftar semua protokol yang terekam, fokus pada bagian bawah **Transmission Control Protocol (TCP)**, terlihat ada 8 protokol yang berjalan di atas TCP:
1. Virtual Network Computing (VNC)  
2. Thrift Protocol  
3. Telnet  
4. Signaling Compression  
5. Hypertext Transfer Protocol (HTTP)  
6. JavaScript Object Notation (JSON)  
7. HiPerConTracer Trace Service  
8. Data`

- Output result

![1.2 & 1.3](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal1/1.2&1.3.jpg?raw=true)

  <br>
  <br>

> d. Ada berapa banyak packet dengan protokol TCP murni yang terekam pada traffic (tanpa data)?

> _d. How many packets with pure TCP protocol are recorded in the traffic (without data)?_

**Answer:** `3223`

- Filter expression

  `frame.protocols matches ":tcp$"`

- Explanation

  `Filter ini menampilkan paket TCP yang tidak memiliki payload (tanpa data aplikasi, hanya header TCP). Ini termasuk paket SYN, ACK, FIN, dsb.`

- Output result

![1.4](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal1/1.4.jpg?raw=true)


## Task 2

- Flag

  `JARKOM25{N1c3_0ne_b4nggg_CMWFNALRARyuMM13yyktreblylhzqgsepdhn yc3r4t0ps4756138537511110132_fe65f2a424142787e0ade6018bdc2d38}`

> a. Berapa banyak packet berhasil yang berbasis murni TCP dan memiliki flag [ACK]?

> _a. How many packets succeed that are pure TCP based and have [ACK] flag?_

**Answer:** `3209`

- Filter expression

  `tcp.len == 0 && tcp.flags.ack == 1 && !tcp.analysis.lost_segment`

- Explanation

  `Filter ini mencari paket **pure TCP** tanpa data (`tcp.len == 0`), 
  yang memiliki **ACK flag** (`tcp.flags.ack == 1`), 
  dan bukan paket hilang (`!tcp.analysis.lost_segment`).  
  Hasilnya menunjukkan ada **3209 paket berhasil** yang memenuhi kriteria tersebut.`

- Output result

  ![2.1](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-revisi-shzirley/blob/main/revisi/soal2/2.1.jpg?raw=true)

  <br>
  <br>

> b. Berapa banyak packet berhasil yang berbasis murni TCP yang hanya memiliki flag [ACK]?

> _b. How many packets succeed that are pure TCP based and have only [ACK] flag?_

**Answer:** `3172`

- Filter expression

  `tcp.len == 0 && tcp.flags == 0x10 && !tcp.analysis.flags`

- Explanation

  `Filter ini mencari paket **pure TCP** tanpa data (`tcp.len == 0`),  
  dengan **hanya flag ACK** aktif (`tcp.flags == 0x10`),  
  serta memastikan tidak ada error analisis seperti segmen hilang (`!tcp.analysis.flags`).  
  Hasilnya didapat **3172 paket berhasil** yang memenuhi kriteria tersebut.`

- Output result

  ![2.2](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-revisi-shzirley/blob/main/revisi/soal2/2.2.jpg?raw=true)

  <br>
  <br>

> c. Berapa banyak packet berhasil yang berbasis murni TCP dan memiliki flag selain hanya [ACK]?

> _c. How many packets succeed that are pure TCP based and contain flags other than just [ACK] flag?_

**Answer:** `49`

- Filter expression

  `frame.protocols matches ":tcp$" && tcp.flags != 0x10`

- Explanation

  `Filter ini menyaring paket yang berbasis **pure TCP** (`frame.protocols matches ":tcp$"`),  
  lalu hanya menghitung paket dengan **flag selain ACK saja** (`tcp.flags != 0x10`).  
  Dengan filter ini diperoleh **49 paket berhasil** yang memenuhi kriteria tersebut.`

- Output result

  ![2.3](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-revisi-shzirley/blob/main/revisi/soal2/2.3.jpg?raw=true)

  <br>
  <br>

## Task 3

- Flag

`JARKOM25{W0w_Y0uU_h4V33e_d0n3_4U4_90od_j0bB_MAPRAg0d1lk3y83Q0c6qfxvvol7nLzHfg_64J24G1e5931e0aa79b4f7805869d0c6}`

> a. Pada port berapa client telnet terbuka?

> _a. In what port is the telnet client open?_

**Answer:** `54184`

- Filter expression

  `tcp.flags.syn == 1 && tcp.dstport == 23`

- Explanation

  `Protokol Telnet menggunakan port server 23. Dari hasil analisis paket SYN yang dikirim client ke server port 23, terlihat source port client adalah 54184. Inilah port yang digunakan client untuk membuka koneksi Telnet.`

- Output result

![3.1](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal3/3.1.jpg?raw=true)

  <br>
  <br>

> b. Berapa byte file response yang dikirim dari server?

> _b. How many bytes of the response files are sent from the server?_

**Answer:** `1449`

- Explanation

  `Kita bisa lihat paket TCP dari server ke client. IP 172.16.16.102 adalah alamat server yang mengirim data, sedangkan 172.16.16.101 adalah alamat client yang menerima data. Dengan klik kanan paket dari server ke client dan pilih Follow → TCP Stream, terlihat server mengirim total 1449 bytes sebagai response file.`

- Output result

![3.2](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal3/3.2.jpg?raw=true)

  <br>
  <br>

> c. Apa username yang digunakan client telnet untuk berhubungan dengan server?

> _c. What telnet client's username is used to connect with the server?_

**Answer:** `jovyan`

- Explanation

  `Saat kita klik salah satu paket Telnet dari client ke server dan pilih Follow → TCP Stream, Wireshark menampilkan seluruh percakapan Telnet antara client dan server. Di aliran tersebut terlihat client mengirim username untuk login ke server, yaitu jovyan.`

- Output result

![3.3](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal3/3.3.jpg?raw=true)

  <br>
  <br>

> d. Apa password client telnet?

> _d. What is the telnet client's password?_

**Answer:** `123`

- Explanation

  `Dengan klik paket Telnet dari client ke server dan pilih Follow → TCP Stream, Wireshark menampilkan seluruh isi percakapan Telnet. Di aliran tersebut, setelah username (jovyan), client mengirim password untuk login ke server, yaitu 123. Dari sini kita bisa melihat langsung password yang digunakan oleh client.`

- Output result

![3.4](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal3/3.4.jpg?raw=true)

  <br>
  <br>

## Task 4

- Flag

  `JARKOM25{G0u4t__4n4Li3z3ar_GRNSPcfGB3WFUHN6BNKr9iqjgzsnmkin9bp3ys82394B5428_4l425f36a229ab5cf0ed9055cf8e1871d1}`

> a. Apa perintah pertama yang ditulis client pada koneksi telnet?

> _a. What is the first command that client wrote on telnet connection?_

**Answer:** `echo`

- Explanation
  
  `Masih pada Follow TCP Stream, dalam trafik tersebut menampilkan perintah pertama yang ditulis client pada koneksi telnet`

- Output result

![4.1](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal4/4.1.jpg?raw=true)

  <br>
  <br>

> b. Apa nama file .txt di server (ditulis bersama ekstensinya)?

> _b. What is the name of .txt file on the server (write with the extension)?_

**Answer:** `test.txt`

- Explanation

  `Masih pada Follow TCP Stream, dalam trafik tersebut menampilkan file .txt di server yang ditulis client pada koneksi telnet`

- Output result

![4.2](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal4/4,2.jpg?raw=true)

  <br>
  <br>

> c. Apa kata pertama dari frasa yang dimasukkan client ke dalam file sebelumnya?

> _c. What is the first word that the client inserted into the previous file?_

**Answer:** `Jarkom`

- Explanation

  `Masih pada Follow TCP Stream, dalam trafik tersebut menampilkan kalimat yang dimasukkan client pada koneksi telnet`

- Output result

![4.3](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal4/4.3.jpg?raw=true)

  <br>
  <br>

## Task 5

- Flag

  `JARKOM25{n41l0ng_m1lk_drUg800n_NA3NV07IY2MYRIP8CMNJD47QKRB9Acrcbbhzx4q8gloj1368V1fkf4B31_4ed9b189f0ac298d513500db3877b21}`

> a. Berapa banyak packet berbasis HTTP yang terekam pada file pcapng?

> _a. How many HTTP packets are recorded in the pcapng file?_

**Answer:** `298`

- Filter expression

  `http`

- Explanation

  `Filter ini hanya menampilkan paket yang menggunakan protokol HTTP. Setelah filter diterapkan, terlihat bahwa ada 298 paket HTTP dalam file tersebut. Artinya, terdapat 298 paket yang membawa data atau permintaan HTTP yang terekam.`

- Output result

![5.1](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal5/5.1.jpg?raw=true)

  <br>
  <br>

> b. Ada berapa HTTP packet yang berupa response?

> _b. How many response HTTP packets are recorded in the traffic?_

**Answer:** `149`

- Filter expression

  `http.response`

- Explanation

  `Dalam protokol HTTP, ada dua jenis paket utama: request (permintaan dari client ke server) dan response (jawaban dari server ke client). Untuk mengetahui jumlah paket HTTP response, kita dapat menggunakan filter http.response di Wireshark. Filter ini hanya menampilkan paket yang berisi balasan HTTP dari server, termasuk status code dan konten yang dikirim kembali ke client. Setelah filter diterapkan, terlihat ada 149 paket HTTP response dalam file pcapng ini.`

- Output result

![5.2](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal5/5.2.jpg?raw=true)

  <br>
  <br>

> c. Ada berapa paket berbasis HTTP yang berhasil?

> _c. How many HTTP packets that succeed?_

**Answer:** `296`

- Filter expression

  `http&&!tcp.analysis.lost_segment`

- Explanation

  `Paket HTTP bisa mengalami kehilangan segmen TCP karena masalah jaringan, sehingga tidak semua paket yang terekam benar-benar “berhasil” dikirim atau diterima. Untuk mengetahui paket HTTP yang berhasil, kita bisa menggunakan filter http && !tcp.analysis.lost_segment di Wireshark.`

`http → menampilkan semua paket HTTP.`

`!tcp.analysis.lost_segment → mengecualikan paket yang mengalami segmen TCP hilang.`

`Setelah filter ini diterapkan, terlihat ada 296 paket HTTP yang berhasil, artinya paket-paket ini dikirim dan diterima tanpa ada kehilangan segmen TCP.`

- Output result

![5.3](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal5/5.3.jpg?raw=true)

  <br>
  <br>

> d. Apa alamat IP dari client HTTP yang tersambung lokal dengan mesin lain?

> _d. What is the client HTTP IP Address in connection with other local machine?_

**Answer:** `172.16.16.101`

- Filter expression

  `http.request&&ip.src`

- Explanation

  `Dalam komunikasi HTTP, client adalah perangkat yang mengirim request ke server. Untuk mengetahui alamat IP client yang berkomunikasi dengan mesin lokal lainnya, kita bisa menggunakan filter http.request && ip.src di Wireshark.`

`http.request → menampilkan paket HTTP yang berupa permintaan dari client.`

`ip.src → menampilkan alamat IP sumber dari paket tersebut.`

`Setelah filter diterapkan, terlihat bahwa alamat IP client HTTP yang terhubung ke mesin lokal lain adalah 172.16.16.101. Ini menunjukkan perangkat tersebut lah yang memulai koneksi HTTP ke server lokal.`

- Output result

![5.4](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal5/5.4.jpg?raw=true)

  <br>
  <br>

## Task 6

- Flag

`JARKOM25{br0mb44rdin0u_Cr0ccc0c0c0cdi1l10l_8516194008awaesa9lk49swmzqsh1n0buJNA3OUH6GSLW2I3_f93e0c0417fffe83edd1470c8e2e9b6a}`

> a. Apakah kamu menemukan fake flag? Tuliskan seluruhnya!

> _a. Did you find the fake flag? Write it whole!_

**Answer:** `FakeFlag{JarkomGampang}`

- Filter expression

  `http.request.uri contains "flag.txt"`

- Explanation

  `  Dengan menggunakan filter tersebut, kita menyaring request HTTP yang mengakses file **flag.txt**.  
  Setelah menemukan paket terkait, dilakukan **Follow TCP Stream** untuk melihat keseluruhan isi komunikasi.  
  Dari stream inilah terlihat bahwa server memberikan respon berupa **fake flag**, yaitu  
  **`FakeFlag{JarkomGampang}`**.`

- Output result

  ![6.1](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-revisi-shzirley/blob/main/revisi/soal6/6.a.jpg?raw=true)

  <br>
  <br>

> b. Tuliskan username dan password yang tertulis! (format username:password)

> _b. Write the written username and password! (format username:password)_

**Answer:** `Rey:123`

- Filter expression

  `http.request.uri contains "passwd.txt"`

- Explanation

  `Dengan filter tersebut, kita menyaring request HTTP yang mengakses file **passwd.txt**.  
  Setelah paket ditemukan, dilakukan **Follow TCP Stream** untuk melihat isi respon server.  
  Dari hasil analisis, terlihat kredensial yang tersimpan adalah **`Rey:123`** dengan format username:password.`

- Output result

  ![6.2](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-revisi-shzirley/blob/main/revisi/soal6/6.b.jpg?raw=true)

  <br>
  <br>

## Task 7

- Flag

  `JARKOM25{tr4Ll4lel0_tr1l1ll_otuebm3gxjk3b0s0sH800Z69T1K1ZQE0_cd293d03198838eaa4e237dd69fe46d3}`

> Apa nama gambar yang direquest oleh client? (tulis dengan ekstensinya)

> _What is the image that is being requested by the client? (write with its extension)_

**Answer:** `donalbebek.jpg`

- Filter expression

  `http.request&&http.request.uri contains ".jpg"`

- Explanation

  `Untuk mengetahui nama gambar yang diminta oleh client dalam komunikasi HTTP, kita dapat menggunakan filter http.request && http.request.uri contains ".jpg" di Wireshark. `

`http.request → menampilkan paket permintaan HTTP dari client ke server.`

`http.request.uri contains ".jpg" → memfilter hanya permintaan yang mengandung file gambar dengan ekstensi .jpg.`

`Setelah filter diterapkan, kita bisa melihat kolom Request URI di Wireshark untuk mengetahui nama file gambar lengkap beserta ekstensi yang diminta oleh client. Nama file inilah yang menjadi jawaban dari pertanyaan ini.`

- Output result

![7](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal7/7.jpg?raw=true)

  <br>
  <br>

## Task 8

- Flag

`JARKOM25{y0u_4r3_s0_G00d_1n_F0r3nsic_EZ96XAYQG3N7YUXIM038SYQBSQH6GTx45y4n6i91cslLvi4dLbx5dwnsvaa8_659b9f2234f458bb75c36bde3a797be6}`

> a. Berapa banyak packet berbasis FTP yang terekam pada file pcapng? (with the data)

> _a. How many FTP packets are recorded in the pcapng file? (with the data)_

**Answer:** `81`

- Filter expression

  `(ftp || ftp-data)&& tcp.len > 0`

- Explanation

  `File pcapng menyimpan rekaman paket jaringan, termasuk protokol FTP (File Transfer Protocol). Untuk menghitung jumlah paket FTP yang terekam beserta data yang dikirim, kita menggunakan filter:`
  
  `ftp → menampilkan paket kontrol FTP (misal perintah seperti USER, PASS, LIST).`
  
  `ftp-data → menampilkan paket data FTP (isi file yang dikirim/diterima).`
  
  `tcp.len > 0 → memastikan hanya paket yang mengandung data TCP yang dihitung, sehingga paket kosong atau ACK saja tidak termasuk.`
  
  `Setelah filter diterapkan di Wireshark, terlihat bahwa ada 81 paket FTP yang terekam, yang mencakup paket kontrol maupun paket data`

- Output result

![8.1](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal8/8.1.jpg?raw=true)

  <br>
  <br>

> b. Apa username dan password client di koneksi FTP? (tulis dalam format username:password)

> _b. What is the client's username and password in FTP connection? (write in following format username:password)_

**Answer:** `rey:password123lingangu`

- Filter expression

  `ftp.request.command == "USER" || ftp.request.command == "PASS"`

- Explanation

  `Dalam protokol FTP, client perlu melakukan login ke server menggunakan username dan password. Paket login dikirim sebagai perintah FTP:`

  `USER → berisi username yang dikirim client ke server.`
  
  `PASS → berisi password yang dikirim client ke server.`
  
  `Dengan menggunakan filter ftp.request.command == "USER" || ftp.request.command == "PASS" di Wireshark, kita dapat menampilkan paket yang membawa informasi login. Dari hasil analisis, terlihat bahwa username adalah rey dan password adalah password123lingangu.`

- Output result

![8.2](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal8/8.2.jpg?raw=true)

  <br>
  <br>

> c. What is the client's command for showing server directory that was sent on request packet?

> _c. Apa command client untuk melihat direktori server yang dikirimkan dalam request packet?_

**Answer:** `LIST`

- Filter expression

  `ftp.request.command`

- Explanation
  
  `Dalam protokol FTP, client dapat meminta daftar isi direktori pada server menggunakan perintah khusus. Perintah ini dikirim sebagai paket request dari client ke server.`

  `ftp.request.command → filter ini menampilkan semua perintah FTP yang dikirim client dalam paket request.
  Dengan menerapkan filter ini di Wireshark dan memeriksa paket yang sesuai, terlihat bahwa perintah yang digunakan client untuk melihat direktori server adalah LIST.`
  
  `Perintah LIST biasanya menghasilkan balasan dari server berupa daftar file dan folder yang ada di direktori yang diminta.`

- Output result

![8.3](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-shzirley/blob/main/screenshots/soal8/8.3.jpg?raw=true)

  <br>
  <br>

## Task 9

- Flag

`JARKOM25{j4rk000000mmm_g4mpp4444n9999999_57300674588i41L4hkq6t17xbvb321k0ncolFV2UMY58E0YXGEJ_1e51076aa7a141cdbefa502edaf70398}`

> a. Apa alamat IP dari FTP server?

> _a. What is the FTP server IP Address?_

**Answer:** `172.16.16.101`

- Filter expression

  `ftp.request.command == "LIST"`

- Explanation

  Dengan filter tersebut, kita menampilkan paket FTP yang berisi perintah **LIST** dari client ke server.  
  Dari paket tersebut dapat dilihat alamat **destination IP** yang menjadi tujuan koneksi FTP.  
  Hasil analisis menunjukkan alamat IP server FTP adalah **172.16.16.101**

- Output result

  ![9.1](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-revisi-shzirley/blob/main/revisi/soal9/9.a.jpg?raw=true)

  <br>
  <br>

> b. Berapa banyak file yang ada dalam direktori FTP server?

> _b. How many files are there inside the FTP server directory?_

**Answer:** `7`

- Filter expression

  `tcp.port == 53525`

- Explanation

  Filter ini digunakan untuk menampilkan komunikasi data pada port **53525**,  
  yaitu port data transfer yang dipakai FTP server ketika merespon perintah **LIST**.  
  Dari hasil analisis paket pada port tersebut, terlihat ada **7 nama file** yang ditampilkan,  
  sehingga jumlah file dalam direktori FTP server adalah **7**.

- Output result

  ![9.2](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-revisi-shzirley/blob/main/revisi/soal9/9.b.jpg?raw=true)

  <br>
  <br>

> c. Apa nama dari file yang digunakan dalam page.html? (tulis lengkap namanya beserta ekstensinya dan dipisahkan dengan koma ',')

> _c. What are the filenames used in the page.html? (write the filebames with their extensions and separate them with comma ',')_

**Answer:** `pokijan.jpg,research_center.jpg`

- Filter expression

  `tcp.port == 37007`

- Explanation

  Filter ini digunakan untuk menampilkan komunikasi data pada port **37007**,  
  yaitu port data transfer FTP ketika client mengunduh file **page.html**.  
  Dengan membuka isi transfer menggunakan **Follow TCP Stream**, terlihat bahwa  
  file **page.html** mereferensikan dua file gambar, yaitu **pokijan.jpg** dan **research_center.jpg**.  
  Sehingga nama file yang digunakan adalah **pokijan.jpg,research_center.jpg**.

- Output result

  ![9.3](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-revisi-shzirley/blob/main/revisi/soal9/9.c.jpg?raw=true)

  <br>
  <br>

## Task 10

- Flag

`JARKOM25{f1nisssshs55s5s533s_l1n333ee333E3_9700174051291070zgmvdgl2345215123123IJRTPTNLOBIENW2_61bc99e0ceb648219c8c20841cc6833b}`

> a. Apa nama file yang mengandung string terencode?

> _a. What is the filename that contains encoded string?_

**Answer:** `secret.txt`

- Filter expression

  `ftp.request.command == "RETR"`

- Explanation

  Filter ini menampilkan perintah **RETR** pada protokol FTP (permintaan unduh file).  
  Kita cek satu per satu file yang diunduh, lalu menemukan request untuk **secret.txt**.  
  Data transfer file tersebut berjalan melalui **port 44189**.  
  Dengan melakukan **Follow TCP Stream** pada koneksi di port ini, terlihat bahwa isi file **secret.txt**  
  berupa **string terencode**.

- Output result

  ![10.1](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-revisi-shzirley/blob/main/revisi/soal10/10.a.jpg?raw=true)

  <br>
  <br>

> b. Apa nama file hasil copy file sebelumnya?

> _b. What is the filename of the previous file copy?_

**Answer:** `secret1.txt`

- Filter expression

  `ftp.request.command == "STOR"`

- Explanation

  Filter ini digunakan untuk menampilkan perintah **STOR** pada protokol FTP,  
  yaitu perintah yang dipakai client untuk **mengunggah (menyimpan) file** ke server.  
  Dari hasil analisis paket, terlihat bahwa file yang diunggah adalah **secret1.txt**,  
  yang merupakan hasil copy dari file sebelumnya (**secret.txt**).

- Output result

  ![10.2](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-revisi-shzirley/blob/main/revisi/soal10/10.b.jpg?raw=true)

  <br>
  <br>

> c. What is the decoded string from the previous file?

> _c. Apa decoded string dari file tersebut?_

**Answer:** `Pada suatu hari Rey bertemu dengan Nailong the Milk Dragon. Ketika bertemu, Rey mengajarkan Nailong apa itu Jaringan Komputer. Nailong pun senang karena ternyata Jaringan Komputer itu gampang.`

- Filter expression

  `tcp.port == 44189`

- Explanation

  Filter ini digunakan untuk menampilkan data transfer file **secret.txt** melalui port **44189**.  
  Dengan melakukan **Follow TCP Stream**, terlihat isi file berupa **string yang terencode**.  
  Setelah dilakukan proses decoding, string tersebut terbaca menjadi:  

  *"Pada suatu hari Rey bertemu dengan Nailong the Milk Dragon. Ketika bertemu, Rey mengajarkan Nailong apa itu Jaringan Komputer. Nailong pun senang karena ternyata Jaringan Komputer itu gampang."*

- Output result

  ![10.3](https://github.com/Praktikum-NETICS-2025/jarkom-modul-1-revisi-shzirley/blob/main/revisi/soal10/10.c.jpg?raw=true)

  <br>
  <br>

## Summary
Dalam praktikum ini, Wireshark digunakan untuk menganalisis lalu lintas jaringan dengan berbagai filter.  
Fitur yang paling sering dipakai adalah **Follow TCP Stream**, yang berfungsi merekonstruksi komunikasi TCP antara client dan server.  

Manfaat utamanya antara lain:  
- Melihat isi file yang ditransfer (flag.txt, passwd.txt, secret.txt, dsb).  
- Menemukan fake flag maupun real flag.  
- Mengidentifikasi username dan password.  
- Menganalisis data terencode dan hasil decoding.  

Dengan demikian, praktikum ini menunjukkan pentingnya Wireshark dalam memahami protokol jaringan serta bagaimana data dapat dianalisis secara detail.

## Problems
Skill issue aja, tapi saya niat belajar kok <3

aku cinta jarkom :3
