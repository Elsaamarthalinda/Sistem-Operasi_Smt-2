# Laporan Pertemuan 10 Sistem Operasi

<h4>Nama : Elsa Marthalinda<h4>
<h4>NIM : 254107020204<h4>
<h4>Kelas : TI-1G<h4>

## Praktikum 10.1 Melihat Penggunaan Memori
1. Jalankan free -h untuk melihat ringkasan RAM dan swap.

<img src="Cuplikan layar 2026-04-29 163304.png" width="75%">

2. Lihat detail memori dari kernel melalui /proc/meminfo.

<img src="Cuplikan layar 2026-04-29 163545.png" width="75%">

> Analisis:
1. Hitung persentase memori tersedia: available / total × 100%. Jika hasilnya di bawah 10%, sistem mulai kekurangan memori.
    - Available: 5.3 Gi, Total: 5.8 Gi
    - (5.3/5.8) x 100% = 91.3%
    - Sistem masih sangat aman karena memori yang tersedia jauh di atas batas 10%.
2. Pada baris Swap, apakah kolom used bernilai 0? Jika lebih dari 0, kernel sudah pernah memindahkan data ke disk karena RAM tidak cukup.
    - Kolom used bernilai 0, karena RAM fisik masih banyak jadi kernel belum memerlukan ruang swap.
3. Perhatikan field Cached dan Buffers di /proc/meminfo. Nilai ini sesuai dengan kolom buff/cache pada free -h.
    - Nilai di free -h (2.1 Gi) sedikit lebih besar karena kolom buff/cache pada perintah free versi terbaru juga menyertakan SReclaimable (memori kernel yang bisa diambil kembali), bukan hanya Buffers dan Cached murni. 

## Studi Kasus 10.1 Server Lambat karena Memori
1. Periksa kondisi memori secara keseluruhan.

<img src="Cuplikan layar 2026-04-29 170043.png" width="75%">

2. Pantau proses secara real-time.

<img src="Cuplikan layar 2026-05-05 224929.png" width="75%">
   
> Analisis:
1. Apakah nilai available sangat kecil (misalnya di bawah 200 MB pada server dengan RAM 2 GB)? Jika ya, server kemungkinan kekurangan memori.
    - Pada perintah free -h, kolom available menunjukkan angka 5.3Gi dari total 5.8Gi. Artinya, server masih memiliki sisa memori yang sangat lega (sekitar 91% masih tersedia), sehingga tidak ada indikasi kekurangan memori.
2. Apakah kolom used pada baris Swap lebih dari 0? Jika ya, kernel sedang menggunakan swap, yang berarti performa menurun.
    - Used = 0, performa masih optional
3. Di tampilan top, proses apa yang memiliki %MEM terbesar? Proses tersebut menjadi kandidat utama penyebab lambatnya server.
    - Di tampilan top, proses dengan PID 21667 (command: unattended-upgr) menggunakan 2.1% memori. Mengingat angkanya sangat kecil dan total RAM yang tersedia masih sangat besar, proses ini sebenarnya tidak memberatkan server sama sekali saat ini.

## Praktikum 10.2 Mengamati Aktivitas Paging
1. Jalankan vmstat dengan interval 1 detik, 5 sampel.

<img src="Cuplikan layar 2026-05-05 225701.png" width="75%">

> Analisis:
1. Amati nilai si dan so pada kelima baris. Pada sistem normal dengan RAM cukup, kedua nilai ini selalu 0.
    - Tidak ada data yang sedang dipindahkan dari RAM ke disk (swap-out) maupun sebaliknya (swap-in).
2. Jika nilai si atau so sesekali muncul lebih dari 0, artinya pernah ada aktivitas swap. Ini masih wajar jika tidak terus-menerus.
    - Tidak ada nilai yang muncul lebih dari 0.
3. Jika si dan so terus-menerus lebih dari 0, sistem dalam kondisi memory pressure serius — performa turun drastis karena akses disk jauh lebih lambat dari RAM.
    - Tidak ada tanda-tanda memory pressure.
