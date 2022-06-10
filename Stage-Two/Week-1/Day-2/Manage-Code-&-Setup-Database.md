# Manage Code & Database

# Membuat server backend dan database menggunakan [IdCloudhost ](https://console.idcloudhost.com/)

# Membuat server backend

1. sama seperti sebelumnya, kita login dulu, kemudian klik compute dan create new 

![image](https://user-images.githubusercontent.com/99697182/172869124-6cd93ecb-6045-4805-8902-ff5687df5bdc.png)

![image](https://user-images.githubusercontent.com/99697182/172869816-56c916c5-a126-494c-9a20-c019b14661cf.png)

![image](https://user-images.githubusercontent.com/99697182/172870479-75c766d4-9f3b-4876-8e93-2ca63039efe2.png)

![image](https://user-images.githubusercontent.com/99697182/172870565-52cb9076-0936-4ddc-8916-43a4d98a2af1.png)

2. kemudian login ke akunnya

![image](https://user-images.githubusercontent.com/99697182/172871161-ab692796-2483-4226-a04f-edd6c794c8da.png)

Update & Upgrade 

![image](https://user-images.githubusercontent.com/99697182/172871792-d51e2b99-fbe6-47b8-ac7f-d3584782f2b5.png)

disini saya akan buat server lain , user : inyi, pw : inyi

![image](https://user-images.githubusercontent.com/99697182/172872418-aa460d29-46a1-4806-9ad2-d7f839e40d01.png)

![image](https://user-images.githubusercontent.com/99697182/172872598-65b06a3c-4844-4ce0-93a0-0d828ee459d4.png)

![image](https://user-images.githubusercontent.com/99697182/172873075-b01301d5-3e38-40da-85f0-4d1bfc306e4b.png)

# membuat server database 

1.kita create vm nya

![image](https://user-images.githubusercontent.com/99697182/172874191-6b9fb3c6-b6ee-4d41-a3c7-67a5fda4ea67.png)

![image](https://user-images.githubusercontent.com/99697182/172874548-a12b09f7-d8be-430f-87ee-ccaa18e8e2d6.png)

![image](https://user-images.githubusercontent.com/99697182/172874912-f7a0d34c-12c6-4a78-b6dc-1bb0e1633cb4.png)

![image](https://user-images.githubusercontent.com/99697182/172875293-b2c83d2c-ceeb-4a03-9a2b-4a8fd7ee665b.png)

2. kita remote 

![image](https://user-images.githubusercontent.com/99697182/172875657-ec6b92d6-1122-4e1b-ae70-ee15e801ed5e.png)

![image](https://user-images.githubusercontent.com/99697182/172875811-3fc9477e-2e9f-4426-bec0-dd172e6ee877.png)

disini saya akan menambakhkan user, user : enye, pw : enye

![image](https://user-images.githubusercontent.com/99697182/172876302-3be8d912-1494-4055-aaeb-5ba6a495a37c.png)

![image](https://user-images.githubusercontent.com/99697182/172876534-989518ec-82a5-46cb-9d1b-91ea29cdc7f8.png)

![image](https://user-images.githubusercontent.com/99697182/172876830-40f76576-3dd8-48e8-bbea-8cd98a5dbc19.png)

Jika DI total dengan pertemuan kemarin, Saya punya 4 Server , berikut ilustrasinya :

![image](https://user-images.githubusercontent.com/99697182/172882892-4b4c53d0-8825-4973-aa7e-95723f58eb3a.png)

# Generate SSH Key dan transfer ke semua server

## SSH

SSH adalah protokol secure yang digunakan untuk mengelola hosting atau server secara remote. Dengan menggunakan protokol ini, Anda tidak perlu mendatangi lokasi fisik server, karena pengelolaan bisa dilakukan secara remote dari lokasi manapun. 

1. Kita generat keygen di Gateaway server 

Pertama tama gunakan ssh-keygen untuk membuat ssh key

```
ssh-keygen
```

![image](https://user-images.githubusercontent.com/99697182/172887388-9a98b382-8799-4312-a948-673e3903e940.png)

2. Kemudian masuk ke direktori .ssh lalu gunakan perintahcat untuk melihat id_rsa.pub

```
cat id_rsa.pub
```

![image](https://user-images.githubusercontent.com/99697182/172888855-f5616d99-3304-4a78-8fc6-42a90aec6834.png)

3. Kemudian buat file authorized_keys dan masukan id_rsa.pub kalian disini lalu save dan exit

![image](https://user-images.githubusercontent.com/99697182/172889108-3ff8aa10-4aaa-410b-a8a8-c689aa1fb00d.png)

![image](https://user-images.githubusercontent.com/99697182/172889333-19a347e0-a938-485f-a1b2-cd7b7b3866de.png)

4. Kemudian Masuk ke frontend-server dan buat direktori .ssh 

![image](https://user-images.githubusercontent.com/99697182/172889937-1f9922c0-9892-4764-8b09-deadcd195eb8.png)

5. Kemudian masuk lagi ke dir di gateaway-server dan migrasikan file id_rsa.pub ke server-frontend menggunakan perintah scp id_rsa.pub "username"@ip:./

Pada server gateway masukan perintah

```
scp id_rsa.pub anya@103.176.78.23:/home/anya/.ssh/
```

![image](https://user-images.githubusercontent.com/99697182/172891212-64b7d005-2ad4-4cf9-b1fb-43adc206e03f.png)

6. kemudian kita cek apakah sudah ter-migrasi ke frontend-server

![image](https://user-images.githubusercontent.com/99697182/172892182-902da92c-6b2f-492c-9655-d2d9adc7c906.png)

kemudian kita buat authorized key juga dan pastekan key nya 

![image](https://user-images.githubusercontent.com/99697182/172892720-cefbc6cd-628e-4fdf-b45b-b28308090d00.png)

![image](https://user-images.githubusercontent.com/99697182/172893003-e08cdbf6-a619-4c29-8a8b-34f7bd6f211c.png)

7. Kemudian kita coba login ke server frontend  dari server gateway tanpa password

dan disini kita berhasil

![image](https://user-images.githubusercontent.com/99697182/172893329-ad71cce5-6ebc-4ce7-8c38-63a1ef0a07d3.png)

8. Kemudian lakukan hal serupa pada server lainnya

![image](https://user-images.githubusercontent.com/99697182/172894696-e52f3b91-dcc1-43bc-8725-a61a1d374797.png)

disini bisa masuk ke backend

![image](https://user-images.githubusercontent.com/99697182/172895147-997d2596-da3d-4078-a829-5e6537d5503c.png)

disini bisa masuk ke database

![image](https://user-images.githubusercontent.com/99697182/172895418-946893f7-cef2-41d3-8ade-f704721cdcd7.png)

# Instalasi MYSQL pada server Database

1. Masukan perintah instal

```
sudo apt-get install mysql-server
```

![image](https://user-images.githubusercontent.com/99697182/172896799-f71f3810-2dcd-4805-94d9-bb2ef100525c.png)

Untuk instalasi baru MySQL, Anda akan menjalankan skrip keamanan DBMS yang disertakan. Skrip ini mengubah beberapa opsi asali yang kurang aman untuk hal-hal seperti log masuk root jarak jauh dan pengguna sampel.

2. lalu jangan lupa jalankan script keamanan dan masukan password baru yang lebih kuat

```
sudo mysql_secure_installation
```

![image](https://user-images.githubusercontent.com/99697182/172899225-39b69f7f-a664-437b-84d7-80a939334260.png)

3. Untuk melihat versi gunakan perintah

```
mysql --version
```

Untuk masuk ke mysql gunakan perintah

```
sudo mysql -u root
```

![image](https://user-images.githubusercontent.com/99697182/172899738-5dfe28f7-734e-40d8-a34e-1b81463a26ed.png)

# Membuat Database Baru pada user baru

1. Untuk membuat pengguna yang dapat terhubung dari host mana pun, gunakan wildcard ‘%‘ sebagai bagian host:

```
CREATE USER 'user_database'@'%' IDENTIFIED BY 'password_user';
```

Opsi ini biasanya digunakan oleh para webmaster yang menginginkan MySQL server ditempat terpisah dengan web server.

![image](https://user-images.githubusercontent.com/99697182/172904375-44168b37-a140-495b-9d97-a42444e460fe.png)

2. Memberikan semua hak istimewa ke akun pengguna untuk semua database :

```
GRANT ALL PRIVILEGES ON *.* TO 'user_database'@'localhost';
```

![image](https://user-images.githubusercontent.com/99697182/172905771-e98d637a-1275-4761-83d3-6a42cdd6f467.png)

3. Kemudian saya login dengan user baru yang tadi di buat

```
mysql -u rahman -p
```

![image](https://user-images.githubusercontent.com/99697182/172969007-131a4b52-7b7f-4aa4-89ba-0be5392a0018.png)


```
SELECT user, FROM mysql.user
```

![image](https://user-images.githubusercontent.com/99697182/172905900-6705511f-378a-47e9-aa88-160b20543b3f.png)

# Membuat database wayshub pada mysql

```
CREATE DATABASE wayshub;
```

Untuk melihat isi dari database gunakan perintah
```
show databases;
```

```
USE wayshub;
```

```
SHOW TABLES;
```

![image](https://user-images.githubusercontent.com/99697182/172970110-42b19262-0e94-458a-a9da-724d8e90baa1.png)


![image](https://user-images.githubusercontent.com/99697182/172906587-776e8675-8097-441a-b0dc-830a13f3160d.png)

# Mengganti bind address

Fungsi melakukan bind address yaitu supaya database dapat di akses oleh client

![image](https://user-images.githubusercontent.com/99697182/172907397-7078a956-b891-47b2-9bf9-cc196ced2f00.png)

```
bind-address            = 0.0.0.0  
mysqlx-bind-address     = 0.0.0.0 
```

![image](https://user-images.githubusercontent.com/99697182/172907514-02f530f5-2fcc-48dd-95fb-b9d574c49419.png)

Lalu restart mysql

```
systemctl restart mysql.service
```

![image](https://user-images.githubusercontent.com/99697182/172907743-0a9c774d-c26a-4fb8-96d6-682ee8697ff4.png)


# Dapat meremote database dari client

# Memberikan Akses Kepada User
