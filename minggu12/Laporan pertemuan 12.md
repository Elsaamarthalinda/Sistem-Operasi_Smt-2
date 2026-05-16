# Laporan Pertemuan 12 Sistem Operasi

<h4>Nama : Elsa Marthalinda<h4>
<h4>NIM : 254107020204<h4>
<h4>Kelas : TI-1G<h4>

## Praktek 10.1: Amati Layanan Aktif Saat Boot
Langkah 1: Lihat semua layanan yang sedang berjalan.

<img src="Cuplikan layar 2026-05-13 120628.png" width="70%">

- Total layanan yang aktif: Terdapat 17 layanan (loaded units) yang terdaftar dalam status berjalan.
- Kriteria status: Seluruh layanan tersebut memiliki status LOAD sebagai loaded, ACTIVE sebagai active, dan SUB sebagai running.

Langkah 2: Lihat semua unit service yang ada (aktif maupun tidak).

<img src="Cuplikan layar 2026-05-13 123744.png" width="70%">

Langkah 3: Analisis waktu boot dan temukan layanan paling lambat.

<img src="Cuplikan layar 2026-05-13 123937.png" width="70%">

> Tantangan
- Identifikasi tiga layanan dengan waktu inisialisasi terlama menggunakan systemd-analyze blame. Gunakan pipeline dari Bab 3 (| sort -rh | head -3) untuk mempercepat pencariannya. Untuk setiap layanan, cari tahu fungsinya dengan systemctl cat nama-layanan. Tuliskan nama layanan, waktu inisialisasinya, dan penjelasan singkat fungsinya.
    - <img src="Cuplikan layar 2026-05-16 100320.png" width="67%">
    - snapd.seeded.service: waktu inisialiasi 791 ms, berfungsi	layanan untuk memastikan paket Snap bawaan sistem sudah terpasang dan siap digunakan saat proses booting Ubuntu.
    - snapd.service: waktu inisialisasi 701 ms, berfungsi layanan utama Snap daemon yang mengelola instalasi, pembaruan, dan menjalankan aplikasi berbasis Snap pada Ubuntu.
    - systemd-udevd.service: waktu inisialisasi 419, berfungsi layanan pengelola perangkat keras (device manager) yang mendeteksi perangkat seperti keyboard, USB, harddisk, dan membuat device file secara otomatis saat sistem berjalan.

## Praktek 10.2: Kelola Layanan SSH
Langkah 1: Periksa status SSH secara menyeluruh.

<img src="Cuplikan layar 2026-05-16 101706.png" width="70%">

Langkah 2: Lakukan restart pantau perubahannya.

<img src="Cuplikan layar 2026-05-16 101845.png" width="70%">

Langkah 3: Lihat depensasi SSH.

<img src="Cuplikan layar 2026-05-16 102024.png" width="70%">

Langkah 4: Cek semua unit yang gagal di sistem.

<img src="Cuplikan layar 2026-05-16 102620.png" width="70%">

> Tantangan
- Buat skrip Bash (referensi Bab 7) bernama cek-layanan.sh yang memeriksa status daftar layanan dari sebuah berkas teks. Berkas teks daftar-layanan.txt berisi satu nama layanan per baris (isi minimal: ssh, cron, rsyslog). Skrip membaca setiap nama layanan, memeriksa statusnya dengan systemctl is-active, lalu menulis laporan ke berkas laporan-layanan.log dengan format: [TANGGAL] nama-layanan: ACTIVE/INACTIVE. Gunakan date untuk mendapatkan tanggal.
    - <img src="Cuplikan layar 2026-05-16 105343.png" width="67%">

## Praktek 10.3: Buat Layanan Sederhana dari Skrip Bash
Langkah 1: Siapkan konten yang akan dilayani.

<img src="Cuplikan layar 2026-05-16 105636.png" width="70%">

Langkah 2: Buat skrip wrapper untuk server HTTP.

<img src="Cuplikan layar 2026-05-16 112339.png" width="70%">

