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

14. Sekarang kita cek di browser



## Langkah 5 - Setup Gateway (Proxy & SSL)
