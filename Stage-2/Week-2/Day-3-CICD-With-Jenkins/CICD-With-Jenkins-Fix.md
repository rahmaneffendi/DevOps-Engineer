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

Kemudian saya akan memberikan akses root kepada docker supaya saat menjalankan docker tidak perlu menggunakan sudo

```
sudo usermod -aG docker $user
```

Kemudian relogin

Login Docker

```
docker login
```
















