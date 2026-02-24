# Laporan pertemuan 1 sistem operasi

<h4>Nama : Elsa Marthalinda<h4>
<h4>NIM : 254107020204
<h4>Kelas : TI-1G<h4>

## 1.10. Latihan
### 1.10.1 Latihan Konseptual
### Pertanyaan Latihan 1.1
1. Jelaskan 5 fungsi utama sistem operasi dengan contoh konkret dari minimal 2 OS berbeda (Windows, macOS, atau Linux).

### Jawaban Latihan 1.1
1. **Manajemen Proses:** Mengatur program yang berjalan bersamaan (multitasking) agar tidak saling bentrok.
* **Windows:** Menggunakan Task Manager untuk memantau dan menutup proses.
* **Linux:** Menggunakan perintah top atau htop di terminal.
2. **Manajemen Memori:** Membagi ruang RAM untuk aplikasi aktif dan menyediakan memori cadangan jika RAM penuh.
* **Windows:** Menggunakan pagefile.sys sebagai memori virtual.
* **Linux:** Menggunakan ruang khusus yang disebut partisi Swap.
3. **Manajemen Sistem File:** Mengatur cara file dan folder disimpan, dinamai, dan dicari di penyimpanan (HDD/SSD).
* **Windows:** Menggunakan format NTFS yang diakses lewat File Explorer.
* **macOS:** Menggunakan format APFS yang sangat optimal untuk SSD.
4. **Manajemen Perangkat Keras (I/O):** Menghubungkan hardware (keyboard, printer, webcam) ke perangkat lunak menggunakan driver.
* **Windows:** Device Manager otomatis mencari driver saat perangkat baru dicolokkan.
* **Linux:** *Kernel modules* langsung membaca flashdisk saat dicolokkan agar isinya bisa diakses.
5. **Keamanan & Kontrol Akses:** Melindungi data dan memastikan hanya pengguna sah yang bisa mengubah sistem penting.
* **Windows:** Memunculkan konfirmasi User Account Control (UAC) saat instalasi aplikasi.
* **macOS/Linux:** Mewajibkan perintah sudo dan memasukkan password administrator.

### Pertanyaan Latihan 1.2
1. Kapan sebaiknya menggunakan Windows vs Linux vs macOS? Analisis berdasarkan use case: gaming, development, server, creative work, dan enterprise.

### Jawaban Latihan 1.2
1. * Gaming (Windows): Pemenang mutlak karena kompatibilitas game nyaris 100% dan dukungan kartu grafis yang paling optimal.
* Development (Linux & macOS): Lingkungan terbaik untuk menulis kode (seperti Java) dan mengelola version control (seperti Git). Terminal berbasis Unix pada keduanya sangat tangguh. Windows bisa menjadi alternatif lewat fitur WSL.
* Server (Linux): Standar utama industri backend. Sangat ringan, aman, dan mendominasi infrastruktur cloud serta arsitektur jaringan secara global.
* Creative Work (macOS): Pilihan utama pembuat konten dan desainer berkat akurasi warna layar dan optimasi perangkat lunak eksklusif (seperti Final Cut Pro). Windows menempel ketat untuk kebutuhan 3D rendering.
* Enterprise (Windows): Menguasai komputer perkantoran karena sistem manajemen Microsoft memudahkan divisi IT mengatur kebijakan keamanan ribuan PC secara terpusat.

### 1.10.2 Latihan Praktikal
### Pertanyaan Latihan 1.3
1. Download Ubuntu Server ISO dari website resmi
2. Create VM baru di VirtualBox (RAM: 2GB, Disk: 25GB)
3. Install dengan automatic partitioning (guided)
4. Buat user account dengan password yang kuat
5. Reboot dan login ke sistem
6. Dokumentasikan proses instalasi dengan screenshot key steps

### Jawaban Latihan 1.3
1. <img src="273c2b23-55b4-4a94-84b6-a500452eab82.jpeg" width="100%">
2. <img src="Screenshot (156).png" width="100%">
4. <img src="Screenshot 2026-02-24 200320.png" width="100%">

### Pertanyaan Latihan 1.4
1. Update package list: sudo apt update
2. Upgrade packages: sudo apt upgrade
3. Install neofetch: sudo apt install neofetch
4. Jalankan neofetch dan screenshot hasilnya
5. Check disk usage dengan df -h
6. Check memory dengan free -h
7. Dokumentasikan output dari setiap command