4. Perhatikan juga kolom free (RAM kosong) dan buff (buffer) untuk memahami kondisi keseluruhan RAM saat itu.
    - Sistem berada dalam kondisi sangat sehat dengan ketersediaan RAM yang melimpah (sekitar 5,3 GiB tersedia). Tidak ditemukan adanya aktivitas swap (si dan so bernilai 0) maupun tekanan memori (memory pressure), sehingga performa server tetap optimal dan stabil.

## Praktikum 10.3 Membuat dan Mengonfigurasi Swap File
1. Buat file berukuran 512 MB sebagai calon swap.

<img src="Cuplikan layar 2026-05-05 231157.png" width="75%">

2. Atur permission file menjadi 600

<img src="Cuplikan layar 2026-05-05 233229.png" width="75%">

3. Format file sebagai area swap, lalu aktifkan.

<img src="Cuplikan layar 2026-05-05 231502.png" width="75%">

4. Verifikasi swap aktif.

<img src="Cuplikan layar 2026-05-05 231643.png" width="75%">

5.  Periksa nilai swappiness, ubah sementara, dan verifikasi perubahan.

<img src="Cuplikan layar 2026-05-05 231835.png" width="75%">

> Analisis:
1. Berapa nilai swappiness default? Apa artinya bagi perilaku kernel dalam menggunakan swap?
    - Nilai swappiness default pada sistem adalah 60. Nilai 60 berarti kernel akan mulai memindahkan proses yang jarang digunakan ke swap secara moderat untuk menjaga ruang kosong di RAM tetap tersedia untuk cache sistem.
2. Setelah diubah ke 10, konfirmasi nilai berubah pada output cat kedua. Apa dampak nilai 10 terhadap penggunaan swap dibanding nilai 60?
    - Setelah diubah ke nilai 10, sistem akan menjadi lebih selektif dalam memindahkan data ke swap. Dampaknya, sistem hanya akan menggunakan memori pada disk jika kondisi RAM benar-benar mendesak, sehingga kecepatan respons server tetap terjaga karena meminimalisir ketergantungan pada media penyimpanan yang lebih lambat.
3. Apakah entri /swapfile-week10 muncul di swapon –show? Jika tidak, pastikan Langkah 2 (chmod 600) sudah dijalankan sebelum Langkah 3.
    - Ya. Swap menandakan sudah aktif tetapi belum perlu digunakan karena RAM masih sangat longgar.

## Praktikum 10.4 Monitoring Memory
1. Ambil snapshot proses diurutkan dari penggunaan memori terbesar.

<img src="Cuplikan layar 2026-05-05 234303.png" width="75%">

2. Pantau secara real-time dengan top.

<img src="Cuplikan layar 2026-05-05 234454.png" width="75%">

> Analisis:
1. Proses apa yang berada di urutan pertama? Catat nilai %MEM dan RSS-nya.
    - Proses urutan pertama: /sbin/multipathd -d -s
    - %MEM: 0.4%
    - RSS: 27312 KB
2. Konversikan RSS dari KB ke MB (bagi 1024). Misalnya, RSS=524288 berarti proses menggunakan 512 MB RAM. Apakah wajar untuk jenis program tersebut?
    - 27312 KB / 1024 = 26.67 MB. Penggunaan memori sekitar 26 MB tergolong kecil dan efisien untuk layanan sistem yang berjalan di latar belakang.
3. Mengapa VSZ selalu lebih besar dari RSS pada proses yang sama?
    - VSZ lebih besar VSZ karena mencakup seluruh memori yang dapat diakses oleh proses, termasuk pustaka (libraries) yang dipakai bersama proses lain, memori yang di-swap ke disk, serta memori yang sudah dialokasikan tetapi belum benar-benar digunakan.
4. Apakah urutan proses di ps konsisten dengan tampilan top saat diurutkan berdasarkan %MEM?
    - Urutan proses pada kedua tampilan tersebut tidak sepenuhnya konsisten pada saat snapshot diambil Perintah top bersifat real-time dan terus memperbarui datanya setiap beberapa detik, sedangkan ps aux bersifat statis (mengambil cuplikan pada satu waktu tertentu).

## Praktikum 10.5 Script Monitor Memori
1. Pindah ke direktori dan buka nano

