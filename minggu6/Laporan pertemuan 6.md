# Laporan Pertemuan 6 Sistem Operasi

<h4>Nama : Elsa Marthalinda<h4>
<h4>NIM : 254107020204<h4>
<h4>Kelas : TI-1G<h4>

## Praktikum 6.1 - Melihat Proses dan Thread
1. Tampilkan semua proses yang berjalan
<img src="Screenshot 2026-04-01 143505.png" width="85%">
2. Menampilkan proses dengan thread
<img src="Screenshot 2026-04-01 143903.png" width="85%">
3. Lihat PID shell aktif dan detail proses
<img src="Screenshot 2026-04-01 144102.png" width="85%">
4. Lihat hierarki proses secara visual
<img src="Screenshot 2026-04-01 144222.png" width="85%">

## Latihan 6.1
Jalankan ps aux dan amati outputnya:
1. Berapa total proses yang berjalan? Proses apa yang memiliki PID terkecil?
- Terdapat 48 baris proses yang ditampilkan.
- PID Terkecil: 1
2. Jalankan pstree -p dan temukan proses bash Anda. Proses apa yang menjadi induk (PPID) dari bash tersebut?
- Proses: bash(986), PID (Process ID): 986.
- Proses induk berada di sebelah kiri dari proses anak dan dihubungkan langsung oleh garis.
Proses Induk: login, PPID (Parent Process ID): 784.
<img src="Screenshot 2026-04-01 144222.png" width="85%">
3. Bandingkan output ps aux dan ps aux -L. Apa perbedaan yang Anda lihat?
- Perintah ps aux menampilkan informasi di level proses sedangkan ps aux -L menampilkan informasi hingga ke level thread (utas).
- Munculnya kolom LWP (Lightweight Process): ID unik untuk setiap thread, dan NLWP (Number of Lightweight Processes): Menunjukkan berapa banyak jumlah thread yang dimiliki oleh satu proses tersebut.
- Duplikasi baris untuk proses yang sama:
- ps aux: Hanya muncul satu baris untuk satu PID (multipathd dengan PID 349).
- ps aux -L: Muncul beberapa baris dengan PID yang sama (349), tetapi memiliki nomor LWP yang berbeda-beda (365, 366, 367).

## Praktikum 6.2 — Mengamati Siklus Hidup Proses
1. Buat proses di background dan amati kondisinya:
<img src="Screenshot 2026-04-03 205751.png" width="85%">
2. Mengamati exit code dari perintah yang berhasil dan gagal:
<img src="Screenshot 2026-04-03 210123.png" width="85%">

## Latihan 6.2
1. Jalankan sleep 120 & dan amati kolom STAT pada ps aux. Kondisi apa yang ditampilkan? Mengapa proses sleep berada di kondisi tersebut?
<img src="Screenshot 2026-04-03 210350.png" width="85%">
<img src="Screenshot 2026-04-03 210752.png" width="85%">
- Pada output ps aux, kolom STAT untuk proses sleep 120 menunjukkan kode: S
- Huruf S merupakan singkatan dari Interruptible Sleep. Alasan mengapa proses tersebut berada dalam kondisi ini:
> Menunggu kejadian (Waiting for Event): Perintah sleep tidak melakukan kalkulasi aktif, pengolahan data, atau penggunaan memori yang intensif.
> Efisiensi sumber daya: Karena tidak ada yang perlu diproses oleh CPU.
> Dapat bangun kapan saja sebelum waktunya habis jika menerima sinyal dari sistem atau pengguna.
2. Jalankan beberapa perintah yang berhasil dan yang gagal, lalu catat exit code masing-masing. Pola apa yang Anda temukan?
<img src="Screenshot 2026-04-07 133921.png" width="85%">
- ls /tmp (sukses) exit code: 0
- ls /direktori-tidak-ada (gagal) exit code: 2
- Pola: Exit code 0 berarti sukses, sedangkan nilai selain 0 erarti gagal. Semakin spesifik jenis kegagalannya, semakin berbeda nilai exit codenya.

## Praktikum 6.3 — Mengatur Prioritas Proses
1. Menjalankan proses dengan nice +10:
<img src="Screenshot 2026-04-07 185600.png" width="85%">
2. Verifikasi nilai nice pada kolom NI:
<img src="Screenshot 2026-04-07 185740.png" width="85%">
3. Mengubah nice dengan renice:
<img src="Screenshot 2026-04-07 185937.png" width="85%">
4. Bersihkan proses percobaan:
<img src="Screenshot 2026-04-07 190032.png" width="85%">

