# Task 5

# Konfigurasi CI/CD Menggunakan Cloudflare

## Sebelumnya Apa itu Cloudflare? 

Cloudflare adalah suite keamanan dan kinerja terintegrasi untuk aplikasi berbasis web. Layanan ini Cloudflare mencoba menghilangkan masalah umum dalam jaringan internet yakni latensi dan keamanan data. Dibuat pada tahun 2007 oleh Matthew Prince, Lee Holloway dan Michelle Zatlyn, Cloudflare bertujuan menawarkan layanan keamanan ke situs web.

Cloudflare ini Mempunyai fitur CI/CD didalamnya, dimana kita bisa memanfaatkannya Untuk Konfigurasi Aplikasi Kita.

# Step 1 -Fork aplikasi 

1.Kita langsung klik link ini https://github.com/dumbwaysdev/wayshub-frontend

2. setelah kita masuk ke githubnya, kita klik saja lambang fork disebelah kanan atas 
 
![Img 1](assets/3.png)

3.Dikarenakan Saya sudah melakukan fork sebelumnya, maka otomatis langsung muncul keterngannya seperti ini:

![Img 1](assets/4.png)

dari gambar diatas, kita bisa tau kalau kita sudah berhasil melakukan `fork` terhadap repository tersebut

# Step 2 -Buat Akun Cloudflare 

Sign Up Akun Cloudflare terlebih dahaulu dengan mengisi Semua data di https://dash.cloudflare.com/sign-up

# Step 3 -Konfigurasi Dan Deployment

1. Login pada akun cloudflare, kemudian masuk ke `pages` dibagian kiri website, kemudian klik `create a project` 

![Img 1](assets/1.png)


2.Hubungkan Cloudflare kita dengan Github dengan klik `Connect Github`

![Img 1](assets/2.png)

3.kita klik all repository 

![Img 1](assets/2.1.png)

4.Jika sudah terhubung dengan github, Kemudian kita pilih repository yang sudah kita fork di step satu, yaitu repository `wayshub-frontend`

![Img 1](assets/5.png)

dari situ kita langsung klik `begin setup`

5.dari sini kita masukan nama project dan branch nya :

![Img 1](assets/6.png)

Disini kita akan konfigurasi build nya, pilih framework yang kalian gunakan di repository yang sudah kalian pilih tadi, disini saya menggunakan React maka saya memilih Create React App, kemudian di "Build Command" akan terganti sesuai rekomendasi framework yang kita pilih tadi, dan untuk build biarkan default rekomendasi

![Img 1](assets/7.png)

Pada bagian ini Root directory saya sudah benar berada di "/" dan Untuk "Environment variables" saya kosongkan karena tidak ada backend didalam project ini hanya front end saja

6.kita tunggu saja sampai deploy nya selesai

![Img 1](assets/8.png)

7.Jika proses build dan deploy berhasil maka akan muncul gambar berikut dan kita akan copy link yang telah diberikan untuk di tes

![Img 1](assets/9.png)

8.Dan setelah di tes proses deploy berhasil, web dapat diakses dengan sempurna

![Img 1](assets/10.png)

![Img 1](assets/11.png)

9.Kemudian kita cek status dari CI/CD kita tadi

![Img 1](assets/12.png)

# Step 4 -Melakukan Perubahan Isi File 

1. kita akan mengubah title `wayshub` menjadi `wayshub Abdul-Rahman`.

Pertama kita masuk ke repository yang kita fork tadi, kemudian masuk ke file `public/index.html` bagian `<title>WaysHub</title>` menjadi `<title>WaysHub - Nama Anda</title>`

![Img 1](assets/13.png)

2. Dan secara otomatis CI/CD kita akan melakukan proses build dan deploy dengan sendirinya dapat dilihat di status berikut:

![Img 1](assets/14.png)

3. Dapat dilihat Log dari proses build kita 

![Img 1](assets/15.png)

4. Dan jika proses CI/CD berhasil maka Log kita akan memberitahu kita.

5. Dapat dilihat hasil CI/CD berjalan dengan baik dan web yang tadinya title hanya "Wayshub" sekarang berubah menjadi "Wayshub - Akmal Ikhsan" yang artinya proses CI/CD kita berhasil!

![Img 1](assets/16.png)

dari yang sebelumnya hanya wayshub saja

![image](https://user-images.githubusercontent.com/99697182/172080513-3c97319e-55e6-4ca2-8885-9b3f96029a06.png)

## Selesai

## Sekian Dan Terimakasih