Langkah 3: Buat berkas unit systemd untuk layanan ini.

<img src="Cuplikan layar 2026-05-16 111247.png" width="70%">

Langkah 4: Jalankan layanan dan verifikasi.

<img src="Cuplikan layar 2026-05-16 113333.png" width="70%">

Langkah 5: Uji fitur restart otomatis.

<img src="Cuplikan layar 2026-05-16 113752.png" width="70%">

Langkah 6: Bersihkan layanan uji setelah selesai.

<img src="Cuplikan layar 2026-05-16 115206.png" width="70%">

> Tantangan 
- Modifikasi berkas unit demo-web.service sebelum menghapusnya: tambahkan RestartSec=10s agar sistemmenunggu 10 detik sebelum mencoba restart, dan tambahkan Environment="PORT=9091" lalu ubah ExecStart agar menggunakan variabel tersebut. Aktifkan layanan dengan enable dan WantedBy=multi-user.target, lalu uji apakah layanan aktif setelah systemctl daemon-reload. Dokumentasikan perbedaan perilaku dibanding versi
sebelumnya.
    - <img src="Cuplikan layar 2026-05-16 114245.png" width="67%">
    - <img src="Cuplikan layar 2026-05-16 114646.png" width="67%">

## Praktek 10.4: Filter dan Analisis Log Layanan
Langkah 1: Lihat log SSH dari satu jam terakhir.

<img src="Cuplikan layar 2026-05-16 115436.png" width="70%">

Langkah 2: Filter log berprioritas error ke atas.

<img src="Cuplikan layar 2026-05-16 115652.png" width="70%">

Langkah 3: Ikuti log secara real-time sambil memicu aktivitas.

<img src="Cuplikan layar 2026-05-16 120753.png" width="70%">
<img src="Cuplikan layar 2026-05-16 122310.png" width="70%">

Langkah 4: Ekstrak log ke berkas untuk analisis.

<img src="Cuplikan layar 2026-05-16 123635.png" width="70%">

> Tantangan
- Ekstrak semua log dengan prioritas error (-p err) dari 24 jam terakhir untuk layanan SSH, simpan ke berkas error-ssh-24jam.txt. Gunakan pipeline dari Bab 3 untuk menghitung total jumlah baris error dengan wc -l, lalu tampilkan 10 pesan error yang paling sering muncul menggunakan sort | uniq -c | sort -rn | head -10. Tuliskan perintah lengkap yang kamu gunakan.
    - <img src="Cuplikan layar 2026-05-16 124144.png" width="67%">

## Praktek 10.5: Konfigurasi SSH Server
Langkah 1: Periksa konfigurasi SSH saat ini.

<img src="Cuplikan layar 2026-05-16 174908.png" width="70%">

Langkah 2: Buat backup dan ubah port SSH.

<img src="Cuplikan layar 2026-05-16 175744.png" width="70%">

Langkah 3: Validasi konfigurasi dan restart layanan.

<img src="Cuplikan layar 2026-05-16 180027.png" width="70%">

Langkah 4: Verifikasi port baru dengan ss.

<img src="Cuplikan layar 2026-05-16 180313.png" width="70%">

Langkah 5: Kembalikan port SSH ke 22 setelah praktek.

<img src="Cuplikan layar 2026-05-16 180554.png" width="70%">

> Tantangan
- Ubah konfigurasi SSH untuk menambahkan dua pengaturan keamanan: PermitRootLogin no (larang login root langsung) dan MaxAuthTries 3 (maksimal tiga kali percobaan). Lakukan
dengan urutan yang aman: backup, edit, validasi dengan sshd -t, reload. Verifikasi perubahan dengan grep -E "PermitRoot|MaxAuth" /etc/ssh/sshd_config. Kemudian periksa log SSH untuk memastikan tidak ada error setelah perubahan dengan journalctl -u ssh -n 20.
    - <img src="Cuplikan layar 2026-05-16 181548.png" width="67%">