## Latihan 6.3
1. Jalankan nice -n 5 sleep 200 & dan verifikasi nilai NI-nya dengan ps.
<img src="Screenshot 2026-04-07 134231.png" width="85%">
2. Ubah nilai nice menjadi 10 menggunakan renice, lalu verifikasi kembali.
<img src="Screenshot 2026-04-07 135710.png" width="85%">
- Hasil: N1 berubah menjadi 10 karena prioritas makin rendah 
3. Coba ubah nilai nice menjadi -5 tanpa sudo. Apa yang terjadi? Mengapa Linux membatasi hal ini untuk user biasa?
<img src="Screenshot 2026-04-07 140158.png" width="85%">
- Muncul error "permission denied". Karena user biasa tidak diizinkan menaikkan prioritas demi menjaga keamanan dan stabilitas sistem.

## Praktikum 6.4 — Mengirim Sinyal ke Proses
1. Membuat proses percobaan:
<img src="Screenshot 2026-04-07 190445.png" width="85%">
2. Hentikan satu proses dengan SIGTERM dan verifikasi:
<img src="Screenshot 2026-04-07 190603.png" width="85%">
3. Jeda dan lanjutkan proses dengan SIGSTOP/SIGCONT:
<img src="Screenshot 2026-04-07 190740.png" width="85%">
4. Hentikan semua proses sleep sekaligus:
<img src="Screenshot 2026-04-07 190830.png" width="85%">

## Latihan 6.4
1. Jalankan sleep 400 &, kirim SIGSTOP, dan amati perubahan kolom STAT. Kondisi apa yang muncul?
<img src="Screenshot 2026-04-07 140907.png" width="85%">
- Setelah sinyal SIGSTOP diterima, kolom STAT (Status) untuk PID 1047 akan berubah menjadi: T. Huruf T dalam sistem Linux melambangkan Stopped yang berarti proses berhenti bekerja sepenuhnya dan tidak akan mendapatkan jatah waktu CPU hingga ia menerima sinyal untuk lanjut kembali.
2. Kirim SIGCONT dan verifikasi proses kembali berjalan.
<img src="Screenshot 2026-04-07 141839.png" width="85%">
- Kolom STAT berubah dari T menjadi S, menunjukkan proses kembali berjalan dalam kondisi sleeping.
3. Hentikan proses dengan SIGTERM lalu verifikasi sudah tidak ada. Kapan Anda memilih SIGKILL daripada SIGTERM?
<img src="Screenshot 2026-04-07 143905.png" width="85%">
- SIGKILL digunakan sebagai upaya terakhir ketika suatu proses tidak merespons SIGTERM atau ketika Anda perlu menghentikan suatu proses dengan segera tanpa penundaan.

## Praktikum 6.5 — Manajemen Job Foreground dan Background
1. Jalankan tiga job di background:
<img src="Screenshot 2026-04-07 191207.png" width="85%">
2. Bawa job pertama ke foreground, jeda, lalu kembalikan ke background:
<img src="Screenshot 2026-04-07 191402.png" width="85%">
3. Hentikan semua job:
<img src="Screenshot 2026-04-07 191514.png" width="88%">

## Latihan 6.5
1. Jalankan top di foreground. Apa yang terjadi di terminal?
<img src="Screenshot 2026-04-07 163440.png" width="85%">
- top (PID 1321) milik user elsa. Ia menggunakan 0.7% CPU hanya untuk memperbarui tampilan yang sedang kamu lihat sekarang. Sebagian besar proses lainnya adalah proses internal kernel Linux (seperti kworker, kthreadd, dll) yang bertugas menjaga sistem tetap stabil.
2. Tekan Ctrl+Z dan cek statusnya dengan jobs. Kondisi apa yang ditampilkan?
- Saat menekan Ctrl + Z pada proses top, proses tersebut akan dihentikan sementara (suspend) dan dipindahkan ke background.
3. Pindahkan ke background dengan bg. Apakah top dapat berjalan dengan baik di background? Mengapa?
<img src="Screenshot 2026-04-07 164340.png" width="85%">
- Tidak, top tidak dapat berjalan dengan baik di background karena ia adalah program interaktif. Ia membutuhkan akses langsung ke terminal (TTY) untuk menampilkan output dan menerima input. Saat dipaksa berjalan di background, sistem akan mengirim sinyal SIGTTIN/SIGTTOU yang menyebabkan proses otomatis dihentikan (Stopped).
4. Kembalikan ke foreground dengan fg, lalu keluar dengan q.
- Perintah fg digunakan untuk mengembalikan proses yang sebelumnya di-background atau di-suspend ke foreground. Tombol q ditekan saat program top aktif berfungsi untuk keluar / menghentikan program top.

## Praktikum 6.6 — Pemantauan Proses
1. Temukan proses dengan penggunaan CPU dan memori tertinggi:
<img src="Screenshot 2026-04-07 171346.png" width="85%">
2. Jalankan top dan eksplorasi shortcut-nya:
<img src="Screenshot 2026-04-07 171523.png" width="85%">
3. Instal dan jalankan htop:
<img src="Screenshot 2026-04-07 171945.png" width="86%">

