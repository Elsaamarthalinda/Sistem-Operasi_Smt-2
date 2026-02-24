# Laporan pertemuan 2 sistem operasi

<h4>Nama : Elsa Marthalinda<h4>
<h4>NIM : 254107020204
<h4>Kelas : TI-1G<h4>

## Praktikum 2.1 - Identifikasi CPU dan Memori
1. <img src="Screenshot 2026-02-22 063603.png" width="100%">
2. <img src="Screenshot 2026-02-19 085940.png" width="100%">
3. <img src="Screenshot 2026-02-21 145224.png" width="100%">

### Pertanyaan Latihan 2.1
1. Jumlah CPU(s), core/thread
2. Total RAM
3. Total swap. Jelaskan perbedaan RAM vs swap dalam 2-3 kalimat.

### Jawaban Latihan 2.1
1. 4 CPU (Socket), 2 Core dan 2 Threads
2. Total RAM sistem adalah 1.7Gi (sekitar 1,82 GB)
3. Total swap adalah 1.0Gi (sekitar 1,07 GB)
    RAM (Random Access) adalah memori utama yang sangat cepat untuk menyimpan data aplikasi yang sedang berjalan, namun kapasitasnya terbatas. Sedangkan swap adalah area di hard disk yang digunakan sebagai "cadangan" ketika RAM sudah penuh, namun kecepatannya jauh lebih lambat karena harus mengakses penyimpanan fisik.

## Praktikum 2.2 - Identifikasi Perangkat PCI/USB dan Driver
1. <img src="Screenshot 2026-02-21 145435.png" width="100%">
2. <img src="Screenshot 2026-02-21 145638.png" width="100%">
3. <img src="Screenshot 2026-02-21 145733.png" width="100%"> 
4. <img src="Screenshot 2026-02-21 145811.png" width="100%">
5. <img src="Screenshot 2026-02-21 145859.png" width="100%">

### Pertanyaan Latihan 2.2
1. Temukan 1 perangkat PCI(misal NIC)
2. Tuliskan: Vendor Device ID(angka hekadesimal)
3. Nama drive/modul kernel
4. Deskripsi singkat fungsinya.

### Jawaban Latihan 2.2
1. Vendor ID: 8086
2. Device ID: 100e
3. Nama Drive/Modul kernel: e1000
4. Perangkat ini berfungsi sebagai antarmuka jaringan (Network Interface Card) yang memungkinkan sistem Linux untuk terhubung, mengirim dan menerima data melalui jaringan atau internet.

## Praktikum 2.3 - Identifikasi Storage dan Filesystem
1. <img src="Screenshot 2026-02-22 064627.png" width="100%">
2. <img src="Screenshot 2026-02-22 064828.png" width="100%">
3. <img src="Screenshot 2026-02-22 064952.png" width="100%">

## Praktikum 2.4 - Melihat Modul Aktif dan Informasinya
1. <img src="Screenshot 2026-02-22 070654.png" width="100%">
2. <img src="Screenshot 2026-02-22 070750.png" width="100%">
3. <img src="Screenshot 2026-02-22 070855.png" width="100%">
4. <img src="Screenshot 2026-02-22 071645.png" width="100%">
5. <img src="Screenshot 2026-02-22 072101.png" width="100%">

## Praktikum 2.5 - Konfigurasi Auto-load dan Blacklist
1. <img src="Screenshot 2026-02-22 072300.png" width="100%">
2. <img src="Screenshot 2026-02-22 072822.png" width="100%">

## Praktikum 2.6 - Mengenali Block vs Character Device
1. <img src="Screenshot 2026-02-21 164359.png" width="100%"> 
2. <img src="Screenshot 2026-02-21 164830.png" width="100%">
3. <img src="Screenshot 2026-02-21 164944.png" width="100%">

### Pertanyaan Latihan 2.3
1. Dari output ls -, jelaskan perbedaan penanda file untuk block device dan character device. (Hint: karakter pertama pada permission string).

