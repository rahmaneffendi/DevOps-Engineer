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
   
# step 1 - 

1. Pertama kita klik [link ini](https://console.idcloudhost.com/user/abdulrahmaneffendi789@gmail.com/lab) untuk masuk kedalam hal id cloud hostnya, kemudian akan tampil gambar di bawah ini :

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

Penjelasan Tambahan : 
<li>
<li>Vpc = Virtual Private CLoud, Suatu layanan yang disediakan untuk sejumlah orang tertentu aja, Biasanya diterapkan dalam suatu perusahaan yang mempunyai sejumlah data yang besar juga bisa bersifat rahasia
 
 <li>cara konek ke vpc yaitu menggunakan VPN, dan biasanya di setup oleh orang lapangan</li>

<li>karakter private cloud ini dapat di scale secara mandiri dengan pengetahuan teknis, biasanya dilakukan oleh orang lapangan dan manajemen datanya hanya bisa di akses oleh orang-orang tertentu, dan tidak perlu membayar layanan karena sudah ada secara default</li>

<li>Private Cloud</li>

<li>Public Cloud</li>

<li>floating ip : Dimana nanti server kita mempunyai 2 ip address yang bersifat public dan private</li>

   