## Latihan 6.6
1. Gunakan ps aux –sort=%mem untuk menemukan proses yang menggunakan memori paling banyak di VM Anda. Proses apa itu?
<img src="Screenshot 2026-04-07 170140.png" width="85%">
- fwupd adalah daemon sistem di Linux yang bertugas untuk mengelola pembaruan firmware pada perangkat keras secara otomatis. Ia sering muncul sebagai pengguna memori yang cukup terlihat saat sedang melakukan pemindaian perangkat atau memeriksa ketersediaan pembaruan ke server pusat.
2. Di dalam top, tekan 1 . Apa yang berubah pada tampilan? Mengapa informasi ini berguna?
- Menekan 1 di top dapat menampilkan penggunaan CPU per core, bukan total, sehingga lebih detail dan membantu analisis performa sistem.
<img src="Screenshot 2026-04-07 170911.png" width="85%">
3. Di dalam htop, navigasikan ke proses sshd menggunakan tombol panah. Tekan F9 dan amati opsi sinyal yang tersedia.
<img src="Screenshot 2026-04-07 172323.png" width="85%">
<img src="Screenshot 2026-04-07 172454.png" width="85%">
- Setelah menekan F9, akan muncul daftar opsi sinyal seperti SIGTERM, SIGKILL, SIGSTOP, SIGCONT dll. Ini  memungkinkan penguna memiliki jenis sinyal yang akan dikirim ke proses tersebut.

## Latihan 6.A
Eksplorasi Proses Sistem
1. Jalankan ps aux –forest dan temukan proses dengan PID 1. Apa nama dan fungsi proses tersebut dalam sistem Linux modern?
<img src="Screenshot 2026-04-07 175701.png" width="85%">
- USER: root, PID: 1, COMMAND: /sbin/initv
- PID 1 adalah proses yang sangat krusial karena ia adalah "Induk dari Semua Proses" (The Mother of All Processes). Proses tersebut berfungsi manajer layanan: bertanggung jawab untuk memulai (starting), menghentikan, dan memantau semua layanan sistem (seperti jaringan, database, dan SSH).
2. Hitung berapa proses yang dimiliki oleh user root dan berapa yang dimiliki oleh user Anda. Mengapa root memiliki lebih banyak proses?
<img src="Screenshot 2026-04-07 181214.png" width="85%">
- Proses yang dimiliki oleh user root yaitu 94, sedangkan yang dimiliki user sebanyak 4.
- Jumlah proses root yang banyak bukan berarti sistem sedang berat, melainkan adalah tanda bahwa sistem operasi sedang bekerja aktif mengelola sumber daya di latar belakang agar bisa bekerja dengan lancar dan aman.
3. Temukan semua proses yang berada dalam kondisi S. Mengapa sebagian besar proses di sistem berada dalam kondisi ini?
- Tidak semua proses dalam kondisi S tidak sedang menggunakan CPU. Proses ini sedang menunggu pemicu tertentu agar bisa aktif kembali, karena banyaknya proses yang dijalankan menghabiskan 99% waktunya hanya untuk menunggu kita mengetik sesuatu. Dan antrean I/O (Input/Output) proses sering kali harus menunggu data dibaca dari hard drive atau menunggu jawaban dari server internet.

## Latihan 6.B
Simulasi Manajemen Job
1. Jalankan tiga perintah sleep dengan durasi 100, 200, dan 300 detik di background. Verifikasi ketiganya dengan jobs.
<img src="Screenshot 2026-04-07 183214.png" width="85%">
2. Bawa job kedua ke foreground, jeda dengan Ctrl+Z , lalu kembalikan ke background dengan bg.
<img src="Screenshot 2026-04-07 183421.png" width="85%">
3. Hentikan job pertama dengan kill %1. Tampilkan kembali daftar job. Berapa job yang tersisa?
<img src="Screenshot 2026-04-07 183728.png" width="85%">
- tersisa 1 job yang masih berjalan, yaitu job ke 3.

## Latihan 6.C
Prioritas dan Sinyal
1. Jalankan dua proses sleep: satu dengan nice +5 dan satu dengan nice +15. Verifikasi nilai NI keduanya dengan ps.
<img src="Screenshot 2026-04-07 184115.png" width="85%">
2. Gunakan renice untuk mengubah nice proses pertama menjadi +10. Proses mana yang kini lebih diprioritaskan scheduler?
<img src="Screenshot 2026-04-07 184311.png" width="85%">
3. Kirim SIGSTOP ke salah satu proses, verifikasi kondisi T-nya, lalu kirim SIGCONT. Akhiri semua proses percobaan dengan pkill sleep.
<img src="Screenshot 2026-04-07 184753.png" width="85%">
<img src="Screenshot 2026-04-07 185013.png" width="85%">