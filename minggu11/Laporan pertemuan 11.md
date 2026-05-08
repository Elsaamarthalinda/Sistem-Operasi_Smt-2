# Laporan Pertemuan 11 Sistem Operasi

<h4>Nama : Elsa Marthalinda<h4>
<h4>NIM : 254107020204<h4>
<h4>Kelas : TI-1G<h4>

## Praktikum 11.1 — Permissions
Langkah 1: Buat direktori kerja dan dua file uji.

<img src="Cuplikan layar 2026-05-06 143840.png" width="70%">

Langkah 2: Jadikan secret.txt privat hanya untuk owner.

<img src="Cuplikan layar 2026-05-06 144012.png" width="70%">

Langkah 3: Jadikan myscript.sh dapat dijalankan.

<img src="Cuplikan layar 2026-05-06 144154.png" width="70%">

Langkah 4: Buat direktori bersama dan amati efek SGID sederhana.

<img src="Cuplikan layar 2026-05-06 144324.png" width="70%">

Langkah 5: Uji efek umask pada file baru.

<img src="Cuplikan layar 2026-05-06 144517.png" width="70%">

> Analisis
1. Mengapa secret.txt tidak dapat dibaca oleh group dan others setelah chmod 600?
    - Karena perintah chmod 600 mengatur permission file sehingga hanya pemilik (owner) yang memiliki hak akses, yaitu baca (read) dan tulis (write). Sementara itu, group dan others tidak diberikan hak akses sama sekali. Secara numerik, angka 6 berarti read (4) + write (2), sedangkan 0 berarti tidak ada izin. Jadi mereka tidak bisa membaca, menulis, maupun mengeksekusi file tersebut.
2. Apa perbedaan arti 600 dan 755 terhadap file yang diuji?
    - Permission 600 berarti hanya owner yang memiliki hak baca dan tulis.
    - Permission 755 memberikan hak akses penuh (read, write, execute) kepada owner, tetapi hanya read dan execute kepada group dan others.
3. Setelah umask 027, permission apa yang dihasilkan untuk file baru, dan mengapa bukan 777?
    - Ketika mengatur umask 027 dan membuat file baru (testfile-027), hak akses yang dihasilkan adalah 640. Permission tidak menjadi 777 karena sistem secara default tidak memberikan izin eksekusi pada file biasa demi keamanan. Execute hanya diberikan jika memang diperlukan (misalnya melalui chmod seperti pada myscript.sh).

> Tantangan
- Ubah owner atau group salah satu file uji ke akun atau group lain yang tersedia di sistem, kemudian jelaskan
perubahan output ls -l sebelum dan sesudahnya.
    - <img src="Cuplikan layar 2026-05-06 151003.png" width="67%">
    - Perubahan ls -l sebelum: Sebelum dilakukan perubahan, file secret.txt dimiliki oleh user elsa dan group elsa, yang terlihat pada output ls -l
    - Perubahan ls -l sesudah: Setelah perubahan, output ls -l menunjukkan perbedaan pada kolom group. Yaitu group diubah menjadi sudo.

## Praktikum 11.2 — ACL
Langkah 1: Siapkan file dan lihat permission standar tanpa ACL tambahan.

<img src="Cuplikan layar 2026-05-06 174810.png" width="70%">

Langkah 2: Beri akses baca ke satu user tertentu tanpa mengubah owner atau group

<img src="Cuplikan layar 2026-05-06 175704.png" width="70%">

Langkah 3: Buat direktori bersama yang mewariskan ACL ke file baru.

<img src="Cuplikan layar 2026-05-06 180508.png" width="70%">

> Analisis
1. Mengapa getfacl confidential.txt awalnya tidak menampilkan user tertentu
    - Sistem hanya mencatat hak akses untuk pemilik (owner), grup pemilik, dan pengguna lain secara umum. Dan karena belum ada instruksi khusus yang diberikan melalui perintah setfacl, daftar entitas yang memiliki akses hanya terbatas pada apa yang dikelola oleh chmod standar.
