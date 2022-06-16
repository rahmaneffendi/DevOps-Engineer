# Bismillah

# CI/CD JENKINS

## Apa itu CI/CD?

CI/CD atau Continuous Integration dan Continuous Deployment merupakan metode untuk mengirimkan perubahan code secara terus menerus hingga aplikasi dapat release ke publik dengan otomatis.

Continuous integration merupakan proses otomatis untuk memastikan semua code sudah berjalan dengan baik, jika terjadi error maka proses tersebut akan diulangi dari awal hingga code tersebut sudah tidak ada error.

Continuous deployment merupakan proses otomatis agar aplikasi yang telah siap di kirim ke server hingga aplikasi dapat diakses secara public.

## Jenkins

Jenkins merupakan sebuah automasi server berbasis open source yang ditulis menggunakan bahasa Java. Salah satu kegunaan Jenkins adalah untuk mengimplementasikan Continuous Integration dan Continous Delivery atau biasa yang disebut CI/CD proses. lebih jelasnya jenkins memudahkan kita untuk Proses seperti testing, building dan deployment yang dapat dijalankan secara otomatis.

# Membuat VPS menggunakan [IDCloudhost](https://github.com/pinoezz/DevOps/blob/master/Stage-2/Week-2/Day-3/idcloudhost.com)

saya akan membuat server dengan os ubuntu 20.04lts yang nantinya akan digunakan untuk jenkins dalam docker

user = jenkins, pw = Sembarang1, public IP : 103.214.113.82

![image](https://user-images.githubusercontent.com/99697182/174062034-d384eb7e-1a91-4e66-be84-96982ea0c998.png)

# Install Docker

```
sudo apt  install docker.io
```

![image](https://user-images.githubusercontent.com/99697182/174063955-2b2808ae-6145-437b-bc56-0cd38fb9b681.png)

![image](https://user-images.githubusercontent.com/99697182/174064219-1477b2fc-0f33-4b6f-86e6-9cdae8aed8fa.png)

Kemudian saya akan memberikan akses root kepada docker supaya saat menjalankan docker tidak perlu menggunakan sudo

```
sudo usermod -aG docker $user
```
![image](https://user-images.githubusercontent.com/99697182/174064309-e3d038c2-db02-47b4-9948-3c0da18fa372.png)

Kemudian relogin

Login Docker

```
docker login
```

![image](https://user-images.githubusercontent.com/99697182/174064482-2d217f2a-c784-4edb-bcef-48f42fd0de8a.png)

# Install Jenkins on Docker

```
docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk11
```

![image](https://user-images.githubusercontent.com/99697182/174064850-dbe973ba-d66c-4595-a53e-ecdc8a6d439e.png)

![image](https://user-images.githubusercontent.com/99697182/174064962-15ed23f2-5a3b-46d7-8e18-4613dfd15664.png)

disini saya mendapatkan code untuk mengakses jenkinsnya

```
2eb05dc836ea49c1b9ee5f23fd700c6a
```

# Install Nginx

```
sudo apt install nginx
```
![image](https://user-images.githubusercontent.com/99697182/174065384-c6cf0c28-45da-4ddf-9bfd-26ffdeedc199.png)

Kemudian cek pada web browser

![image](https://user-images.githubusercontent.com/99697182/174065630-3fbc003e-ba5a-4750-b348-96dead6bb5a8.png)