<img src="Cuplikan layar 2026-05-06 001830.png" width="75%">

2. Isi file monitor-memori.sh

<img src="Cuplikan layar 2026-05-06 001635.png" width="75%">

3. Menjalankan script monitor

<img src="Cuplikan layar 2026-05-06 002054.png" width="75%">

> Analisis:
1. Variabel THRESHOLD=20 menetapkan batas persentase. Perintah free | awk ’/Mem/ {printf "%d", $7/$2*100}’ mengambil kolom ke-7 (available) dibagi kolom ke-2 (total) dari baris Mem, lalu dikalikan 100 untuk menghasilkan
persentase bilangan bulat.
    - THRESHOLD=20: Variabel ini menetapkan batas minimal memori tersedia sebesar 20%. Perintah free | awk menghitung presentase memori tersedia dari available kemudian dikalikan 100 untuk mendapatkan nilai persentase dalam bentuk bilangan bulat
2. Kondisi if [ "$AVAIL" -lt "$THRESHOLD" ] bernilai benar jika persentase memori tersedia di bawah 20.
    - Evaluasi if: Kondisi if [ "$AVAIL" -lt "$THRESHOLD" ] akan bernilai benar (true) jika persentase memori yang tersedia lebih kecil dari angka yang ditentukan di variabel THRESHOLD.
3. Ubah THRESHOLD menjadi 90 dan jalankan ulang. Apa yang berubah pada output? Mengapa demikian?
    - <img src="Cuplikan layar 2026-05-06 002728.png" width="73%">

## Studi Kasus 10.2 Gagal Akses File
1. Buat direktori dan file konfigurasi contoh.

<img src="Cuplikan layar 2026-05-06 003225.png" width="75%">

2. Simulasikan permission bermasalah.

<img src="Cuplikan layar 2026-05-06 003439.png" width="75%">

3. Kembalikan permission dan verifikasi.

<img src="Cuplikan layar 2026-05-06 003559.png" width="75%">

> Analisis:
1. Mengapa cat menghasilkan Permission denied setelah chmod 000? System call apa yang gagal?
    - Karena system call openat() gagal — kernel menolak permintaan membuka file karena tidak ada bit izin baca (r).
2. Apa perbedaan pesan error Permission denied vs No such file or directory? Coba rm app.conf lalu cat app.conf untuk melihat perbedaannya.
    - Permission denied: File ada, tetapi pengguna tidak memiliki izin yang diperlukan untuk mengakses atau membacanya.
    - No such file or directory: File tidak ditemukan atau sudah dihapus.
3. Permission 644 berarti apa untuk owner, group, dan others?
    - Owner (6): Memiliki hak untuk Membaca (Read) dan Menulis/Mengedit (Write).
    - Group (4): Hanya bisa Membaca (Read) saja.
    - Others (4): Hanya bisa Membaca (Read) saja.

## Praktikum 10.6 Mengamati System Call dengan strace
1. Lihat 30 baris pertama system call dari perintah ls.

<img src="Cuplikan layar 2026-05-06 004633.png" width="75%">

2. Lihat ringkasan statistik dan bandingkan dua direktori berbeda.

<img src="Cuplikan layar 2026-05-06 004809.png" width="75%">

> Analisis:
1. Dari output Langkah 1, identifikasi minimal 4 system call berbeda. Jelaskan fungsi singkat masing-masing berdasarkan argumen yang terlihat.
    - execve: Digunakan untuk mengeksekusi program. Di kasus ini menjalankan /usr/bin/ls.
    - brk: Mengatur batas data segment (biasanya untuk alokasi memori dasar).
    - openat: Membuka file. Terlihat digunakan untuk membuka pustaka sistem.
    - mmap: Memetakan file atau perangkat ke dalam memori.
2. Dari ringkasan strace -c, system call mana yang paling 
sering dipanggil? Mengapa?
    - System call terbanyak: mmap dipanggil sebanyak 18 kali. Karena ls memerlukan banyak pustaka bersama (shared libraries) agar bisa berjalan (seperti libc, libselinux, dsb). Setiap pustaka tersebut harus dipetakan ke memori melalui beberapa panggilan mmap.