2. Setelah setfacl -m u:userA:r confidential.txt, apa perbedaan output ls -l dan getfacl?
    - Output ls -l: Muncul tanda plus (+) di akhir deretan izin akses yang merupakan tanda indikator bahwa file tersebut memiliki ACL aktif.
    - Output getfacl: Menampilkan rincian yang jauh lebih spesifik. Muncul baris baru yaitu user:userA:r--, yang secara eksplisit menunjukkan bahwa userA memiliki hak baca.
3. Mengapa file inherited.txt mewarisi ACL dari direktori shared?
    - Sistem Linux dirancang agar setiap file atau sub-direktori baru yang dibuat di dalam direktori dengan Default ACL akan secara otomatis mengadopsi aturan izin tersebut tanpa perlu dikonfigurasi ulang secara manual.
> Tantangan
- Tambahkan satu ACL lagi agar group readonly-group hanya dapat membaca confidential.txt. Setelah itu, hapus ACL untuk userA dan verifikasi hasil akhirnya dengan getfacl.
    - <img src="Cuplikan layar 2026-05-06 181656.png" width="67%">

## Praktikum 11.3A — Membuat dan Mengelola User
Latihan user management

<img src="Cuplikan layar 2026-05-06 191248.png" width="70%">
<img src="Cuplikan layar 2026-05-06 192059.png" width="70%">

Pertanyaan:
1. Apa perbedaan output id userA sebelum dan sesudah menambah group?
    - Sebelum penambahan grup: Output menampilkan uid=1001(userA), gid=1001(userA), dan groups=1001(userA),100(users).
    - Sesudah penambahan grup: Meskipun kamu tidak melampirkan screenshot perintah usermod -aG, secara teknis jika kamu menambahkan grup (misalnya readonly-group), maka pada bagian groups= akan muncul tambahan ID dan nama grup baru tersebut di akhir daftar.
2. Bagaimana status passwd -S userB berubah saat akun di-lock?
    - Status berubah menjadi L (singkatan dari Locked). Baris lengkapnya terbaca: userB L 2026-05-06 .... Dalam kondisi ini, userB tidak akan bisa login ke sistem meskipun menggunakan password yang benar.

## Praktikum 11.3B — Group Management
Latihan group management

<img src="Cuplikan layar 2026-05-06 193420.png" width="70%">

Pertanyaan:
1. Apa yang ditampilkan id userA vs groups userA?
    - id userA: Menampilkan informasi identitas secara lengkap dan teknis. Output mencakup UID (User ID), GID (Group ID utama), serta daftar seluruh groups (grup tambahan) lengkap dengan nomor ID masing-masing grup.
    - groups userA: Jika dijalankan hanya akan menampilkan daftar nama grup tempat pengguna tersebut bergabung tanpa menyertakan nomor ID (UID/GID).
2. Mengapa -a pada usermod -aG penting?
    - Karena tanpa -a, perintah usermod -G akan mengganti seluruh grup tambahan yang sudah ada dengan grup baru yang Anda masukkan. Dengan menggunakan -aG, dapat menambahkan grup baru ke dalam daftar keanggotaan pengguna tanpa menghapus grup-grup yang sudah diikuti sebelumnya.

## Praktikum 11.3C — Password Aging Policy
Latihan password policy

<img src="Cuplikan layar 2026-05-06 195312.png" width="70%">

Pertanyaan:
1. Apa arti nilai yang ditampilkan chage -l userA?
    - Last password change: Tanggal terakhir pengguna mengganti kata sandi.
    - Password expires: Tanggal di mana kata sandi akan kedaluwarsa.
    - Password inactive: Jumlah hari akun tetap nonaktif setelah kata sandi kedaluwarsa.
    - Account expires: Tanggal akun pengguna akan kedaluwarsa dan tidak bisa digunakan sama sekali.
    - Minimum/Maximum number of days: Jarak waktu minimum penggantian kata sandi dan durasi maksimum masa aktif kata sandi.
    - Number of days of warning: Jumlah hari sebelum kedaluwarsa sistem mulai memberikan peringatan kepada pengguna.