### Jawaban Latihan 1.4
1. <img src="Screenshot 2026-02-24 201029.png" width="100%">
2. <img src="Screenshot 2026-02-24 204808.png" width="100%">
3. <img src="Screenshot 2026-02-24 205417.png" width="100%">
4. <img src="Screenshot 2026-02-24 205844.png" width="100%">
5. <img src="Screenshot 2026-02-24 205958.png" width="100%">
6. <img src="Screenshot 2026-02-24 210058.png" width="100%">

### Pertanyaan Latihan 1.5
1. Tampilkan informasi OS: cat /etc/os-release
2. Tampilkan versi kernel: uname -r
3. List partisi: lsblk
4. Check network connectivity: ping -c 4 google.com
5. Install dan jalankan htop untuk melihat resource usage
6. Buat laporan singkat tentang konfigurasi sistem Anda

### Jawaban Latihan 1.5
1. <img src="Screenshot 2026-02-24 210232.png" width="100%">
2. <img src="Screenshot 2026-02-24 210323.png" width="100%">
3. <img src="Screenshot 2026-02-24 210401.png" width="100%">
4. <img src="Screenshot 2026-02-24 210559.png" width="100%">
5. <img src="Screenshot 2026-02-24 210732.png" width="100%">
6. * OS & Kernel: Menjalankan Ubuntu 24.04.4 LTS dengan versi kernel 6.8.0-100-generic.
* Penyimpanan: Total disk 25 GB. Menggunakan sistem LVM dengan alokasi partisi utama (root) sebesar 11.5 GB dan partisi boot 2 GB.
* Jaringan: Terhubung ke internet dengan sangat stabil (Ping ke Google sukses dengan 0% packet loss dan rata-rata latency 37 ms).
* Performa (Resource): Berjalan sangat ringan dan efisien. Beban CPU di bawah 1% dan RAM hanya terpakai sekitar 200 MB dari total 2 GB.

### Latihan Refleksi
### Pertanyaan Latihan 1.6
1. Sistem operasi apa yang Anda gunakan sehari-hari? (Windows, macOS, Linux, atau lainnya)
2. Berapa lama Anda menggunakan sistem operasi tersebut?
3. Apa yang Anda sukai dari sistem operasi tersebut?
4. Apa tantangan atau masalah yang pernah Anda hadapi?
5. Apakah Anda pernah menggunakan sistem operasi lain? Bandingkan pengalaman Anda.
6. Setelah mempelajari bab ini, apakah ada sistem operasi lain yang ingin Anda coba? Mengapa?

### Jawaban Latihan 1.6
1. Saya menggunakan sistem operasi Windows sebagai OS utama saya sehari-hari.
2. Saya sudah menggunakan Windows selama lebih dari 5 tahun.
3. Saya suka pakai Windows karena tampilannya sangat mudah digunakan dan hampir semua software didukung oleh OS ini. Untuk aktivitas sehari-hari seperti mengetik tugas, membuat flowchart, atau belajar pemrograman dasar, Windows terasa sangat praktis. Selain itu, kalau kita memasang perangkat keras baru, sistemnya otomatis langsung mendeteksi dengan lancar.
4. Tantangan yang sering muncul adalah manajemen memori yang kadang membuat sistem terasa berat atau lambat (lemot) saat menjalankan banyak proses sekaligus.
5. Pernah, saya nyoba pakai macOS buat bikin simulasi topologi jaringan. Bedanya lumayan kerasa dibanding Windows. Kalau di Windows kadang suka berat pas buka aplikasi simulator, di Mac jalannya jauh lebih smooth pas geser-geser komponen kayak router atau switch. Terus, karena Terminal di Mac itu turunan Unix, dipakai buat nge-test jaringan (kayak ping atau cek routing) rasanya lebih enak dan real banget dibanding pakai CMD di Windows.
6. Saya sangat tertarik untuk belajar Linux. Alasannya karena saya minat di bidang network engineering dan pengembangan perangkat lunak. Seperti yang kita tahu, Linux adalah standar industri untuk urusan jaringan, server, dan cloud. Jadi, dengan belajar menggunakan terminal Linux serta memahami cara kerjanya, ini akan dapat mempermudah untuk menjadi fondasi karir depannya.