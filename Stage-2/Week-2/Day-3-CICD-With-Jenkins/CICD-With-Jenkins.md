# CICD With Jenkins

# Step 1 - Membuat Server Di IDCH

Disini Saya membuat 1 Server Dengan Ket :

Public Ip = 103.55.38.183 , username = rahman, Pw= Sembarang1, CPU = 2, Ram = 2, Disk = 20 Gb

![image](https://user-images.githubusercontent.com/99697182/173757885-90dbdf71-d937-4667-9366-354518b271e5.png)
 
 dan Jangan lupa untuk selalu Update & Upgrade Servernya 

# Step 2 - Instalasi & Konfigurasi Jenkins

1. Install jenkins menggunakan perintah berikut :

```
sudo apt install openjdk-11-jdk
```

```
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
```

```
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \ 
/etc/apt/sources.list.d/jenkins.list'
```

```
sudo apt update
```
![image](https://user-images.githubusercontent.com/99697182/173762177-c4a9bf00-b9b3-421d-8887-89e8f5da67a8.png)

![image](https://user-images.githubusercontent.com/99697182/173765347-ecf0d521-5be1-47c0-aac8-46b02b495ba3.png)

Install Jenkins Menggunakan Perintah berikut :

```
sudo apt install jenkins
```

![image](https://user-images.githubusercontent.com/99697182/173765661-48a7a382-b213-41e2-8d0f-c74e6e0cc0f4.png)

2. Cek Statusnya menggunakan :

```
sudo systemctl status jenkins
```

3. Sekarang masuk ke jenkins menggunakan web browser dengan port jenkins 8080

```
103.55.38.183:8080
```