2. Bagaimana cara membuktikan userB terkunci dari output passwd -S?
    - Menggunakan passwd -S userB pada output kolom kedua setelah nama.
    - Jika muncul huruf L, berarti akun tersebut dalam status Locked (Terkunci).
    - Jika muncul huruf P, berarti akun dalam status Password set (Aktif/Dapat digunakan).
3. Kapan sebaiknya menggunakan chage -d 0 vs passwd -e?
    - chage -d 0: Digunakan saat mengelola kebijakan kedaluwarsa secara mendetail dalam satu baris perintah administratif yang lebih teknis.
    - passwd -e: Digunakan karena lebih mudah diingat (e untuk expire) dan merupakan cara cepat standar untuk menghanguskan kata sandi pengguna saat itu juga./

> Tantangan
- Buat user bernama intern yang: memiliki shell /bin/bash; menjadi anggota labgroup; dipaksa ganti password pada login pertama; password expired setelah 45 hari dengan warning 7 hari sebelumnya.
    - <img src="Cuplikan layar 2026-05-06 202137.png" width="67%">

## Praktikum 11.4 — Konfigurasi sudo
Langkah 1: Buat file konfigurasi sudo khusus untuk userA.

<img src="Cuplikan layar 2026-05-06 202643.png" width="70%">

Langkah 2: Verifikasi aturan yang aktif dan uji hasilnya.

<img src="Cuplikan layar 2026-05-06 203349.png" width="70%">

> Analisis
1. Mengapa aturan disimpan di /etc/sudoers.d//, bukan langsung di /etc/sudoers?
    - Penyimpanan aturan di `/etc/sudoers.d//` dilakukan untuk menjaga modularitas dan kerapihan sistem, sehingga konfigurasi user tidak bercampur dengan file utama `/etc/sudoers`. Metode ini juga mencegah hilangnya pengaturan saat terjadi pembaruan sistem dan meminimalisir risiko kesalahan sintaksis yang dapat mengunci akses administratif secara keseluruhan.
2. Mana perintah yang bisa dijalankan tanpa password, dan mana yang masih perlu autentikasi?
    - Tanpa Password (NOPASSWD): /usr/bin/apt update, /usr/bin/apt upgrade
    - Memerlukan Password (Autentikasi): /bin/systemctl status * (Perintah ini tidak memiliki tag NOPASSWD, sehingga secara default akan meminta password userA).
3. Informasi apa saja yang dicatat di log sudo?
    - Timestamp: Kapan perintah dijalankan (contoh: `2026-05-06T12:39:01...`)`.
    - Hostname: Nama mesin tempat perintah dijalankan (`ubuntu`).`
    - User Penginput: Siapa yang memanggil sudo (`elsa`).
    - Terminal (TTY): Jalur terminal yang digunakan (`tty1`).
    - Working Directory (PWD): Lokasi folder saat perintah dipanggil (`/home/elsa/lab-acl`).
    - Target User: Perintah dijalankan sebagai user siapa (`USER=root`).
    - Command: Perintah spesifik yang dieksekusi (`COMMAND=/usr/bin/chage -d userA`).

>Tantangan
- Tambahkan satu aturan baru agar userA boleh menjalankan /bin/systemctl restart ssh tetapi tidak boleh menjalankan reboot.
    - <img src="Cuplikan layar 2026-05-06 213004.png" width="67%">
    - <img src="Cuplikan layar 2026-05-06 213137.png" width="67%">

## Praktikum 11.5 — Disk Quota
Langkah 1: Buat image filesystem kecil dan mount dengan opsi quota.

<img src="Cuplikan layar 2026-05-06 214547.png" width="70%">

Langkah 2: Buat database quota dan aktifkan enforcement.

<img src="Cuplikan layar 2026-05-06 214946.png" width="70%">

Langkah 3: Tetapkan quota untuk user uji dan amati hasilnya.

<img src="Cuplikan layar 2026-05-06 220529.png" width="70%">

Langkah 4: Bersihkan lingkungan uji setelah selesai.

<img src="Cuplikan layar 2026-05-06 221918.png" width="70%">