### Jawaban Latihan 2.3
1. Block Device ditandai dengan huruf b, bahwa perangkat jenis ini membaca dan menulis data dalam bentuk blok-blok berukuran tetap.
2. Character Device ditandai dengan huruf c, perangkat ini mengirim atau menerima data satu per satu karakter secara berurutan.

## Praktikum 2.7 - Melihat Informasi udev
1. <img src="Screenshot 2026-02-22 073050.png" width="100%">

## Praktikum 2.8 - Membuat Workspace Praktikum
1. <img src="Screenshot 2026-02-22 155528.png" width="100%">
2. <img src="Screenshot 2026-02-22 155726.png" width="100%">
3. <img src="Screenshot 2026-02-22 160134.png" width="100%">
4. <img src="Screenshot 2026-02-22 160238.png" width="100%">

## Praktikum 2.9 - Pencarian Pola dengan grep
1. <img src="Screenshot 2026-02-22 160614.png" width="100%">
2. <img src="Screenshot 2026-02-22 160728.png" width="100%">
3. <img src="Screenshot 2026-02-22 160916.png" width="100%">
4. <img src="Screenshot 2026-02-22 161045.png" width="100%">

### Pertanyaan Latihan 2.4
1. Gunakan grep untuk menampilkan hanya baris yang mengandung INFO atau WARN dari data.log. (Hint: gunakan grep -E dengan pola alternatif).

### Jawaban Latihan 2.4
1. Perintah ini bertugas membaca seluruh isi file data.log, kemudian menyaring dan hanya menampilkan baris yang sesuai dengan kriteria yang diminta yaitu INFO dan WARN.
    <img src="Screenshot 2026-02-21 190136.png" width="100%">

## Praktikum 2.10 - Substitusi dengan sead (Aman di File Latihan) 
1. <img src="Screenshot 2026-02-22 161512.png" width="100%">
2. <img src="Screenshot 2026-02-22 162424.png" width="100%">
3. <img src="Screenshot 2026-02-22 162638.png" width="100%">
4. <img src="Screenshot 2026-02-22 162908.png" width="100%">

## Praktikum 2.11 - Ekstraksi Kolom dengan awk
1. <img src="Screenshot 2026-02-22 163007.png" width="100%">
2. <img src="Screenshot 2026-02-22 163220.png" width="100%">
3. <img src="Screenshot 2026-02-22 171615.png" width="100%">

## Praktikum 2.12 - Melihat Proses dengan ps
1. <img src="Screenshot 2026-02-22 172022.png" width="100%">
2. <img src="Screenshot 2026-02-22 172143.png" width="100%">

## Praktikum 2.13 - Monitoring Real-time dengan top
1. <img src="Screenshot 2026-02-22 172508.png" width="100%">

## Praktikum 2.14 - Menghentikan Proses dengan kill
1. <img src="Screenshot 2026-02-22 172835.png" width="100%">
2. <img src="Screenshot 2026-02-22 174238.png" width="100%">
3. <img src="Screenshot 2026-02-22 185522.png" width="100%">
4. <img src="Screenshot 2026-02-22 185957.png" width="100%">

## Praktikum 2.15 - Cek Disk, Load, dan Service
1. <img src="Screenshot 2026-02-22 190435.png" width="100%">
2. <img src="Screenshot 2026-02-22 190801.png" width="100%">
3. <img src="Screenshot 2026-02-22 190859.png" width="100%">
4. <img src="Screenshot 2026-02-22 191014.png" width="100%">
5. <img src="Screenshot 2026-02-22 191557.png" width="100%">

## Praktikum 2.16 - Monitoring Port dan Koneksi (Nnetwork Basics)
1. <img src="Screenshot 2026-02-22 191919.png" width="100%">
2. <img src="Screenshot 2026-02-22 192006.png" width="100%">
3. <img src="Screenshot 2026-02-22 192129.png" width="100%">

### Pertanyaan Latihan 2.5
1. Pilih satu port yang listening dari output ss -tulpn(misal port 22)
2. Lalu tuliskan service/proses yang membukanya.
3. Jelaskan kegunaan port tersebut secara singkat.

