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


# Step 3 - Membuat Konfigurasi Reverse Proxy pada server gateway yang mengarah ke server aplikasi1 dengan domain dumbways.xyz

## Apa itu Reverse Proxy?

Reverse proxy adalah konfigurasi standar yang digunakan untuk mengubah jalur traffic, misalkan aplikasi menggunakan port 3000 tetapi agar dapat di akses melalui port 80 maka harus menggunakan reverse proxy.

Berikut adalah konfigurasi dari revese proxy :

```
server { 
    server_name domain.com; 
    
    location / { 
             proxy_pass http://127.0.0.1:3000;
    }
}
```

## Kenapa Harus Reverse Proxy?
Untuk mengamankan aplikasi yang berjalan pada server maka kita perlu untuk melakukan reverse proxy, supaya pengguna tidak dapat mengakses aplikasi kita secara langsung.

## Membuat Konfigurasi Revese Proxy 
Untuk membuat reverse proxy dapat mengikuti langkah-langkah berikut :

1. Pertama-tama masuk ke folder nginx setelah itu buat suatu directory baru telebih dahulu.

```
cd /etc/nginx
```

![image](https://user-images.githubusercontent.com/99697182/171996781-2533fa5b-3451-43a8-acf7-fdbf8476ca13.png)

```
sudo mkdir wayshub
```

![image](https://user-images.githubusercontent.com/99697182/171999870-5e8c0e2e-ed81-48ec-af36-e1e9e7cd41ac.png)


2.Setelah itu masuk ke directory yang sudah kalian buat, setelah itu buat suatu file dengan nama `frontend.conf`

```
cd wayshub
```

```
sudo nano frontend.conf
```

![image](https://user-images.githubusercontent.com/99697182/171999935-ac94b67a-e4e0-4e74-bed8-8a0f3df6e477.png)

3. Setelah itu masukkan konfigurasi berikut:

```
server { 
    server_name dumbways.xyz; 
  
    location / { 
             proxy_pass http://127.0.0.1:3000;
    }
}
```

dan jangan lupa menamakan domainnya dengan `dumbways.xyz`

![image](https://user-images.githubusercontent.com/99697182/172000262-4b411829-a180-4fc0-a1a9-f0fb24896b90.png)


`
INFO
pastikan port 3000 di ganti sesuai aplikasi yang digunakan.
`

`
ket : 127.0.0.1  nya diganti dengan ip dimana aplikasinya berada
`

4.Untuk mendapatkan ip dimana aplikasi nya berada, kita pindah dulu ke server1 dan  kita clone apilkasinya dengan perintah ini :

```
git clone https://github.com/dumbwaysdev/wayshub-frontend
```

![image](https://user-images.githubusercontent.com/99697182/172000135-18c24a67-8afc-4379-8492-86a065a1b36d.png)

5.Kemudian Kita masuk ke folder aplikasinya dan ketik `ip a` untuk meng-copy ip nya

![image](https://user-images.githubusercontent.com/99697182/172000212-48609984-3769-441c-b1f6-cb3939bc539f.png)

6.Setelah itu kita masuk lagi gateaway-server, lalu ke file `frontend.conf` dan paste ip aplikasinya kemudian save 

![image](https://user-images.githubusercontent.com/99697182/172000318-b931433d-605a-46f4-aa88-38850c28773d.png)

7. Selanjutnya keluar dari directory `wayshub`, setelah itu masuk ke dalam file `nginx.conf`.

![image](https://user-images.githubusercontent.com/99697182/172000481-14d98c4e-d6a6-42cb-b4ea-139870bfdedc.png)

```
sudo nano nginx.conf
```

![image](https://user-images.githubusercontent.com/99697182/172000508-6370a848-d361-49dd-8503-f2c012c2c3e4.png)

8. Selanjutnya pergi ke-bagian include, setelah itu masukan lokasi dari directory yang bersi konfigutasi yang sudah kalian buat tadi.

![image](https://user-images.githubusercontent.com/99697182/172000570-60c6b0dc-3d69-451c-89d3-24c4d9ad52e6.png)

`
INFO
/*; menandakan file nginx.conf akan membaca seluruh file yang berada di dalam directory wayshub
`

9. Beberapa proses tadi adalah cara untuk membuat reverse proxy untuk aplikasi kita, kemudian pastikan untuk melakukan pengecekan konfigurasi dengan menjalankan perintah :

```
sudo nginx -t
```

![image](https://user-images.githubusercontent.com/99697182/172000669-c60b9a25-aba3-402c-9236-1626fb78bf9b.png)

ket : Disini saya mengalami fail karena typo pada file `frontend.conf`, oleh karena nya saya akan memperbaikinya :

![image](https://user-images.githubusercontent.com/99697182/172000730-512898c8-1de6-4c29-beb1-05beea36c384.png)

saya akan menambahkan `a` 

![image](https://user-images.githubusercontent.com/99697182/172000748-e4897148-f73f-485c-8845-9e1cfb1f9572.png)

setelah itu kita cek lagi 

![image](https://user-images.githubusercontent.com/99697182/172000762-db14d9bc-75d7-43ad-ba28-b75eab02a0a3.png)

nah disini dikatakan kalau syntax kita ok

10. Jika sudah sekarang kita tinggal melakukan restart/reload Nginx kita.

```
sudo systemctl restart nginx
```

![image](https://user-images.githubusercontent.com/99697182/172000855-e91abbaf-bb2d-4000-bf2b-684b02eba18c.png)

11. kita akan melakukan cek status 

![image](https://user-images.githubusercontent.com/99697182/172000927-21501301-d822-458e-abbf-ec16c322cdf7.png)

12. kita akan melakukan reload juga 

![image](https://user-images.githubusercontent.com/99697182/172000945-c888bf3f-efee-4d1e-9a22-4ab5605eaa9a.png)

13. Sekarang kita akan membuat sebuah virtual host. Untuk membuat virtual host kita harus masuk ke local server kita setelah itu masuk ke dalam file `/etc/hosts`.

```
sudo nano /etc/hosts
```

![image](https://user-images.githubusercontent.com/99697182/172001022-356d50fa-2430-4c16-85c4-2fa7409849c9.png)

14. Setelah itu masukkan IP server kita selanjutnya masukkan nama domain yang kalian inginkan.

untuk mengecek ip server kita, kita masuk ke gateaway server, kemudian ketik `ip a`

![image](https://user-images.githubusercontent.com/99697182/172001257-08c78883-b876-4214-85a2-de56b580ec41.png)

selanjutnya masukan ip nya di lokal server dan masukan nama yang diinginkan

![image](https://user-images.githubusercontent.com/99697182/172001198-4c76d645-3c9c-446a-8a0b-f5de632451e4.png)

15. Jika sudah sekarang coba buka web browser kalian setelah itu coba akses nama domain kalian.

![image](https://user-images.githubusercontent.com/99697182/172001318-8680686e-b804-4298-80bb-608f5b8dcb5b.png)

16. Jika kita lihat disini adalah kita mendapatkan 502 Bad Gateway kenapa? karena kita belum menjalankan aplikasi kita. Sekarang kita coba untuk menjalankan aplikasi wayshub yang sudah pernah kita pakai sebelumnya. Untuk menjalankan aplikasi wayshub kalian dapat mengikuti langkah-langkah berikut ini.

17. Masuk ke server1 yang sudah kita clone aplikasi wayshub tadi

kemudian masuk ke file nya

kemudian install npm nya 

```
sudo apt install npm
```

![image](https://user-images.githubusercontent.com/99697182/172003075-8266b664-aefb-4db8-8a04-263d44083329.png)

keterangan : perintah di atas ini bertujuan untuk meng-install module dari aplikasi `node.js`

kita boleh cek dulu versi npm dan node nya `npm -v` dan `node -v`

![image](https://user-images.githubusercontent.com/99697182/172003680-08c28bdd-f008-4ea7-95eb-35dce7c41777.png)


18. kemudian kita coba jalankan apknya

```
npm start
```
perintah diatas untuk menjalankan aplikasinya

![image](https://user-images.githubusercontent.com/99697182/172003752-ca7b8920-ee4f-4eec-a6eb-fe1a622ab981.png)

dari gambar diatas, menunjukan error 

![image](https://user-images.githubusercontent.com/99697182/172004345-fc9dd2e8-8bb8-4b23-ac66-289431086743.png)

diatas  saya mencoba untuk install npm lagi dengan perintah `npm i`

![image](https://user-images.githubusercontent.com/99697182/172004521-8fbfe282-3b02-44f3-b55e-c0816f521ad2.png)

dari gambar diatas sudah terlihat bahwa package node_modules nya sudah ada 

19. Kemudian Kita jalankan lagi dengan perintah `npm start`

![image](https://user-images.githubusercontent.com/99697182/172005070-79be6202-2ac4-4ee7-bcf7-0df0939b8432.png)


![image](https://user-images.githubusercontent.com/99697182/172005000-879469cb-72ab-4652-90f0-b874f1c64aeb.png)

![image](https://user-images.githubusercontent.com/99697182/172005107-e3d59e2b-dbf4-48fc-9d78-08f07a9ac517.png)

20. Kemudian kita refresh browser apk kita

dan disini saya masih mengalami error :

![image](https://user-images.githubusercontent.com/99697182/172005034-cb4d4ca1-a2e7-4cc7-bbc6-e14dcf772073.png)

21. disini saya coba lagi dengan install ulang ngine node js nya 

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```

![image](https://user-images.githubusercontent.com/99697182/172005711-71a232c9-f776-4385-b7d7-4a0dd5754f38.png)

```
exec bash
```

![image](https://user-images.githubusercontent.com/99697182/172005796-6f9947f5-6e69-4de3-bfd6-aa7c0a5fa2dd.png)

![image](https://user-images.githubusercontent.com/99697182/172005993-41033ead-42d0-454d-8ef0-91056ccc7056.png)

Selanjutnya kita coba untuk me-refresh web browser kita.

![image](https://user-images.githubusercontent.com/99697182/172006014-52777224-0a7a-49c3-b11a-ea2545d08469.png)

dan diatas masih menunjukan blum berjalan

22. kemudian jika saya cek browser menggunakan ip nya, aplikasinya berjalan :

![image](https://user-images.githubusercontent.com/99697182/172030202-19fdb143-f5b1-4ede-a4d4-5f6067a64f23.png)

dikarenakan masih tidak terhubung, disini saya masih mau cek kembali dari langkah awal


# Step 4 - Membuat konfigurasi load balancing pada server gateway yang mengarah ke server aplikasi2 dengan domain loadbalance.dumbways.xyz

## Apa itu Load Balancing?

Load Balancing adalah suatu jaringan komputer yang menggunakan metode untuk mendistribusikan beban kerjaan pada dua atau bahkan lebih suatu koneksi jaringan secara seimbang agar pekerjaan dapat berjalan optimal dan tidak overload (kelebihan) beban pada salah satu jalur koneksi.

## Kenapa Harus Load Balancing?

Jika kita memiliki website atau aplikasi yang telah digunakan hingga ribuan, ratusan atau bahkan jutaan pengguna maka kita harus melakukan load balancing pada aplikasi tersebut agar tidak down, karena beban akses pengguna dibagi ke beberapa server sekaligus.

## Membuat Konfigurasi Load Balancing

1. Untuk membuat Load Balancing kalian harus membuat server baru lagi. Untuk cara membuat server kalian ikuti saja step by step seperti saat pertemuan Fundamental DevOps : https://ebook-devops.vercel.app/Fundamental-DevOps/Install-Ubuntu-Server

2. Jika server kalian sudah terbuat maka buatlah aplikasi sederhana sama seperti pertemuan sebelumnya (node.js). setelah itu jalankan aplikasi tersebut.

- disini saya memakai server2 yang telah saya buat

![image](https://user-images.githubusercontent.com/99697182/172033637-ec48dc55-4294-411a-8064-8f619f6785a2.png)

![image](https://user-images.githubusercontent.com/99697182/172033682-950a0e7f-212c-4133-92b7-fda8759e202b.png)

![image](https://user-images.githubusercontent.com/99697182/172033838-37c9e140-dc62-4108-b1f1-25dad867508e.png)

![image](https://user-images.githubusercontent.com/99697182/172034103-8b006ce6-def1-4c25-956d-b2b50d3e7feb.png)

![image](https://user-images.githubusercontent.com/99697182/172034136-f24147c3-564c-4aa5-8337-b0f5d93db49b.png)

![image](https://user-images.githubusercontent.com/99697182/172034142-5fd7a121-a79c-4c49-ac6a-2dde20dbf541.png)

![image](https://user-images.githubusercontent.com/99697182/172034160-1ed815c0-92e5-4451-b415-38e6edfaed2e.png)

- Sekarang kita sudah mempunyai 2 buah server untuk aplikasi kita.

- Sekarang kita akan coba untuk membuat konfigurasi load balancing.

3. Kemudian kita masuk ke dalam konfigurasi reverse proxy yang sudah kita buat sebelumnya di server gateaway

```
sudo nano sudo nano /etc/nginx/wayshub/frontend.conf
```
![image](https://user-images.githubusercontent.com/99697182/172034345-419a7d64-8829-4d8a-950c-87270f424c58.png)

4. Selanjutnya kita akan tambahkan konfigurasi ke dalam file frontend.conf. Sekarang kita akan coba tambahkan beberapa konfigurasi, kalian dapat menggunakan konfigurasi di bawah ini.

```
upstream wayshub { 
    server 10.109.135.6:3000;
    server 10.109.171.2:3000;
}
server { 
    server_name loadbalance.dumbways.xyz; 
  
    location / { 
             proxy_pass http://dwayshub;
    }
}
```



pada gambar dibawah ini, kita bisa liat ip server-server kita :

![image](https://user-images.githubusercontent.com/99697182/172034453-62e342b4-610a-4e3c-87fa-8da5deea550b.png)

kemudian :

![image](https://user-images.githubusercontent.com/99697182/172034550-abdda0b5-11eb-4381-bf83-923d182d620f.png)

keterangan :

- Pada bagian upstream kalian dapat mengganti nama domain dengan nama yang kalian inginkan.

- Pada bagian server masukan IP dari server kalian, setelah itu diikuti dengan port aplikasi.

- Selanjutnya pada bagian proxy_pass ubah dari yang sebelumnya adalah alamat IP dari aplikasi kalian, sekarang kalian samakan dengan nama upstream yang ada di konfigurasi kalian.

- Jika sudah sekarang kita coba cek apakah konfigurasi yang sudah kita buat tadi itu error atau tidak.

```
sudo nginx -t
```

![image](https://user-images.githubusercontent.com/99697182/172034598-8ad7f0c4-1612-463d-9191-4fee82ccac3a.png)

5. Jika tidak ada error jalankan perintah restart nginx untuk merestart nginx kita, karena kita sudah menambahkan suatu konfigurasi baru di dalam file reverse proxy kita.

```
sudo systemctl restart nginx
```

![image](https://user-images.githubusercontent.com/99697182/172034623-136c6d0d-cd1a-4451-a125-24472f24e7df.png)

6. Selanjutnya jalankan aplikasi kita yang ada di server kita.

-kita clone , install npm dan jalankan 

```
git clone https://github.com/dumbwaysdev/wayshub-frontend
```

![image](https://user-images.githubusercontent.com/99697182/172034698-e216fc3a-d5bd-4168-a227-a14ebbae9e16.png)

```
sudo apt install npm
```
![image](https://user-images.githubusercontent.com/99697182/172034718-786be8c4-2fd1-4e63-9a08-fedccda1a763.png)

```
npm i
```



