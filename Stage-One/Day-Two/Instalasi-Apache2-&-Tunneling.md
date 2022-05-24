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

1. Untuk mengecek IP yang sudah kita ubah tadi kita akan coba dengan remote server. Caranya dengan perintah berikut 

```
ssh are2@192.168.134.254
```
Untuk san kalian ganti dengan username Ubuntu Server kalian sendiri, jika ssh berhasil maka akan muncul seperti gambar berikut:

![Img 1](assets/3.JPG)