> Analisis
1. Apa perbedaan soft limit dan hard limit saat quota mulai terlampaui?
    - Soft Limit: Ketika pengguna melewati batas ini, sistem masih mengizinkan penulisan data, namun pengguna akan diberikan waktu tenggang (grace time—biasanya 7 hari) untuk mengurangi penggunaan datanya.
    - Hard Limit: Jika pengguna mencapai angka ini, sistem akan segera memblokir penulisan data baru tanpa kecuali, sehingga pengguna tidak bisa menambah file lagi meskipun masa tenggang belum habis.
2. Mengapa praktikum ini memakai loopback filesystem, bukan langsung /home/?
    - Penggunaan loopback filesystem melalui file image dilakukan untuk menjamin keamanan dan isolasi sistem, sehingga eksperimen kuota tidak berisiko mengganggu stabilitas direktori `/home`. Selain itu, memberikan kemudahan praktikum karena pengelolaan sistem berkas tanpa perlu melakukan partisi ulang pada harddisk fisik.
3. Dari output repquota, informasi apa yang menunjukkan quota sudah aktif?
    - Munculnya daftar User (seperti root dan userA).
    - Terisinya nilai pada kolom Block limits dan File limits (khususnya nilai 5120 dan 10240 untuk userA).

> Tantangan
- Coba atur quota baru untuk userA dengan batas inode yang sangat kecil, kemudian jelaskan kapan pembatasan inode lebih penting daripada pembatasan block.
    - <img src="Cuplikan layar 2026-05-06 223841.png" width="67%">
    - Ketika sebuah sistem menangani ribuan hingga jutaan file berukuran sangat kecil yang dapat menghabiskan seluruh nomor indeks metadata sebelum kapasitas penyimpanan fisik penuh. Hal ini sangat penting untuk mencegah gangguan layanan pada lingkungan seperti mail server atau sistem cache web yang rentan terhadap serangan atau penumpukan file kecil yang bisa melumpuhkan operasional sistem berkas.

## 1.7 Latihan
## Latihan 11.A — Audit dan Kolaborasi
1. Temukan file SUID aktif dengan find / -perm -4000 -type f 2>/dev/null, lalu jelaskan tiga file yang Anda kenali beserta alasannya.
    - <img src="Cuplikan layar 2026-05-06 225530.png" width="67%">
    - /usr/bin/passwd: Membutuhkan hak akses SUID agar pengguna biasa dapat mengubah hash password mereka sendiri yang tersimpan di file terproteksi /etc/shadow.
    - /usr/bin/sudo: Menggunakan SUID untuk memvalidasi kredensial pengguna dan sementara waktu memberikan hak akses root guna mengeksekusi perintah administratif.
    - /usr/bin/chage: Diperlukan agar pengguna dapat melihat atau mengubah informasi kedaluwarsa password mereka sendiri, yang datanya berada di bawah kontrol sistem root.
2. Cari direktori world-writable dan tentukan mana yang valid dan mana yang berisiko.
    - <img src="Cuplikan layar 2026-05-06 225920.png" width="67%">
    - Valid (Aman): /tmp, /var/tmp, /dev/shm, /run/lock
    - Berisiko (Bahaya): /mnt/quota-test, rwxrwxrwx
3. Rancang konfigurasi permission standar dan ACL untuk direktori proyek /srv/webapp/ agar group webapp-team dapat menulis, user deploy hanya membaca, dan file baru selalu mewarisi group proyek.
    - <img src="Cuplikan layar 2026-05-06 231427.png" width="67%">

## Latihan 11.B — Kebijakan Akun dan Quota
1. Tuliskan langkah untuk membuat user intern, menambahkannya ke group labgroup, memaksa pergantian password tiap 45 hari (warning 7 hari), memberi izin sudo hanya untuk systemctl status, dan menetapkan quota ruang serta inode sederhana pada /home/.
    - <img src="Cuplikan layar 2026-05-08 222115.png" width="67%">
    - <img src="Cuplikan layar 2026-05-08 222343.png" width="67%">
    - <img src="Cuplikan layar 2026-05-08 222822.png" width="67%">
    - <img src="Cuplikan layar 2026-05-08 223325.png" width="67%">