3. Apakah ada system call dengan errors lebih dari 0? Apakah itu berarti program bermasalah, ataukah bagian normal dari logika program?
    - Ya ada. access (2 error) dan statfs (2 error).
    - Bagian ini normal dari logika pemrograman. Sistem sering mengecek keberadaan file konfigurasi tertentu. Jika file tersebut tidak ada, kernel mengembalikan error ENOENT. Program sudah mengantisipasi hal ini dan akan melanjutkan ke langkah berikutnya tanpa berhenti (crash).
4. Apakah jumlah system call berbeda antara ls dan ls /etc? Faktor apa yang menyebabkan perbedaan tersebut?
    - ls: Total 75 calls (4 total error).
    - ls /etc: Total 74 calls (5 total error).
    - Perbedaan jumlah system call antara ls dan ls /etc dipengaruhi oleh variasi jumlah entri file yang menentukan frekuensi panggilan getdents64 serta perbedaan izin akses pada direktori tersebut. Selain itu, urutan pemuatan pustaka sistem dapat sedikit berubah tergantung pada lingkungan direktori yang sedang diakses.

## 1.6 Tugas Praktikum
Kerjakan seluruh tugas pada direktori berikut.

### Tugas 10.1 Audit Penggunaan Memori Sistem
<img src="Cuplikan layar 2026-05-06 013757.png" width="75%">

> Analisis:
1. Hitung persentase memori tersedia (available / total × 100%). Apakah sistem dalam kondisi normal?
    - 5.3/5.8 100% = 91.3%. Sistem berada dalam kondisi normal karena persentase memori tersedia jauh di atas 10%.
2. Mengapa buff/cache tidak dihitung sebagai memori yang terpakai dari sudut pandang ketersediaan untuk aplikasi?
    - Karena buff/cache digunakan Linux untuk menyimpan cache file dan buffer I/O agar akses data lebih cepat. Memori ini bisa dibebaskan otomatis saat aplikasi membutuhkan RAM. Artinya walaupun terlihat “used”, buff/cache sebenarnya masih bisa dipakai kembali.
3. Dari /proc/meminfo, apakah SwapTotal lebih besar dari 0? Berapa nilai wapFree?
    - Ya, nilai SwapTotal lebih besar dari 0, yaitu:
    - SwapTotal: sebesar 524284 KB.
    - SwapFree: sebesar 524284 KB.

### Tugas 10.2 Identifikasi Proses dengan Memori Tertinggi
<img src="Cuplikan layar 2026-05-06 015115.png" width="75%">

> Analisis
1. Proses apa di urutan pertama? Catat nilai %MEM dan RSS.
    - Proses pertama: /sbin/multipathd -d -s
    - %MEM: 0.4
    - RSS: 27312 KB
2. Konversikan RSS ke MB (bagi 1024). Apakah wajar?
    - 27312/1024 = 26.67MB. Nilai ini sangat wajar karena multipath adalah service sistem linux untuk manajemen storage
3. Jumlahkan %MEM dari 5 proses teratas. Berapa persen RAM yang mereka gunakan bersama?
    - 0.4+0.3+0.2+0.2+0.2= 1.3% RAM yang digunakan oleh sistem.

### Tugas 10.3 Membuat dan Memverifikasi Swap File
<img src="Cuplikan layar 2026-05-06 080729.png" width="75%">

> Analisis
1. Identifikasi kolom NAME, TYPE, SIZE, dan USED pada output swapon –show.
    - NAME: /swapfile-tugas-week10
    - TYPE: file
    - SIZE: 256M
    - USED: 0B
2. Apakah nilai total pada baris Swap di free -h bertambah 256 MB?
    - Ya, swap bertambah 256 Mib sesuai ukuran file yang dibuat.
3. Mengapa permission 600 penting? Apa risiko jika diatur ke 644?
    - Permission 600 penting karena memastikan hanya pengguna root (sistem) yang memiliki hak untuk membaca dan menulis ke file swap. Jika diatur ke 644, pengguna lain di dalam sistem dapat membaca isi file swap tersebut. Hal ini dapat menimbulkan risiko kebocoran data sensitif

