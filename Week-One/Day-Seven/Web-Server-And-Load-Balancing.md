# Task

## Apa itu Web Server?

Menurut Saya, Web server merupakan suatu software yang memberikan layanan berbasis data dan berfungsi untuk menerima request dari client berupa http atau htpps yang dusebut juga web browser kemudian memberikan respond dengan memberikan halaman web yang secara umum berupa halaman html.

# Step 1 - Install VM 

1.Kita install Virtual Machine kita terlebih dahulu, disini saya mencoba menggunakan multipass, kita bisa menggunakan link `https://multipass.run/` ini untuk melihat langkah-langkahnya.

![image](https://user-images.githubusercontent.com/99697182/171821089-da74b4fd-ab8b-459a-b548-134e5e93fa07.png)

2.setelahnya, kita cek apakah snap sundah ikut terinstall atau belum dengan perintah `snap --version`

![image](https://user-images.githubusercontent.com/99697182/171866311-7128ba6e-82ed-4fa5-b779-6b53f22fcdbf.png)

3.Kemudian Kita buat servernya menggunakan perintah `multipass launch --name foo`

![image](https://user-images.githubusercontent.com/99697182/171837821-a2a2e59a-ce50-41e8-8725-d96abdd04cfd.png)

4.Kemudian, Karena saya ngga serek sama nama servernya, saya mau delete dan kemudian membuat server nya kembali :

![image](https://user-images.githubusercontent.com/99697182/171865162-53b78eac-599c-4ef8-93cf-89bf64eef0ab.png)

5.kita bisa menghapus status delete nya dengan perintah `multipass purge`

![image](https://user-images.githubusercontent.com/99697182/171867215-559042f0-ede7-4ef1-ba2c-a76c06830607.png)

6.disini saya membuat 3 buah server, : 1.Server gateaway, 2 dan 3 nya untuk server aplikasi :

![image](https://user-images.githubusercontent.com/99697182/171868652-3a2b2e0d-058e-43c1-9726-f244fc7b4d3c.png)



# Step 2 - Instalasi NGinx Web Server Di Gateaway Server

1.Langkah awal saya akan masuk pada server gateway dengan menggunakan perintah

```
multipass shell gateaway-server
```

![image](https://user-images.githubusercontent.com/99697182/171869947-11d89641-70d5-475a-9683-ac4d82fb8496.png)

2. Kita update dulu, agar environment kita selalu ter up-to-date 

```
sudo apt update; sudo apt upgrade
```

![image](https://user-images.githubusercontent.com/99697182/171870904-81aff732-1084-43f8-8538-1bac4d4c31b7.png)

3. Kemudian kita install Nginx

```
sudo apt install nginx
```

![image](https://user-images.githubusercontent.com/99697182/171872028-3c4b699c-29d0-4915-be2f-3abbd9031001.png)

4.Untuk cek status nginx gunakan perintah

```
sudo systemctl status nginx
```
![image](https://user-images.githubusercontent.com/99697182/171872870-d89a8ac4-260b-4ed8-b4f2-34a869907532.png)

5. Mengecek versi nginx menggunakan

```
nginx -v
```

![image](https://user-images.githubusercontent.com/99697182/171873151-0c80a7eb-b7e0-47fd-84e4-ea363f4b3de4.png)

6. kemudian saya akan cek pada web browser

![image](https://user-images.githubusercontent.com/99697182/171873498-dff4b92d-c262-4374-9fec-c027dc616fd4.png)

Keterangan : Apabila muncul seperti gambar diatas artinya web server nginx sudah berhasil diinstall dan sudah berjalan

# Step 3 - Instalasi NodeJs pada server 1 & 2



















# Step 2 - 

# Ketentuan

Jalankan 1 aplikasi yang sama pada 2 buah server

Buatlah sebuah konfigurasi reverse proxy pada server gateway (nginx)

Buatlah sebuah konfigurasi load balancing pada server gateway (nginx)

Aplikasi dapat di akses menggunakan domain virtual dan otomatis load balance ke 2 aplikasi tersebut

