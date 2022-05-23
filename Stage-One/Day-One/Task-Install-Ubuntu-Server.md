# Requirements

Sebelum melakukan instalasi ubuntu server, hal pertama yang harus kita lakukan adalah menginstall tools virtual machine serta meng-unduh file ISO server terlebih dahulu.Pada materi kali ini, kita akan menggunakan tools VMware Workstation Player.

Silahkan klik link dibawah untuk meng-unduh tools yang diperlukan.

VMware Installation : https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html

akan tampil 2 option
![Img 1](Assets/2.png)
silahkan di pilih sesuai os

Ubuntu Server 20.04 : https://ubuntu.com/download/server
![Img 1](Assets/3.png)
klik 1 dulu kemudian 2

ket : menggunakan Versi 20 untuk pemula

# Installation Ubuntu Server

1.Buka Virtual machine kalian, untuk contohnya disini menggunakan VMware. Jika sudah langsung klik saja di bagian Create a new Virtual Machine.
![Img 1](Assets/4.png)

2.Jika sudah nanti akan masuk ke halaman seperti gambar dibawah. Disini kalian pilih saja di bagian installer disc image(iso). Setelah itu masuk ke bagian browser lalu cari lokasi ISO ubuntu server yang sudah kalian download sebelumnya.
![Img 1](Assets/5.png)
![Img 1](Assets/6.png)

3.Lalu tahapan selanjutnya masukan saja user dan password yang kalian inginkan.

![Img 1](Assets/7.png)

4.Tahapan selanjutnya adalah menentukan lokasi dimana Virtual machine kalian ingin disimpan.

![Img 1](Assets/8.png)

5.Setelah atur size disk yang ingin kalian gunakan. Disini sebagai contoh saya menggunakan 10GB. Disini ada 2 pilihan yaitu Store Disk as a single file dan Split virtual disk into multiple files.

Keterangan :

Store Disk as a single file maksudnya adalah disk yang kalian buat itu nantinya akan langsung terbuat 10Gb. (ini tidak disarankan untuk pengguna yang memiliki hardisk yang berkapasitas kecil).

Split virtual disk into multiple files maksudnya adalah disk yang kita pakai untuk virtual machine kita nantinya itu akan dibagi menjadi beberapa bagian. Jadi walaupun kita menggunakan disk berkapasitas 10Gb itu nanti tidak akan terpakai seluruhnya.
![Img 1](Assets/9.png)

6.Sekarang kita akan meng-customisasi hardware untuk server kita, tekan saja di bagian Customize Hardware.
![Img 1](Assets/10.png)

7.Disini ada beberapa pilihan untuk kita melakukan customisasi seperti Memory, Processors dan Network adapter.

Keterangan:

Memory berfungsi untuk penyimpanan data yang ingin kita gunakan untuk Virtual Machine yang ingin kita buat. Disini kita pilih gunakan saja defaultnya yaitu sebesar 4Gb tetapi misalkan kalian merasa kurang kalian boleh untuk menaikkannya sesuai keinginan kalian.

Processors adalah salah satu komponen penting untuk Virtual Machine yang ingin kita bangun, serta berfungsi untuk memproses data dan mengontrol sistem yang ada pada Virtual Machine kita. Disini kita menggunakan defaultnya saja yaitu sebesar 2 core.

Network adapter berfungsi untuk menghubungkan komputer ke jaringan. Untuk penjelasan lebih lanjut ada di poin berikutnya.

8.Jika sudah selesai untuk meng-setting memory dan processor, kalian bisa pergi ke bagian Network Adapter.
Keterangan:

kalau menggunakan NAT nantinya server yang kita buat ini akan mendapatkan IP yang sudah di sediakan oleh Virtual Machine kita.

Kalau Menggunakan Bridge nantinya server yang kita buat akan mendapatkan IP dari internet yang sedang kita gunakan.
![Img 1](Assets/11.png)

setelah itu klik finish
![Img 1](Assets/10.png)

lalu akan muncul tampilan ini
![Img 1](Assets/12.png)
![Img 1](Assets/13.png)

