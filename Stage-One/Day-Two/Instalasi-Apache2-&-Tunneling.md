# Instalasi Apache2 Dan Tunneling

## Step 1 - Setting IP

1. langkah awal mensetting IP terlebih dahulu jika menggunakan jaringan bridge, maka kita gunakan IP dalam satu network dengan cara berikut:

```
sudo nano /etc/netplan/00-installer-config.yaml
```
Akan muncul sebagai berikut lalu ubah IP nya
![Img 1](assets/2.png)

2. Setelah selesai men-setting IP maka kita coba gunakan perintah `ping google.com` untuk mengetes koneksi dan jika berhasil maka akan muncul seperti gambar berikut

![Img 1](assets/3.png)

# Step 2

## Apache2 Installation

1. Untuk mengecek IP yang sudah kita ubah tadi kita akan coba dengan remote server. Caranya masuk ke terminal lokal kalian dan masukan perintah berikut 

```
ssh rahman3@192.168.132.254
```
Untuk rahman3 kalian ganti dengan username Ubuntu Server kalian sendiri, jika ssh berhasil maka akan muncul seperti gambar berikut:

![Img 1](assets/4.png)

Selanjutnya tahapan pertama yang harus kita lakukan pada saat sedang berada di dalam server yaitu melakukan update serta upgrade terlebih dahulu gunanya untuk menjaga agar system kita tetap up-to-date.

Untuk melakukan update dan upgrade, kalian bisa menggunakan perintah di bawah ini.

```
sudo apt update; sudo apt upgrade
```

![Img 1](assets/5.png)

Selanjutnya kita akan coba untuk menginstall aplikasi Apache2.

Kalian bisa gunakan perintah di bawah ini.

```
sudo apt install apache2
```
Lalu nanti akan muncul notifikasi Do you want to continue? [Y/n] kalian ketik saja Y. Jika sudah maka instalasi akan berjalan.

![Img 1](assets/6.png)

Jika instalasi sudah selesai kita bisa cek dengan menggunakan perintah dibawah ini.

```
sudo systemctl status apache2
```

![Img 1](assets/7.png)

Sekarang coba buka browser kalian, lalu masukkan IP dari server kalian.

![Img 1](assets/8.png)
