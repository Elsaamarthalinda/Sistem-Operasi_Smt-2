# Laporan pertemuan 4 sistem operasi

<h4>Nama : Elsa Marthalinda<h4>
<h4>NIM : 254107020204<h4>
<h4>Kelas : TI-1G<h4>

## Tugas Pendahuluan
Jawablah pertanyaan-pertanyaan di bawah ini :
1. Apa yang dimaksud perintah-perintah direktory : pwd, cd, mkdir, rmdir.
2. Apa yang dimaksud perintah-perintah manipulasi file : cp, mv dan rm (sertakan format yang digunakan)
3. Jelaskan perbedaan Symbolic link menggunakan hard link (direct) dan soft link (indirect).
4. Tuliskan maksud perintah-perintah : file, find, which, locate dan grep.
### Jawaban
1. Perintah-perintah direktori: 
- **pw:** Digunakan untuk menampilkan jalur (path) lengkap dari direktori tempat file berada saat ini.
- **cd:** Digunakan untuk berpindah dari satu direktori ke direktori lain.
- **mkdir:** Digunakan untuk membuat direktori atau folder baru.
- **rmdir:** Digunakan untuk menghapus direktori yang kosong. Jika direktori ada isinya, perintah ini biasanya akan menolak penghapusan.
2. perintah-perintah manipulasi file:
- **cp:** Menyalin (copy) file atau direktori. Format: cp [sumber tujuan]
- **mv:** Memindahkan atau mengubah nama (rename) file/direktori. Format: mv [sumber tujuan]
- **rm:*** Menghapus (remove) file atau direktori secara permanen. Format: rm [nama_file]
3. Perbedaan Hard Link dan Soft Link:
- **Hard Link (Direct):** Membuat salinan yang merujuk langsung ke Inode (identitas fisik file di disk) yang sama.
> Jika file asli dihapus, file hard link tetap bisa diakses karena data fisiknya masih ada. Hanya bisa dilakukan pada file di dalam sistem file (filesystem) yang sama.
- **Soft Link/Symbolic Link (Indirect):** Berfungsi seperti shortcut di Windows. Ia merujuk pada nama jalur file asli, bukan datanya langsung.
> Jika file asli dihapus, soft link akan "rusak" (broken) dan tidak bisa dibuka. Bisa merujuk ke direktori dan bisa melintasi sistem file yang berbeda.
4. Maksud perintah-perintah:
- **file:** Cek tipe/format file (teks, gambar, atau data biner).
- **find:** Cari file secara real-time berdasarkan kriteria(nama, ukuran, dll).
- **which:** Cari lokasi file executable dari sebuah perintah sistem.
- **locate:** Cari file dengan cepat menggunakan database indeks.
- **grep:** Cari baris teks atau kata tertentu di dalam file.

## Latihan
1. Cobalah urutan perintah berikut :
- $ cd
- $ pwd
- $ ls –al
- $ cd .
- $ pwd
- $ cd ..
- $ pwd
- $ ls -al
- $ cd ..
- $ pwd
- $ ls -al
- $ cd /etc
- $ ls –al | more
- $ cat passwd
- $ cd –
- $ pwd
<img src="Screenshot 2026-03-10 120321.png" width="100%">
<img src="Screenshot 2026-03-10 121010.png" width="70%">
<img src="Screenshot 2026-03-10 121154.png" width="70%">
<img src="Screenshot 2026-03-10 121408.png" width="70%">
<img src="Screenshot 2026-03-10 121729.png" width="70%">
<img src="Screenshot 2026-03-10 121921.png" width="70%">

2. Lanjutkan penelusuran pohon pada sistem file menggunakan cd, ls, pwd dan cat. Telusuri direktory /bin, /usr/bin, /sbin, /tmp dan /boot.
<img src="Screenshot 2026-03-10 123011.png" width="70%">
<img src="Screenshot 2026-03-10 144518.png" width="70%">
<img src="Screenshot 2026-03-10 144839.png" width="70%">
<img src="Screenshot 2026-03-10 145928.png" width="70%">
<img src="Screenshot 2026-03-10 150604.png" width="70%">
<img src="Screenshot 2026-03-10 150742.png" width="70%">


3. Telusuri direktory /dev. Identifikasi perangkat yang tersedia. Identifikasi tty (termninal) Anda (ketik who am i); siapa pemilih tty Anda (gunakan ls –l).
<img src="Screenshot 2026-03-10 152016.png" width="70%">
- Dari hasil who am i, user elsa menggunakan terminal tty.
- Dilihat dari hasil ls -l tty, pemilik tty adalah root dengan group tty.

4. Telusuri derectory /proc. Tampilkan isi file interrupts, devices, cpuinfo, meminfo dan uptime menggunakan perintah cat. Dapatkah Anda melihat mengapa directory /proc disebut pseudo -filesystem yang memungkinkan akses ke struktur data kernel?
<img src="Screenshot 2026-03-10 151120.png" width="70%">
<img src="Screenshot 2026-03-10 151413.png" width="70%">
<img src="Screenshot 2026-03-10 151525.png" width="70%">
<img src="Screenshot 2026-03-10 152259.png" width="70%">
<img src="Screenshot 2026-03-10 152414.png" width="70%">
- Direktori /proc disebut pseudo -filesystem karena isinya buka file sungguhan di disk, tetapi informasi kernel yang dibuat secara dinamis di RAM setiap kali diakses.

