# Setup Docker | Frontend, Backend dan Database Deployment.


## Langkah 1 - Membuat Server Pada IdCLoudHost

Disini Saya membuat 2 Buah Server Dengan Spek Berikut:

1. Gateway-Server : CPU : 1, RAM : 1, Disk : 20

Ip Public = 103.179.56.23

User 1 & Pwnya : ubuntu = Sembarang1

User 2 & Pwnya : get = get

![image](https://user-images.githubusercontent.com/99697182/173317837-8777500c-ad84-48e0-9d1e-812405ac9395.png)

2. App-Server : CPU : 2, RAM : 2, Disk : 20

Ip Public = 103.172.204.174

User 1 & Pwnya : ubuntu = Sembarang1

User 2 & Pwnya : app = app

![image](https://user-images.githubusercontent.com/99697182/173318847-e2f149f1-55e3-4a43-9e88-497fa8045475.png)

## Langkah 2 - Instalasi and Config Docker

1. Install Docker menggunakan bash dengan isi berikut:

```
sudo apt-get update
sudo apt-get install \
ca-certificates \
curl \
gnupg \
lsb-release
    
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

![image](https://user-images.githubusercontent.com/99697182/173328366-5d49fd58-9767-4a76-b731-be9fc7b53b74.png)

![image](https://user-images.githubusercontent.com/99697182/173328172-7e98178c-229d-4a81-bf28-0f4083355234.png)

2. Cek versi docker menggunakan:

```
docker -v
```

![image](https://user-images.githubusercontent.com/99697182/173328661-b8536b6f-4a90-4894-87b2-da84b175ac71.png)

```
docker versi
```

![image](https://user-images.githubusercontent.com/99697182/173495456-052fb8d5-c2a3-4466-bd3c-fb7c80d4cb6c.png)


3. Kita akan membuat perintah docker agar tidak menggunakan sudo lagi dengan perintah berikut:

```
sudo usermod -aG docker app
```

![image](https://user-images.githubusercontent.com/99697182/173329013-3e364858-4811-4dcd-868a-fb9a01fe1f23.png)

4. Sekarang kita login menggunakan:

```
docker login
```

Sebelumnya, Saya mau membuat akun terlebih dahulu pada [hub.docker](https://hub.docker.com/signup) ini

![image](https://user-images.githubusercontent.com/99697182/173330457-129b621d-21f8-4db8-87ae-7f793985d7f3.png)

Disini saya mempunyai akun docker : arahmane = Docker123

![image](https://user-images.githubusercontent.com/99697182/173330690-0764764c-9d30-484d-b648-90039fa7b468.png)

## Langkah 3 - Docker Images

1. Sekarang kita mendownload node versi dubnium alpine 3.11 dan mysql dengan tag latest

```
docker pull node:dubnium-alpine3.11
```

```
docker pull mysql
```

![image](https://user-images.githubusercontent.com/99697182/173342836-f7019cce-e212-4115-bf74-676753e9f912.png)

2. Sekarang kita cek images apakah sudah berhasil di pull dengan:

```
docker images
```

![image](https://user-images.githubusercontent.com/99697182/173342959-9f3015b8-e137-4471-8636-0473668c02ab.png)

Untuk memasuki container mysql gunakan perintah

```
docker container exec -it database bash
```

![image](https://user-images.githubusercontent.com/99697182/173495847-d5dac6db-b4c9-48f7-b7e7-491c3ebd78cc.png)

masuk ke mysql nya dan masukan password : Are132465798

![image](https://user-images.githubusercontent.com/99697182/173496247-8fb8bbff-83cf-4da6-99cc-805e20eaa400.png)

Show Databases

![image](https://user-images.githubusercontent.com/99697182/173496405-d3658537-2d81-4742-ac89-6e857f7dbe52.png)


## Langkah 4 - Setup Frontend & Backend

1. Sekarang saya clone front end dan back end nya

```
git clone https://github.com/dumbwaysdev/wayshub-frontend
```

```
git clone https://github.com/dumbwaysdev/wayshub-backend
```

![image](https://user-images.githubusercontent.com/99697182/173343711-1a37d019-e94b-4d50-8d8e-2bc09a6ec5e1.png)

2. Sekarang saya akan run images mysql dan membuat volume dengan directory mysql-data

```
docker run -d --name database -p 3306:3306 -v ~/mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=Are132465798 -e MYSQL_DATABASE=wayshub mysql:latest
```

![image](https://user-images.githubusercontent.com/99697182/173344364-c1b8acc4-d729-4e4e-8625-7ab411f36c68.png)

3. Sekarang saya akan mengkonfigurasi backend nya dengan membuat docker compose

Install terlebih dahulu docker compose

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

```
sudo chmod +x /usr/local/bin/docker-compose
```

```
docker compose --version
```

![image](https://user-images.githubusercontent.com/99697182/173344915-c6edcc32-d49a-4fab-93a0-1e97e04c90ba.png)

4. Masuk ke directory backend dan copy env.example menjadi .env

Karna disini saya sudah mempunyai .env maka disini saya hanya memperlihatkan isinya

```
cat .env
```

![image](https://user-images.githubusercontent.com/99697182/173345883-14877cc2-04e3-4046-ac1b-ea0c365700bc.png)

5. Sekarang konfigurasi backend ke database dengan cara:

Masuk ke directory config dan edit file config.json

```
nano config.json
```

![image](https://user-images.githubusercontent.com/99697182/173346504-f09ec8be-221c-4a93-af4b-289cdf50a398.png)

![image](https://user-images.githubusercontent.com/99697182/173347257-ec6f1abb-200a-41ba-945c-ea150e9d3c73.png)

6. Kembali ke folder backend dan buat file bernama dockerfile berisi:

```
FROM node:dubnium-alpine3.11
WORKDIR /usr/app
COPY . .
RUN npm install
RUN npm install sequelize-cli -g
RUN npx sequelize db:migrate
EXPOSE 5000
CMD [ "npm", "start" ]
```

![image](https://user-images.githubusercontent.com/99697182/173347854-df788f04-c583-46e8-bb7b-2d4d675e83b4.png)

![image](https://user-images.githubusercontent.com/99697182/173348003-41cd5397-04a4-484c-a084-951144bdc9a6.png)

7. Sekarang buat file docker-compose.yml dengan isi berikut:

```
version: '3.7'
services:
 backend:
   build: .
   container_name: be
   image: arerahman/wayshub-be:stable
   stdin_open: true
   ports:
    - 5555:5000
```
![image](https://user-images.githubusercontent.com/99697182/173348518-d6c32b1e-c64e-4587-ada2-558235efbfcb.png)

![image](https://user-images.githubusercontent.com/99697182/173348565-62e61c9b-e182-4c93-8d4f-6b5e1acaec5e.png)

8. Build dan Jalankan compose secara daemon dengan:

```
docker-compose up -d
```

![image](https://user-images.githubusercontent.com/99697182/173348857-023fc0fe-a7ff-4f21-aaf1-e3c6976a1b99.png)

9. Jika sudah running tes di web browser dengan masukkan ip dan custom port tadi

![image](https://user-images.githubusercontent.com/99697182/173349186-88563ebe-bd35-49d5-964d-499afaf115ab.png)

Jka hasilnya seperti ini, maka berarti berhasil

Kemudian saya akan cek juga migrasi datanya pada mysql

![image](https://user-images.githubusercontent.com/99697182/173497414-ac17b8a7-65d6-417a-bc91-c2ab36d29d4b.png)

Migrasi Data Berhasil 

Selanjutnya saya ingin push repo menuju docker hub

![image](https://user-images.githubusercontent.com/99697182/173498208-7d865218-a6ab-4367-83b1-9294c1bbfde0.png)

Dikarenakan nama repository saya berbeda tidak sesuai username docker hub jadi saya akan membuat tag baru

```
docker tag 7890f31eac9c arahmane/wayshub-be
```

![image](https://user-images.githubusercontent.com/99697182/173498517-858f0329-178a-4372-99b5-b2c0c1d0133a.png)

`KETERANGAN` : Apabila nama repository tidak sesuai dengan akun docker hub maka akan muncul pesan "denied: requested access to the resource is denied"

```
docker push arahmane/wayshub-be
```
![image](https://user-images.githubusercontent.com/99697182/173498824-2e11e26a-320d-407a-8fbf-943c372b898a.png)

Selanjutnya cek di web browser

![image](https://user-images.githubusercontent.com/99697182/173498875-02116a64-99b0-438c-b7f5-8d42ac2da759.png)

![image](https://user-images.githubusercontent.com/99697182/173498939-2b376fcc-5e91-4d59-a2c8-23b5c7eb3e46.png)

10. Jika back end sudah selesai sekarang kita akan ke front end dan mengkonfigurasi front end sebelum membuat compose

Edit api.js di directory syc/config untuk mengkoneksikan ke back end nya

![image](https://user-images.githubusercontent.com/99697182/173349497-500ce5f3-4a60-45eb-a2d4-0aad61121c60.png)

![image](https://user-images.githubusercontent.com/99697182/173349835-b62b1373-c1b1-4142-9630-7a8001ea3069.png)

11. Sekarang ke folder wayshub-frontend dan kita akan buat file dockerfile seperti di backend tadi dengan isi:

```
FROM node:dubnium-alpine3.11
WORKDIR /usr/app
COPY . .
RUN npm install
EXPOSE 3000
CMD [ "npm", "start" ]
```

![image](https://user-images.githubusercontent.com/99697182/173353065-80e2d1c4-de40-494a-a55c-976b0b8427fd.png)

![image](https://user-images.githubusercontent.com/99697182/173353220-b322a013-126a-420d-99c5-062674c0470c.png)

12. Buat file docker-compose.yml untuk front end dengan isi:

```
version: '3.7'
services:
 frontend:
   build: .
   container_name: fe
   image: arerahman/wayshub-fe:stable
   stdin_open: true
   ports:
    - 3333:3000
```

![image](https://user-images.githubusercontent.com/99697182/173353292-8083d78c-cd86-4182-87ea-f4e7a8b5e7d8.png)

![image](https://user-images.githubusercontent.com/99697182/173353613-f1e44d97-f21a-42fd-b0a2-c24c7d3de5c9.png)

13. Build dan Jalankan compose secara daemon dengan:

```
docker-compose up -d
```

disini ada error karena sebelumnya saya sudah membuat container, 

![image](https://user-images.githubusercontent.com/99697182/173354174-fd6af234-ff69-410d-a557-6be884ccd55c.png)

disini saya akan mencoba untuk menghapusnya

![image](https://user-images.githubusercontent.com/99697182/173354504-94646596-bf10-43ad-8b4d-1eb7d570093b.png)

kemudian saya coba ulang

![image](https://user-images.githubusercontent.com/99697182/173354693-93e26ceb-7090-4162-b500-43039e1c2a68.png)

disini saya masih tidak bisa menjalankan apk nya karena status containernya exit, meskipun saya sudah mencoba mencari banyak referensi untuk start tapi masih tidak bisa

karena masih tidak bisa, jadi saya buat saja container baru dengan nama baru saja

![image](https://user-images.githubusercontent.com/99697182/173358931-3dc95b24-03f4-45ca-838d-7188bd3558e5.png)

![image](https://user-images.githubusercontent.com/99697182/173359669-e5f04c62-5954-4382-8ce2-fe214560de31.png)

14. Sekarang kita cek di browser

```
http://103.172.204.174:3333/login
```

![image](https://user-images.githubusercontent.com/99697182/173359819-ea0009e4-b20b-4eae-9a52-581fec711a11.png)



## Langkah 5 - Setup Gateway (Proxy & SSL)

1. Sekarang kita akan mengkonfigurasi gateaway nya dengan reverse proxy

![image](https://user-images.githubusercontent.com/99697182/173477311-ae63eeec-acf7-421b-925e-834a96cc9863.png)

2. Masukkan konfigurasi reverse proxy untuk link domain rahman.studentdumbways.my.id

![image](https://user-images.githubusercontent.com/99697182/173477193-8b4c297f-05c6-4115-903b-4f9d70df2823.png)

3. Masukkan konfigurasi reverse proxy untuk link domain api.rahman.studendumbways.my.id

![image](https://user-images.githubusercontent.com/99697182/173492870-f3e1b9b2-8fc9-470d-96f1-589ec6e0198f.png)

![image](https://user-images.githubusercontent.com/99697182/173493098-2b41a66d-77ab-464c-a3d3-9913583b169f.png)

4. Sekarang konfigurasi nginx.conf agar konfigurasi kita tadi terbaca oleh nginx

![image](https://user-images.githubusercontent.com/99697182/173493356-880e264b-257a-416e-84d6-c2600efa9e8f.png)

5. Tambahkan include folder wayshub tadi

![image](https://user-images.githubusercontent.com/99697182/173493302-d82314d9-f7e0-4cd7-9981-0a4bc92b6dbb.png)

6. Verifikasi hasil konfig dan restart nginx

![image](https://user-images.githubusercontent.com/99697182/173493469-c9a7ab24-f066-442f-9b6e-fafbcc7a84c6.png)

kita daftarkan dulu DNS nya :

![image](https://user-images.githubusercontent.com/99697182/173494763-c8dbac90-542d-4cd4-a0aa-fd9251c0f1dc.png)

![image](https://user-images.githubusercontent.com/99697182/173494815-3d32850c-c9d5-494a-8d89-a9324049b3b1.png)

kita boleh cek browser

```
http://rahman.studentdumbways.my.id/
```

![image](https://user-images.githubusercontent.com/99697182/173494628-6f063f73-8496-4ca4-a682-a5ffd4a6e3b0.png)


```
http://api.rahman.studentdumbways.my.id/
```

![image](https://user-images.githubusercontent.com/99697182/173494489-32348fc6-5ad6-42a7-b10c-453fe4dc477b.png)



7. Sekarang kita akan membuat SSL menggunakan certbot agar domain kita menjadi https dengan cara:

Install terlebih dahulu certbot nya

```
sudo snap install --classic certbot
```

```
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
![image](https://user-images.githubusercontent.com/99697182/173503475-d652c173-85d3-4cda-aec5-af0306479fff.png)

8. Sekarang kita akan membuat folder baru yaitu .secrets dan membuat file rahman.ini dan masukkan private key cloudflare kita

![image](https://user-images.githubusercontent.com/99697182/173503729-7ba25322-474d-447a-ac37-be9aac2070b1.png)

![image](https://user-images.githubusercontent.com/99697182/173503962-4e6a8cd9-e862-4050-b76c-db04e5d3a9fe.png)

![image](https://user-images.githubusercontent.com/99697182/173504426-a4c3dba0-3af8-4b77-98a2-0ca9fc6c7b11.png)

9. Sekarang jalankan certbot menggunakan perintah:

```
sudo certbot --nginx
```

![image](https://user-images.githubusercontent.com/99697182/173504742-fc3693d3-14fe-48cc-b3f5-7f7285b11b7f.png)

![image](https://user-images.githubusercontent.com/99697182/173504777-868805bc-1533-45b7-b5a6-30183b3cb44d.png)

10. Sekarang kita cek apakah sudah berhasil HTTPS atau belum

disini saya dapat error, Sepertinya error ini karena blum konek ke backendnya

![image](https://user-images.githubusercontent.com/99697182/173505423-6327486d-ded6-41df-a09a-34731e9bbf4f.png)

ketika saya clik esc maka keluar slide hitam

![image](https://user-images.githubusercontent.com/99697182/173509896-a8571b38-e652-4578-89ec-8a9308e46211.png)







link yang saya coba research selain menggunakan certbot :

[ini](https://youtu.be/oRMp2IzdS68) 

