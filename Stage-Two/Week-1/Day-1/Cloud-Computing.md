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

Kemudian isi username password dan resource name , untuk ssh ini opsional kemudian pilih create, untuk lokasi, saya pindah ke north jakarta, dikarenakan di pertengahan ada error

![image](https://user-images.githubusercontent.com/99697182/172554915-ee0c9ae8-e03c-4a57-bf0f-94326ff2b167.png)

![image](https://user-images.githubusercontent.com/99697182/172555125-935edb51-749b-4432-867c-53a6dc66aedc.png)

tunggu hingga selesai

![image](https://user-images.githubusercontent.com/99697182/172555218-e8946bbe-1012-47a3-9f24-26a8f368d43f.png)

jika sudah selesai, maka akan muncul ini 

![image](https://user-images.githubusercontent.com/99697182/172556402-32ee94b2-164e-4f4b-a299-2f3ca02bd42f.png)

3. Kemudian Kita akan remote server nya dari lokal kita :

```
ssh ubuntu@103.55.37.95
```
![image](https://user-images.githubusercontent.com/99697182/172556945-51d62286-1a54-4477-ac45-a23143f07956.png)

4. Kita  akan melakukan update dan upgrade pada server Gateway agar selalu terupdate 

```
sudo apt update ; sudo apt upgrade
```

![image](https://user-images.githubusercontent.com/99697182/172557303-65829e7e-3683-4c2a-b9e9-7414c2e78dc1.png)

5. Kemudian check versi nginx dengan menggunakan perintah

```
nginx -v
```

Seharusnya pada server Gateway ini otomatis terinstall nginx

![image](https://user-images.githubusercontent.com/99697182/172560234-56c1e3d8-7867-4ffd-b815-853e54dd9b82.png)

6. Sebelumnya Disini saya akan membuat user yang lain sebagai utama dengan cara sebelumnya :

```
sudo adduser nginx
```
![image](https://user-images.githubusercontent.com/99697182/172562413-4a5faf6a-ba32-4358-9851-abe86bbe6c35.png)

disini user : nginx, pw nya : nginx123

```
sudo nano /etc/ssh/sshd_config
```

![image](https://user-images.githubusercontent.com/99697182/172562554-e6ca0ca3-31c2-4aab-8baa-b21179b3b2cb.png)

![image](https://user-images.githubusercontent.com/99697182/172562664-284a82ac-9316-4806-a6d5-b9153ceed221.png)

```
sudo systemctl reload sshd
```

```
sudo usermod -aG sudo nginx
```

```
logout
```

```
ssh nginx@103.55.37.95
```

![image](https://user-images.githubusercontent.com/99697182/172563045-23bf47c1-b607-41e6-9aed-89f22ace5e51.png)

![image](https://user-images.githubusercontent.com/99697182/172564239-9d3b895e-edd9-471e-a6ff-698b66d72759.png)


7. Selanjutnya buat direktori baru pada /etc/nginx , saya akan membuat direktori baru bernama wayshub dengan perintah

```
sudo mkdir wayshub
```

![image](https://user-images.githubusercontent.com/99697182/172564764-02fdf6c7-00b1-4cf2-b29a-f3ecc2de7026.png)

8. Selanjutnya saya akan membuat file untuk menyimpan konfigurasi dari reverse proxy

```
sudo nano proxy.conf
```

9. Kemudian masukan script dibawah ini 

```
server {
        server_name wayshub.xyz;

        location / {
                proxy_pass http://10.71.15.131:3000;
        }
}
```

![image](https://user-images.githubusercontent.com/99697182/172565437-c1a5a0d5-c0c2-46b7-877d-4729c5133814.png)

Keterangan : server_name adalah nama server , proxy_pass isi dengan ip dari aplikasi

lalu save 

![image](https://user-images.githubusercontent.com/99697182/172565608-b52e7315-9cf1-4082-8736-9f0caed7b20f.png)

10. Kemudian masuk ke file nginx.conf untuk menambahkan konfigurasi proxypass

![image](https://user-images.githubusercontent.com/99697182/172565893-558df0a9-9de4-436e-a669-6f598dda7831.png)

![image](https://user-images.githubusercontent.com/99697182/172566109-0f30ae79-af0c-43b3-ba67-67a7dbb2f2a4.png)

11. Kemudian Cek dan reload

```
sudo nginx -t
```

```
sudo systemctl reload nginx
```

```
sudo systemctl status nginx
```

![image](https://user-images.githubusercontent.com/99697182/172566671-35f8715e-b3b1-46de-b4e7-5a923190260f.png)


# Step 3 - Menjalankan Aplikasinya

1. Pertama-tama kita beralih ke user aplikasi yang sudah kita buat di awal , kemudian masuk ke direktori aplikasinya , dan kita  akan menginstall PM2 yang tujuannya yaitu supaya aplikasi dapat berjalan pada background

```
npm install pm2 -g
```

![image](https://user-images.githubusercontent.com/99697182/172569491-c19b5330-dd09-43b3-af90-ba1ed1ef80f0.png)

2. Kemudian Kita akan membuat ekosistem pm2 ,

```
pm2 init simple
```

```
pm2 ecosystem simple
```
![image](https://user-images.githubusercontent.com/99697182/172569691-49f31ccb-1dc3-488e-9741-0c43abf5c30f.png)

![image](https://user-images.githubusercontent.com/99697182/172569779-78a7612d-5c04-40cf-9242-27c0aca6868b.png)

3. Kemudian masuk ke file ecosystem.config.js 

![image](https://user-images.githubusercontent.com/99697182/172570117-66ba98b0-b1a0-4e28-83c2-f8610ab289f7.png)

dan sesuaikan dengan script ini

```
module.exports = {
  apps : [{
    name   : "frontend-wayshub",
    script : "npm start"
  }]
}
```
kemudian save dan exit

![image](https://user-images.githubusercontent.com/99697182/172570391-437d523e-0787-4538-8225-916353f2d5f9.png)

4. kemudian kita jalan kan aplikasinya 

```
pm2 start ecosystem.config.js
```

![image](https://user-images.githubusercontent.com/99697182/172570809-2aa0455f-3dd4-46fd-90b3-b853ff5aba5c.png)

5. dan kita cek browser kita 

```
103.176.78.23:3000
```

![image](https://user-images.githubusercontent.com/99697182/172572352-81e71726-c0e5-4ee5-94bf-e4169f631750.png)

Disitu Meskipun kita keluar dari aplikasinya, statusnya masih tetap berjalan karena kita menggunakan pm2

# Step 4 - Membuat DNS (Domain Name Server)

Singkatnya, DNS adalah sebuah sistem yang mengubah URL website ke dalam bentuk IP Address. Tanpa DNS, Anda harus mengetikkan IP Address secara lengkap ketika ingin mengunjungi sebuah website

Disini saya akan membuat DNS pada aplikasi frontend wayshub menggunakan cloudflare

1. Daftar atau login terlebih dahulu di website [CloudFlare](https://dash.cloudflare.com/)

disini klik Studentnya

![image](https://user-images.githubusercontent.com/99697182/172581627-f57a3877-528d-40f9-9de3-06473964a362.png)

kemudian klik DNS

![image](https://user-images.githubusercontent.com/99697182/172581957-6a0fbeb6-ff4d-4528-bdd6-7eece2bf1613.png)

klik add record dan isi 

![image](https://user-images.githubusercontent.com/99697182/172582332-68bdf65a-8b20-4ee3-890d-bb44f129d2b5.png)

Isi nama dan ipv4(ip gateway) kemudian save

Domain yang saya buat : rahman.studentdumbways.id

![image](https://user-images.githubusercontent.com/99697182/172582666-6c03e869-1ba9-42fe-8880-4ac4b64e7f8b.png)

![image](https://user-images.githubusercontent.com/99697182/172582902-f1aa6ea8-a458-4536-8cb2-634ad39889ba.png)

diatas, kita edit menjadi dns only , agar nantinya kita bisa mengakses htpps

![image](https://user-images.githubusercontent.com/99697182/172587185-121df429-01d9-4e3f-bca3-053e66727719.png)


2. Kemudian Masuk ke terminal lagi server gateway dan melakukan konfigurasi baru pada /etc/nginx/wayshub

```
server { 
        server_name rahman.studentdumbways.my.id; 

        location /{
        proxy_pass http://103.176.78.23:3000;
        }
}
```

![image](https://user-images.githubusercontent.com/99697182/172585142-96bef1b4-ae2c-4295-814c-a3fddb6f4e13.png)

![image](https://user-images.githubusercontent.com/99697182/172585300-65147124-7a72-4fb8-a68a-1d88d700b877.png)

3. Kemudian kita cek di browser kita 

```
http://rahman.studentdumbways.my.id/
```

![image](https://user-images.githubusercontent.com/99697182/172586725-7f63f52a-3d59-4813-b614-eeaf339e691e.png)

Apabila berhasil akan tampil aplikasi frontend menggunakan domain http://rahman.studentdumbways.my.id/

# Step 4 - Menggunakan SSL CertBot untuk mengamankan website

## Apa itu SSL ?

SSL adalah singkatan dari Secure Socket Layer, salah satu komponen penting yang harus dimiliki website. Dengan SSL, transfer data di dalam website menjadi lebih aman dan terenkripsi. Bahkan saking pentingnya, Google Chrome melabeli website tanpa sertifikat SSL sebagai Not Secure. 

SSL ini bersifat opensource dan gamapang konfigurasinya 

Apabila sistem keamanan ini ditambahkan pada website Anda, maka URL website akan berubah menjadi HTTPS. Tujuan utama pemasangan SSL adalah sebagai pengaman pertukaran data yang terjadi melalui jaringan internet.

1. langkah pertama masuk ke clouflare dulu , klik myprofile

![image](https://user-images.githubusercontent.com/99697182/172668637-d8dfb8ad-b948-40d9-9163-1d9f75200a77.png)

klik API token

![image](https://user-images.githubusercontent.com/99697182/172668784-bb8d6e63-d042-4e65-92ba-14ec5e5a24c3.png)

klik View DI global API key, dan masukan password cloudflare nya

![image](https://user-images.githubusercontent.com/99697182/172669084-7b991a17-34f5-4526-b289-4f1750613c4f.png)

kemudian copy tokennya

![image](https://user-images.githubusercontent.com/99697182/172669213-eb7997b4-9f2e-4828-bf06-2dee3de8de6c.png)

2. Kemudian balik ke gateway server dan buat direktori `.secret`, dan buat konfigurasi untuk cloudflare didalamnya 

![image](https://user-images.githubusercontent.com/99697182/172669789-03042613-ae4c-4c15-a7cd-66addf9cebbf.png)

masukan script berikut dan pastekan token didalamnya

```
dns_cloudflare_email = "abdulrahmaneffendi789@gmail.com"
dns_cloudflare_api_key = "dadd0433b3e3faf6a822472c0a7193e881169"

```

![image](https://user-images.githubusercontent.com/99697182/172670096-82c9941b-c944-478e-80a6-6bdf5e54a52a.png)

kemudian agar lebih aman kita akan mengatur izinnya agar hanya bisa di read aja

```
chmod 400 nginx.ini
```

![image](https://user-images.githubusercontent.com/99697182/172670806-9a73556b-bdc6-4fc6-983d-e4125eef7f5d.png)

jika sudah , maka cloudflare kita sudah terhubung dengan gateaway server kita

3. Langkah selanjutnya masuk ke gateaway server, dan instalasi certbot

kita pastikan dulu kalau snapd kita ter update

```
sudo snap install core; sudo snap refresh core
```
![image](https://user-images.githubusercontent.com/99697182/172592350-19862911-6012-4beb-9b65-1248ed4ffca7.png)

![image](https://user-images.githubusercontent.com/99697182/172664736-dd4e2f93-b04a-4c52-8905-814c55c1daa6.png)

disini, server saya done, dan akan membuatnya kembali 

![Img 1](assets/7.png)

saya ganti dan buat lagi os = nginx ubuntu 20, dan 2 user, sebagai user utamanya "unyu" pw = unyu 

![Img 1](assets/8.png)

Kemudian saya juga mengubah DNS nya

![Img 1](assets/12.png)

kemudian saya juga mengubah API tokennya 

`2312cc76618891ed4cb390af35876866b5a96`

![Img 1](assets/13.png)

![Img 1](assets/14.png)

kemudian saya coba lagi untul instalasi certbot 

![Img 1](assets/9.png)

setelahnya masukan perintah :

```
sudo snap install --classic certbot
```

![Img 1](assets/10.png)

4. Kemudian Masukan perintah berikut agar certbet bisa di akses menggunakan coment 

```
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

![Img 1](assets/11.png)

5. Jalankan certbot menggunakan perintah

```
sudo certbot 
```

pertama di minta email dari cloudflare 

kedua klik y untuk sertifikat nya 

ketiga optional kalau sertifikatnya mau expired, akan ada email berisikan pemberitahuan expired 

keempat masukan nama domain yang akan di gunakan 

kemudian Sukses

![Img 1](assets/15.png)

6. dan kita cek 

![Img 1](assets/16.png)

disini sepertinya ada yang salah, dan kesalahannya adalah belum membuat reverse proxy di server nginx baru unyu ini. 

7. Kemudian saya menambahkan proxy dan membuat sertifikat lagi 

disini saya menginstall ulang certifikatnya

![Img 1](assets/17.png)

namun masih belum berubah

![Img 1](assets/18.png)

8. Kemudian saya coba untuk renew dan replace sertifikatnya 

![Img 1](assets/19.png)

dan masih tetap sama

![Img 1](assets/20.png)










