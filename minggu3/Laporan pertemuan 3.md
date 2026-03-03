# Laporan pertemuan 3 sistem operasi

<h4>Nama : lsa Marthalinda<h4>
<h4>NIM : 254107020204<h4>
<h4>Kelas : TI-1G<h4>

## 1.11. Latihan
### Latihan 3.1
Buat scrip yang:
1. Menampilkan daftar 10 file terbesar di direktori /var/log/
2. Menyimpan hasilnya ke file large-logs.txt
3. Menampilkan output juga di terminal menggunakan tee
4. Menangani error dengan redirect ke error.log
### Jawaban
<img src="Screenshot 2026-03-03 192725.png" width="100%">

### Latihan 3.2
Buat pipeline yang:
1. Membaca /etc/passwd
2. Mengekstrak username (kolom pertama)
3. Mengurutkan alfabetis
4. Menyimpan ke file sorted-users.txt: Gunakan cut, sort, dan operator redirect.
### Jawaban
<img src="Screenshot 2026-03-03 194956.png" width="100%">

### Latihan 3.3
Tulis script monitoring yang:
1. Mencatat penggunaan CPU dan memory setiap 5 detik
2. Menyimpan log dengan timestamp
3. Berjalan selama 1 menit (12 iterasi)
4. Output ditampilkan di terminal DAN disimpan ke file
### Jawaban
<img src="Screenshot 2026-03-03 200436.png" width="100%">

### Latihan 3.4
Buat perintah yang:
1. Mencari semua file .conf di sistem
2. Membuang pesan "Permission denied"
3. Menghitung jumlah file yang ditemukan
4. Menyimpan daftar path lengkap ke file
### Jawaban
<img src="Screenshot 2026-03-03 201136.png" width="100%">
<img src="Screenshot 2026-03-03 205331.png" width="100%">

### Latihan 3.5
Implementasikan script backup yang:
1. Menggunakan tar untuk backup direktori
2. Menampilkan progress dengan tee
3. Mencatat stdout ke backup-success.log
4. Mencatat stderr ke backup-error.log
5. Menambahkan timestamp di setiap log entry
### Jawaban
<img src="Screenshot 2026-03-03 212657.png" width="100%">
<img src="Screenshot 2026-03-03 221558.png" width="100%">