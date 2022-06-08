# Cloud Computing

![image](https://user-images.githubusercontent.com/99697182/172390865-2a05120d-c06e-461c-afbb-cf00b115a506.png)

## Apa itu Cloud Computing?

Menurut Saya Cloud Computing Merupakan Suatu pengiriman layanan yang berbeda-beda melalui internet, seperti storage, database, Network, software dls


### Mengapa Menggunakan Cloud Computing ?

<li>Perusahaan Besar bahkan startup Sudah menggunakan cloud computing</li>

<li>mempermudah pembuatan server dan management bisnis</li>

<li>menghemat biaya</li>

<li>Efisiensi Kecepatan dan keamanan datanya Bagus</li>

<li>Lokasi data centernya bisa dimanapun</li>

<li>Adanya fitur Recovery dan Backup data</li>



## Type of cloud computing

1. Onpremise , Dimana kita memenage/mengatur sendiri keseluruhan aspek server, Seperti membuat server di lokal, 
 
   Seperti : Virtual Box, Vmware dls.

2. Iaas ( infrastruktur as a Service)
 
   Seperti : AWS, IdCloud Host, Oracle Cloud, Digital Ocean, GCP(Google CLoud Platform) dls.

3. Paas (Platform as a Service)

   Seperti : cloudflare pages, Vercel, Heroku, Netlify dls.

4. Saas (Software as a Service) , Dimana Keseluruhan aspek server sudah di manage/atur oleh pemberi layanannya,
   
   Seperti : Fb, Yt, Wa, Tiktok, Photoshop dls.
   
# step 1 - Membuat Server Aplikasi Menggunakan IdCloudHost

1. Pertama kita klik [link ini](https://console.idcloudhost.com/user/abdulrahmaneffendi789@gmail.com/lab) untuk masuk kedalam hal id cloud hostnya, kemudian akan tampil gambar di bawah ini :

![image](https://user-images.githubusercontent.com/99697182/172544922-f1ca4570-5a62-48a9-95f6-a102bea7a112.png)

kemudian akan muncul tampilan ini

![image](https://user-images.githubusercontent.com/99697182/172397565-921cbff3-63b2-4626-85fe-4af58e92f141.png)

kemudian ke bagian profile di sebelah kanan, kemudian klik profile (kita akan ganti akun), kemudian klik acces user d sebelah bawah

![image](https://user-images.githubusercontent.com/99697182/172439384-1eb7e6d5-b8d2-4d72-9311-7a038a48448f.png)

kemudian klik start

![image](https://user-images.githubusercontent.com/99697182/172439535-ab10fb6a-c986-494e-b777-84c15367e8c5.png)

lalu, Disini Klik `Compute` dan klik `New` Untuk mulai membuat server nya

![image](https://user-images.githubusercontent.com/99697182/172439607-838a0160-5575-48d2-85dc-ec8f6935d24a.png)

2. kemudian kita pilih :

<li>type nya : Virtual Machine</li>

<li>Os nya : Ubuntu 20.04lts </li>

<li>Location nya : Indonesia</li>

![image](https://user-images.githubusercontent.com/99697182/172439851-30306c5f-f99a-441c-a08e-523c52de8112.png)

<li>Size nya : Disesuaikan Dengan Kebutuhan, Untuk pembelajaran disini Saya pakai `1 CPU` `1GB RAM` `20GB Disk` `50k/month`</li>

**`note : Jangan Lupa untuk ceklis Dibagian Public IP Agar server nya bisa diakses menggunakan IP Public`**

<li>Vpc : Gunakan Default saja</li>

<li>Username : Gunakan Default saja, Karena nanti kita akan membuat server lain sebagai user utama</li>

<li>pw : bebas</li>

![image](https://user-images.githubusercontent.com/99697182/172440036-1f50c515-29c1-4937-920d-4400a0f5305a.png)

<li>SSH : Boleh Digunakan Boleh tidak</li>

<li>Resource Name : Bebas, Disini saya Grouping</li>


Kemudian Klik `Create`

![image](https://user-images.githubusercontent.com/99697182/172440114-5d4702e4-16c0-4bb8-b119-921738caac96.png)

kemudian kita tunggu proses Building aplikasi servernya hingga selesai :

![image](https://user-images.githubusercontent.com/99697182/172440426-fb395d60-e669-4787-bc6a-5e389dcfc663.png)

jika sudah akan muncul seperti ini :

![image](https://user-images.githubusercontent.com/99697182/172512025-6b22234b-297b-457a-9a7d-7a16cf8fad5e.png)


________________________________________________________________________________________________________________________________________________________
Penjelasan Tambahan : 

<li>Vpc = Virtual Private CLoud, Suatu layanan yang disediakan untuk sejumlah orang tertentu aja, Biasanya diterapkan/digunakan dalam suatu perusahaan yang mempunyai sejumlah data yang besar juga bisa bersifat rahasia</li>
 
 <li>karakter private cloud ini dapat di scale secara mandiri dengan pengetahuan teknis, biasanya dilakukan oleh orang lapangan dan manajemen datanya hanya bisa di akses oleh orang-orang tertentu, dan tidak perlu membayar layanan karena sudah ada secara default, dan angka ipnya biasanya rapi</li>
 
 <li>cara konek ke vpc yaitu menggunakan VPN, dan biasanya di setup oleh orang lapangan(orang yang hidup di data center)</li>

<li>floating ip : Dimana nanti server kita mempunyai 2 ip address yang bersifat public dan private</li>

 ![image](https://user-images.githubusercontent.com/99697182/172511005-be350bdc-b54c-4121-ac5c-eede83162560.png)
  
________________________________________________________________________________________________________________________________________________________

3. Setelah pembuatan servernya selesai, kita akan mengaksesnya dari lokal kita, cara nya sama seperti sebelumnya 

```
ssh user@.....ip.....
```

![image](https://user-images.githubusercontent.com/99697182/172512766-7dada765-a8f2-4dd5-af20-c6d83a0b969b.png)

4. Setelahnya kita melakukan update

```
sudo apt update; sudo apt upgrade
```

![image](https://user-images.githubusercontent.com/99697182/172512897-f59017c8-a087-4482-9b06-94e430719667.png)

5. Kemudian Kita menambahkan user lagi, selaku user utama 

![image](https://user-images.githubusercontent.com/99697182/172513579-72a2247e-7ec1-4c3b-9765-36e21e63e0dd.png)

user : anya
pw : anya123

untuk fullname sampai other di skip aja

6. setelah nya kita akan menyalakan `pubkeyauthenticationyes` dan `passwordauntheticationyes`nya

```
sudo nano /etc/ssh/sshd_config
```

![image](https://user-images.githubusercontent.com/99697182/172513954-79776b4e-b331-46ad-b1b9-1f9bd69e3d7d.png)

![image](https://user-images.githubusercontent.com/99697182/172514186-9911015c-e788-40b3-adcf-b398ad219c52.png)

7. Kemudian Kita reload dulu, kemudian izinkan user yang sudah kita buat dapat mengakses menggunakan perintah sudo, dan kita logout dari akun kita kemudian kita masuk ke user utama yang sudah kita buat tadi 

```
sudo systemctl reload sshd
```

```
sudo usermod -aG sudo anya
```

```
logout
```

```
ssh anya@103.176.78.23
```

![image](https://user-images.githubusercontent.com/99697182/172515170-22aa6020-8d19-452f-8d47-24ae5f9d7cde.png)

8. Kemudian disini Saya akan mulai menjalankan aplikasi frontend wayshub 

Karena disini saya akan mendeploy aplikasi frontend dengan konfigurasi node js jadi terlebih dahulu saya akan menginstall NPM (Node Package Manager) dan NVM (Node Version Manager) terlebih dahulu

```
sudo apt install npm
```

![image](https://user-images.githubusercontent.com/99697182/172549100-5a591536-b98f-4622-b442-2e706dfdf373.png)

selanjutnya saya akan install engine node.js nya 

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```

```
exec bash
```

![image](https://user-images.githubusercontent.com/99697182/172551129-b18eb58c-c643-4df4-9665-850696339432.png)


```
nvm i 14
```

```
nvm -v
```

```
npm -v
```

![image](https://user-images.githubusercontent.com/99697182/172551797-f6b83956-a036-4e4f-9669-15600a39d9d1.png)

Selanjutnya cloning fork https://github.com/dumbwaysdev/wayshub-frontend menggunakan perintah :

```
git clone https://github.com/dumbwaysdev/wayshub-frontend
```

![image](https://user-images.githubusercontent.com/99697182/172552686-cd0f3d80-c8d0-418b-8297-776b78ae9697.png)

Setelah itu jalankan perintah npm i untuk node_modulesnya

```
npm i
```
![image](https://user-images.githubusercontent.com/99697182/172552928-ff8d28c0-7e9a-4e3e-b3a3-e30659d38492.png)

# Step 2 - Membuat Gateaway-Server Menggunakan Idcloudhost dan konfigurasi proxynya

1. Pertama kita Login ke akun idclouhost kita di [sini](https://console.idcloudhost.com/user/abdulrahmaneffendi789@gmail.com/lab)

![image](https://user-images.githubusercontent.com/99697182/172554380-c7eded5a-cf75-4bc0-8d39-a7740846b343.png)

2. Kemudian pilih menu Compute di kiri pojok dan pilih create new resource

Untuk type pilih app catalog dan Os nya Nginx

![image](https://user-images.githubusercontent.com/99697182/172554728-6faa9698-7efd-47b2-bd15-25926abd8ae8.png)

Kemudian isi username password dan resource name , untuk ssh ini opsional kemudian pilih create

![image](https://user-images.githubusercontent.com/99697182/172554915-ee0c9ae8-e03c-4a57-bf0f-94326ff2b167.png)

![image](https://user-images.githubusercontent.com/99697182/172555125-935edb51-749b-4432-867c-53a6dc66aedc.png)

tunggu hingga selesai

![image](https://user-images.githubusercontent.com/99697182/172555218-e8946bbe-1012-47a3-9f24-26a8f368d43f.png)