## 1.7 Latihan
## Latihan 10.1 Audit Layanan dan Analisis Boot
1. Jalankan systemctl list-units –type=service –state=running dan catat semua layanan aktif. Pilih tiga layanan yang kamu kenal, periksa status masing-masing dengan systemctl status, dan jelaskan fungsinya.
    - <img src="Cuplikan layar 2026-05-16 182205.png" width="67%">
    - <img src="Cuplikan layar 2026-05-16 182402.png" width="67%">
    - ssh.service: Menyediakan akses kontrol terminal jarak jauh (remote) secara aman melalui jaringan.
    - cron.service: Menjalankan tugas atau skrip otomatis berdasarkan jadwal waktu yang ditentukan.
    - systemd-udevd.service: Mendeteksi dan mengelola perangkat keras yang terhubung ke sistem secara otomatis.
2. Jalankan systemd-analyze blame dan identifikasi lima layanan dengan waktu inisialisasi terlama. Tampilkan hasilnya menggunakan pipeline: systemd-analyze blame | head -5.
    - <img src="Cuplikan layar 2026-05-16 182749.png" width="67%">
3. Jalankan systemctl –failed dan dokumentasikan hasilnya. Jika ada layanan yang gagal, cari tahu penyebabnya dengan journalctl -u nama-layanan -n 30.
    - <img src="Cuplikan layar 2026-05-16 182909.png" width="67%">
    - Sistem Ubuntu dalam kondisi sangat sehat. dengan keterangan: "Tidak ada layanan yang gagal pada sistem."

## Latihan 10.2 Layanan Kustom dengan Restart Otomatis
1. Buat skrip Bash (referensi Bab 7) bernama monitor-disk.sh yang setiap 30 detik menuliskan penggunaan disk ke berkas log. Gunakan df -h dan date.
    - <img src="Cuplikan layar 2026-05-16 183512.png" width="67%">
2. Buat berkas unit /etc/systemd/system/monitor-disk.service untuk menjalankan skrip tersebut dengan konfigurasi: Restart=always, RestartSec=5s, dan berjalan sebagai pengguna kamu sendiri.
    - <img src="Cuplikan layar 2026-05-16 184218.png" width="67%">
3. Aktifkan dan jalankan layanan. Verifikasi dengan systemctl status dan pastikan log masuk ke journal.
    - <img src="Cuplikan layar 2026-05-16 184605.png" width="67%">
4. Simulasikan crash dengan membunuh proses secara paksa (kill -9), tunggu 10 detik, dan verifikasi bahwa layanan hidup kembali secara otomatis.
    - <img src="Cuplikan layar 2026-05-16 185221.png" width="67%">
5. Bersihkan: nonaktifkan layanan dan hapus berkas unit setelah selesai
    - <img src="Cuplikan layar 2026-05-16 185702.png" width="67%">

## Latihan 10.3 Investigasi Log dan Keamanan SSH
1. Gunakan journalctl -b -p err untuk menemukan semua error sejak boot terakhir. Simpan hasilnya ke berkas dan hitung jumlah baris dengan wc -l.
    - <img src="Cuplikan layar 2026-05-16 190714.png" width="67%">
2. Lakukan tiga perubahan keamanan pada /etc/ssh/sshd_config: tambahkan PermitRootLogin no, MaxAuthTries 3, dan LoginGraceTime 30. Ikuti alur aman: backup, edit, validasi sshd-t, reload.
    - <img src="Cuplikan layar 2026-05-16 191214.png" width="67%">
3. Setelah reload, verifikasi tiga hal: layanan masih berjalan (systemctl status ssh), port masih mendengarkan (ss -tlnp | grep ssh), dan konfigurasi baru terbaca (grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config).
    - <img src="Cuplikan layar 2026-05-16 191605.png" width="67%">
4. Kembalikan konfigurasi SSH ke kondisi semula menggunakan berkas backup.
    - <img src="Cuplikan layar 2026-05-16 192417.png" width="67%">