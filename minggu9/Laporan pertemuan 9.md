# Laporan Pertemuan 9 Sistem Operasi

<h4>Nama : Elsa Marthalinda<h4>
<h4>NIM : 254107020204<h4>
<h4>Kelas : TI-1G<h4>

## Praktikum 9.1 Script Pertama: Laporan Sistem
1. Buat workspace praktikum:

<img src="Cuplikan layar 2026-04-22 111220.png" width="75%">

2. Buat script dengan nano:

<img src="Cuplikan layar 2026-04-22 111849.png" width="75%">

3. Ketik isi berikut, simpan ( Ctrl+O Enter ), lalu keluar ( Ctrl+X ):

<img src="Cuplikan layar 2026-04-22 113219.png" width="75%">

4. Beri izin dan jalankan:

<img src="Cuplikan layar 2026-04-22 113434.png" width="75%">

## Latihan 9.1
Modifikasi laporan-sistem.sh agar menyimpan output ke file
laporan-YYYY-MM-DD.txt sekaligus menampilkannya di terminal. Petunjuk: gunakan tee yang sudah dipelajari di bab sebelumnya.

<img src="Cuplikan layar 2026-04-22 114307.png" width="75%">

<img src="Cuplikan layar 2026-04-22 114844.png" width="75%">

## Praktikum 9.2 Script Info Sistem dengan Argumen
1. Buat script:

<img src="Cuplikan layar 2026-04-22 123847.png" width="75%">

2. Ketik isi berikut:

<img src="Cuplikan layar 2026-04-22 130947.png" width="75%">

3. Simpan, beri izin, uji dengan berbagai kombinasi argumen:

<img src="Cuplikan layar 2026-04-22 131729.png" width="75%">

## Latihan 9.2
Buat script kalkulator.sh yang menerima tiga argumen: <angka1> <operator> <angka2> dengan operator +, -, *, atau /. Contoh: ./kalkulator.sh 20 + 5 menghasilkan 25. Gunakan case untuk memilih operasi, dan validasi jika argumen tidak lengkap.

<img src="Cuplikan layar 2026-04-22 134650.png" width="75%">

<img src="Cuplikan layar 2026-04-22 135307.png" width="75%">

## Praktikum 9.3 Script Grading dan Menu Interaktif
1. Buat script grading (menggunakan if dan for):
2. Isi grading-batch.sh:

<img src="Cuplikan layar 2026-04-22 143823.png" width="75%">

3. Simpan, beri izin, dan jalankan:

<img src="Cuplikan layar 2026-04-22 143555.png" width="75%">

4. Buat script menu interaktif (while + case):

<img src="Cuplikan layar 2026-04-22 144835.png" width="75%">

5. Isi menu-sistem.sh:

<img src="Cuplikan layar 2026-04-22 152756.png" width="75%">

6. Beri izin dan jalankan, coba setiap opsi:

<img src="Cuplikan layar 2026-04-22 152945.png" width="75%">

## Latihan 9.3
Tambahkan ke script grading-batch.sh sebuah ringkasan di bagian bawah yang menampilkan: jumlah mahasiswa per grade (A, B, C, D, E) menggunakan perulangan for kedua yang mengiterasi array MAHASISWA.

<img src="Cuplikan layar 2026-04-22 160226.png" width="75%">
<img src="Cuplikan layar 2026-04-22 161031.png" width="75%">

## Praktikum 9.4 Library Fungsi Validasi
1. Buat file library:
2. Isi lib-validasi.sh:

<img src="Cuplikan layar 2026-04-22 184949.png" width="75%">

3. Buat script yang menggunakan library:

<img src="Cuplikan layar 2026-04-22 185131.png" width="75%">

4. Isi pakai-library.sh:

<img src="Cuplikan layar 2026-04-23 183043.png" width="75%">

5. Beri izin dan uji semua skenario:

<img src="Cuplikan layar 2026-04-23 183358.png" width="75%">

## Latihan 9.4
Tambahkan fungsi konfirmasi() ke lib-validasi.sh. Fungsi ini menampilkan pertanyaan, membaca input Y/N dari user, mengembalikan 0 jika Y dan 1 jika N. Buat script demo yang memanggil fungsi ini sebelum menghapus sebuah file.

<img src="Cuplikan layar 2026-04-23 200812.png" width="75%">

<img src="Cuplikan layar 2026-04-23 200327.png" width="75%">

<img src="Cuplikan layar 2026-04-23 195142.png" width="75%">

## Praktikum 9.5 Script Backup dengan Opsi
1. Buat script:

<img src="Cuplikan layar 2026-04-23 201111.png" width="75%">

2. Isi backup-data.sh:

<img src="Cuplikan layar 2026-04-23 205111.png" width="75%">

3. Beri izin dan uji:

<img src="Cuplikan layar 2026-04-23 211233.png" width="75%">

## Praktikum 9.6 Debugging Script
1. Buat script untuk dianalisis:

<img src="Cuplikan layar 2026-04-26 223302.png" width="75%">

2. Isi debug-latihan.sh:

<img src="Cuplikan layar 2026-04-26 224216.png" width="75%">

3. Cek sintaks, lalu jalankan dengan tracing:

<img src="Cuplikan layar 2026-04-26 224538.png" width="75%">

## Latihan 9.6
Script debug-latihan.sh tidak menangani direktori yang tidak ada. Perbaiki dengan menambahkan:
- set -e di baris kedua
- Pengecekan -d "$DIREKTORI" sebelum memanggil du
- Pesan error yang informatif jika direktori tidak ditemukan.
- Uji dengan direktori yang tidak ada.

<img src="Cuplikan layar 2026-04-26 231440.png" width="75%">
<img src="Cuplikan layar 2026-04-26 231247.png" width="75%">

## Tugas 1 Script Absensi Kelas
Konteks: instruktur mencatat kehadiran mahasiswa dari command line.
Instruksi:
1. Buat script absensi.sh yang:
- Menerima argumen nama mahasiswa dan status (hadir/izin/alpha)
- Menyimpan entri ke absensi-YYYY-MM-DD.txt dengan format [HH:MM] NAMA - STATUS
- Opsi -r: tampilkan rekapitulasi (jumlah per status)
- Opsi -h: tampilkan bantuan
2. Rekam minimal 5 entri dan tampilkan rekapitulasinya.
Konsep wajib: variabel, parameter posisional, getopts, if, for, fungsi, dan redirection ke file.

<img src="Cuplikan layar 2026-04-27 083005.png" width="75%">
<img src="Cuplikan layar 2026-04-27 084647.png" width="75%">

## Tugas 2 Script Health Check Sistem
Konteks: administrator membuat pemeriksaan kondisi server sebelum maintenance.
Instruksi:
1. Buat script healthcheck.sh menggunakan template profesional dari bagian Best Practices.
2. Script menampilkan: tanggal/waktu, hostname, uptime, penggunaan CPU, memori, dan disk untuk setiap filesystem yang terpasang.
3. Jika penggunaan disk mana pun melebihi 80%, tampilkan peringatan.
4. Simpan hasil ke healthcheck-YYYY-MM-DD.log dan tampilkan ke terminal sekaligus menggunakan tee.
5. Opsi -t <persen> mengubah batas peringatan disk (default 80).
Konsep wajib: set -euo pipefail, trap, getopts, fungsi dengan local, for, if, dan tee.

<img src="Cuplikan layar 2026-04-28 133300.png" width="75%">
<img src="Cuplikan layar 2026-04-28 133402.png" width="75%">
<img src="Cuplikan layar 2026-04-28 133122.png" width="75%">
