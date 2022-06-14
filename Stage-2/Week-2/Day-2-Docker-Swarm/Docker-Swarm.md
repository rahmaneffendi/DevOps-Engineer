# Docker Swarm

# Langkah 1 - Buat Servernya Dulu

disini saya membuat 3 buah server:

dengan user dan pw  yang sama semuanya : test =Sembarang1

1. Manager-rahman, public ip = 103.171.84.101

2. Worker1-rahman, public ip = 103.186.1.174

3. Worker2-rahman, public ip = 103.186.0.4

![image](https://user-images.githubusercontent.com/99697182/173568747-2c68d72e-e86c-453a-a7b6-6582b945b8d4.png)

![image](https://user-images.githubusercontent.com/99697182/173568831-ed21ceba-beb0-482c-8677-c3da8fa824a9.png)

![image](https://user-images.githubusercontent.com/99697182/173568858-34c42e9d-d00b-4c94-967d-ed99e611757f.png)

jangan lupa untuk melakukan persiapan :

```
sudo apt update; sudo apt upgrade
```

```
docker -v
```

```
docker-compose -v
```

```
sudo usermod -aG docker (user)
```

```
logout
```

```
ssh user@ip
```

```
docker ps
```

# Langkah 2 - Melakukan Inisiasi Server

1. Jika sudah melakukan instalasi docker dan docker compose lalu inisiasi server manajer dengan perintah berikut:

```
docker swarm init --advertise-addr 103.171.84.101
```

![image](https://user-images.githubusercontent.com/99697182/173590338-faaf0b32-9904-40f0-8a5a-806f621eaf7f.png)

2. Join server worker kalian ke server manajer dengan perintah yang diberikan di step 3, copy dan jalankan di server worker kalian

```
docker swarm join --token SWMTKN-1-2xqvi55x47oi4txjxbwrihwtf54e8wie53rtpqcqvc15iqltzw-dzzhrgqznftrqjnwmzz7tw04r 103.171.84.101:2377
```

Join server worker 1

![image](https://user-images.githubusercontent.com/99697182/173591048-af1c3c61-c9db-4f21-b09f-e44174c55cf4.png)

Join server worker 2

![image](https://user-images.githubusercontent.com/99697182/173591242-03c24903-0e8e-4592-90b8-0ae5dd7ff17f.png)

3. Untuk memeriksa apakah worker sudah join ke server manager gunakan perintah berikut:

```
docker node ls
```

![image](https://user-images.githubusercontent.com/99697182/173591746-ad1a53da-5f76-43d6-a879-4fc88c0d652e.png)

# Langkah 2 - Docker Swarm Commands

1. Untuk membuat docker service gunakan perintah berikut:

```
docker service create --replicas 1 --name helloworld alpine ping google.com
```

![image](https://user-images.githubusercontent.com/99697182/173593350-9a65babf-8ea1-40c5-a014-05c9c253858e.png)

2. Kita lihat service nya sudah berjalan atau blum dengan :

```
docker service ps helloworld
```

```
docker ps
```

dan dia terdeploy di managernya langsung

![image](https://user-images.githubusercontent.com/99697182/173594180-a7f45d9d-148e-47cb-826e-fd810ac205ff.png)

3. Kemudian Untuk scale aplikasi gunakan perintah berikut:

```
docker service scale helloworld=5
```
![image](https://user-images.githubusercontent.com/99697182/173594910-8e22d6a2-5061-418f-9740-e9cd14c615f5.png)

Kemudian Kita cek di seluruh servernya :

```
docker ps
```

Manager

![image](https://user-images.githubusercontent.com/99697182/173595075-7989bc68-a957-4048-8a00-0557233e16ed.png)

Worker1

![image](https://user-images.githubusercontent.com/99697182/173595269-2b3fadad-7e80-4acd-97a9-c3469c9f9bc0.png)

Worker2

![image](https://user-images.githubusercontent.com/99697182/173595413-99163bc1-a280-417e-a20d-0341b251e1b2.png)

4. Untuk melihat konfigurasi container gunakan perintah berikut:

```
docker service inspect helloworld
```

![image](https://user-images.githubusercontent.com/99697182/173596012-8ef93571-3d9a-4d86-a7e4-e90d5c9eb382.png)

5. Kemudian Untuk me-remove service gunakan perintah berikut:

```
docker service rm helloworld
```

![image](https://user-images.githubusercontent.com/99697182/173596687-ca13e100-461f-4034-9932-512ef686ae00.png)

# Langkah 3 - Menuju Ke Aplikasinya 

1. clone aplikasinya terlebih dahulu

```
git clone https://github.com/sgnd/dumbways-docker-microservices.git
```

![image](https://user-images.githubusercontent.com/99697182/173597588-39732d10-312c-40b8-9e05-cdc2f884f219.png)

![image](https://user-images.githubusercontent.com/99697182/173597815-a56fdb9a-8100-4890-a581-5ccbc29bb6fa.png)

2. Buat/edit composenya :