### Tugas 10.4 Analisis System Call dengan strace
<img src="Cuplikan layar 2026-05-06 082902.png" width="75%">
<img src="Cuplikan layar 2026-05-06 083116.png" width="75%">

> Analisis
1. Sebutkan minimal 5 system call dari strace-summary.txt beserta fungsi singkatnya.
    - read: Membaca data dari sebuah file descriptor.
    - write: Menulis data ke sebuah file descriptor (menampilkan output ke terminal).
    - openat: Membuka file atau direktori untuk diproses oleh sistem.
    - mmap: Memetakan file atau perangkat ke dalam memori fisik (RAM) proses agar bisa diakses lebih cepat
    - close: Menutup file descriptor yang sudah tidak digunakan agar sumber daya sistem dilepaskan kembali.
2. System call mana yang paling sering dipanggil? Mengapa?
    - System call mmap dipanggil sebanyak 18 kali. Karen setiap kali program dijalankan, ia perlu memetakan berbagai pustaka sistem (shared libraries) dan mengalokasikan ruang memori untuk operasi program tersebut ke dalam RAM.
3. Apakah ada errors lebih dari 0? Apakah program tetap berjalan normal meskipun ada kegagalan tersebut?
    - Ya, terdapat 4 errors yaitu pada system call access (2 errors) dan statfs (2 errors). Program tetap dianggap berjalan dengan normal karena kesalahan tersebut telah diantisipasi dalam kode program (mekanisme error handling) sehingga tidak menyebabkan penghentian paksa atau crash.

### Tugas 10.5 Studi Kasus Diagnosa Server Lambat
<img src="Cuplikan layar 2026-05-06 124157.png" width="75%">

> Analisis
1. Jelaskan peran masing-masing fungsi: cek_memori, cek_swap, cek_proses, cek_paging, dan ringkasan. Mengapa diagnosa dipecah menjadi fungsi terpisah?
    - cek_memory: Menampilkan informasi RAM (total memori, used, free, buffer, available) menggunakan perintah free -h.
    - cek_swap: Menampilkan penggunaan swap (total swap swap yang digunakan) menggunakan free.
    - cek_proses: Mengambil daftar proses dengan penggunaan memori tertinggi (menggunakan ps aux --sort=-%mem).
    - cek_paging: Melihat apakah sistem aktif menggunakan swap secara intensif menggunakan vmstat.
    - ringkasan: Memberikan kesimpulan berdasarkan threshold tertentu.
2. Berdasarkan bagian RINGKASAN, apakah kondisi sistem normal atau kritis? Jelaskan berdasarkan nilai threshold yang digunakan script.
    - Memori tersedia (available) Anda adalah 5.3 GiB dari total 5.8 GiB, yang berarti sekitar 91%. Karena nilai 91% jauh lebih besar daripada ambang batas minimum 20%, skrip menyimpulkan kondisi memori dalam keadaan "normal".
3. Mengapa script menggunakan tee "$LAPORAN" bukan redirection biasa > "$LAPORAN"? Apa keuntungannya?
    - Perintah tee menampilkan skrip secara langsung sekaligus disimpan ke dalam file laporan.
    - Keuntungan: Jika menggunakan > "$LAPORAN", layar terminal akan kosong dan Anda tidak bisa melihat proses diagnosa secara real-time. Dengan tee, administrator bisa langsung memantau hasil diagnosa tanpa harus membuka file teksnya terlebih dahulu.
4. Dari output cek_paging, apakah ada aktivitas si atau so? Jika ada, apa implikasinya terhadap performa server?
    - Data si (swap-in) dan so (swap-out) semuanya menunjukkan angka 0.
    - Implikasi terhadap performa: Menunjukkan bahwa tidak ada aktivitas paging yang terjadi antara RAM dan disk. RAM fisik masih cukup untuk menangani semua proses berjalan, sehingga sistem tidak perlu memindahkan data ke swap (disk) yang lambat. Performa server saat ini sangat optimal karena seluruh operasi memori dilakukan langsung di RAM fisik.