5. Ubahlah direktory home ke user lain secara langsung menggunakan cd ~username.
<img src="Screenshot 2026-03-10 161956.png" width="70%">

6. Ubah kembali ke direktory home Anda.
<img src="Screenshot 2026-03-10 162200.png" width="85%">

7. Buat subdirektory work dan play.
<img src="Screenshot 2026-03-10 162422.png" width="85%">

8. Hapus subdirektory work.
<img src="Screenshot 2026-03-10 162720.png" width="85%">

9. Copy file /etc/passwd ke direktory home Anda.
<img src="Screenshot 2026-03-10 163007.png" width="75%">

10. Pindahkan ke subirectory play.
<img src="Screenshot 2026-03-10 163249.png" width="83%">

11. Ubahlah ke subdirektory play dan buat symbolic link dengan nama terminal yang menunjuk ke perangkat tty. Apa yang terjadi jika melakukan hard link ke perangkat tty?
<img src="Screenshot 2026-03-10 163614.png" width="70%">
- ln -s /dev/tty terminal > berhasil membuat symbolic link terminal > /dev/tty.
- Hard link ke perangkat tty tidak bisa dilakukan karena /dev/tty adalah character device, bukan file biasa.

12. Buatlah file bernama hello.txt yang berisi kata ”hello word”. Dapatkah Anda gunakan "cp" menggunakan "terminal" sebagai file asal untuk menghasilkan efek yang sama?
<img src="Screenshot 2026-03-10 164809.png" width="70%">
- Ya bisa, cp terminal hello.txt akan menghasilkan efek yang sama karena terminal adalah symbolic link ke /dev/tty yang membaca input dari keyboard, namun hasilnya tergantung input yang diketik user.

13. Copy hello.txt ke terminal. Apa yang terjadi?
<img src="Screenshot 2026-03-10 165234.png" width="75%">
- cp terminal hello.txt akan menghasilkan efek yang sama karena terminal adalah symbolic link ke /dev/tty yang membaca input dari keyboard, namun hasilnya tergantung input yang diketik user.

14. Masih direktory home, copy keseluruhan direktory play ke direktory bernama work menggunakan symbolic link.
<img src="Screenshot 2026-03-10 165604.png" width="70%">

15. Hapus direktory work dan isinya dengan satu perintah.
<img src="Screenshot 2026-03-10 165858.png" width="70%">

## Laporan Resmi
1. Analisa hasil percobaan yang Anda lakukan.
- a. Analisa setiap hasil tampilannya.
- Sistem operasi Linux memiliki struktur direktori yang hirarkis dan terpusat. Analisa terhadap perintah cd dan pwd membuktikan bahwa semua direktori bermuara pada satu titik yaitu Root (/). Penggunaan simbol khusus seperti . (direktori saat ini), .. (satu tingkat di atas), dan ~ (home) sangat efisien untuk berpindah-pindah posisi dalam struktur pohon file yang kompleks.
- b. Pada Percobaan 1 point 3 buatlah pohon dari struktur file dan direktori
/ (Root)

├── bin (Binary perintah umum)

├── boot (File pemuatan sistem/kernel)

├── dev (File perangkat/hardware)

├── etc (Konfigurasi sistem)

├── home (Direktori personal user)

│   └── elsa (Home user saat ini)

├── lib (Library sistem)

├── proc (Informasi kernel & proses)

├── sbin (Binary sistem/admin)

├── tmp (File sementara)

└── usr (Aplikasi user)

- c. Bila terdapat pesan error, jelaskan penyebabnya.
- Error pada ln (Hard Link ke tty): Jika mencoba membuat hard link ke /dev/tty, sistem akan memunculkan error "Operation not permitted" atau "Invalid cross-device link"
    Penyebab: Hard link hanya bisa dibuat untuk file biasa (reguler) dalam sistem file yang sama. /dev/tty adalah file perangkat (character device), sehingga hanya bisa dihubungkan menggunakan Symbolic Link (Soft Link).
- Error pada cd ~username: Jika username yang dituju tidak ada, akan muncul "No such file or directory".
    Penyebab: Direktori home untuk user tersebut tidak ditemukan dalam /home.
    
2. Kerjakan latihan diatas dan analisa hasil tampilannya.
- Dari latihan 1 sampai 15, dapat disimpulkan bahwa manipulasi file di Linux sangat bergantung pada pemahaman jalur (path). Penggunaan opsi -r pada perintah rm sangat krusial saat menghapus direktori yang memiliki isi (seperti pada latihan no. 15), karena tanpa opsi tersebut, perintah akan gagal. Interaksi dengan terminal (tty) melalui perintah cp menunjukkan fleksibilitas Linux dalam menangani I/O (Input/Output).

3. Berikan kesimpulan dari praktikum ini.
- Dari praktikum ini dapat disimpulkan bahwa sistem operasi Linux memiliki struktur file berbentuk hierarki. Pengguna dapat mengelola file dan direktori menggunakan berbagai perintah dasar seperti cd, ls, pwd, cp, mv, mkdir, dan rm untuk navigasi dan manajemen file.