### Jawaban Latihan 2.5
1. Port yang listening: Port 53 (TCP) pada alamat 127.0.0.53 dan 127.0.0.54
2. Service/proses yang membukanya: systemd-resolve (Process ID/PID: 528)
3. Kegunaan port 53: Port standar yang digunakan untuk layanan DNS. Proses systemd-resolve berfungsi sebagai local DNS resolver yang bertugas menerjemahkan nama domain web menjadi deretan IP angkka, sehingga komputer bisa mengenali dan menyambungkan koneksi ke server tujuan.
    <img src="Screenshot 2026-02-21 194154.png" width="100%">

## 1.9 Latihan

### Pertanyaan Latihan 2.A
1. Jalankan lspci -nnk. Pilih 1 perangkat PCI dan tuliskan: nama perangkat
2. ID vendor:device
3. Kernel driver in use.

### Jawaban Latihan 2.A
1. Nama perangkat: Intel Corporation 82801AA AC'97 Audio Controller
2. ID Vendor:Device: 8086:2415
3. Kernel driver in use: snd_intel18x0
    <img src="Screenshot 2026-02-21 200454.png" width="100%">

### Pertanyaan Latihan 2.B
1. Tentukan device root filesystem dengan findmnt /. Lalu cocokkan dengan lsblk -f dan tuliskan tipe filesystem serta UUID-nya.

### Jawaban Latihan 2.B
1. Device Root Filesystem: /dev/mapper/ubuntu--vg-ubuntu--lv
2. Tipe Filesystem: ext4
3. UUID: 82c88ecc-521c-4fea-95c3-b33b9df68a9f
    <img src="Screenshot 2026-02-21 213118.png" width="100%">

### Pertanyaan Latihan 2.C
1. Buat file server.log berisi minimal 10 baris dengan variasi kata: INFO, WARN, ERROR. Gunakan grep untuk menampilkan hanya baris ERROR.

### Jawaban Latihan 2.C
1. Saat dieksekusi, grep memindai file server.log dan hanya menampilkan baris yang mengandung kata "ERROR". Baris lainnya (seperti INFO dan WARN) diabaikan.
    <img src="Screenshot 2026-02-21 221409.png" width="100%">

### Pertanyaan Latihan 2.D
1. Gunakan sed untuk mengganti semua kata server menjadi node pada file latihan. Tunjukkan sebelum dan sesudah.

### Jawaban Latihan 2.D
1. Sebelum: <img src="Screenshot 2026-02-21 223538.png" width="100%">
2. Sesudah: <img src="Screenshot 2026-02-21 223924.png" width="100%">

### Pertanyaan Latihan 2.E
1. Gunakan df -h lalu awk untuk menampilkan file system yang penggunaan disk di atas 70%.

### Jawaban Latihan 2.E
1. Tidak ada satupun partisi atau disk di server Ubuntu yang penggunaanya melebihi 70%. Karena yang muncul hanya baris judul (Filesystem, Size, Used, Avail, Use%, dan Mounted on).
    <img src="Screenshot 2026-02-22 192809.png" width="100%">

### Pertanyaan Latihan 2.F
1. Jalankan sleep 600 &. Temukan PID-nya dengan ps. Hentikan dengan SIGTERM.
2. Jelaskan beda SIGTERM vs SIGKILL.

### Jawaban Latihan 2.F
1. Nomor_PID: 1273.
2. SIGTERM: Meminta proses berhenti secara baik (graceful).
    SIGKILL: Memaksa proses berhenti segera (force).
    <img src="Screenshot 2026-02-22 194116.png" width="100%">

### Pertanyaan Latihan 2.G
1. Gunakan systemctl –failed. Jika tidak ada yang gagal, pilih satu service aktif (misal ssh) dan tampilkan status serta 30 baris log terakhirnya.

### Jawaban Latihan 2.G
1. <img src="Screenshot 2026-02-22 195956.png" width="100%">
    <img src="Screenshot 2026-02-22 200245.png" width="100%">
    