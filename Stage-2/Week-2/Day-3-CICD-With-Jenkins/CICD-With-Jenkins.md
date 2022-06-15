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

![image](https://user-images.githubusercontent.com/99697182/173768942-41534acf-74b3-4722-9054-16dacb32c623.png)

3. Sekarang masuk ke jenkins menggunakan web browser dengan port jenkins 8080

```
103.55.38.183:8080
```
![image](https://user-images.githubusercontent.com/99697182/173769515-18a5ca56-ad5a-4843-85e2-eafcad9ba831.png)

4. Ikuti perintah ini dengan masukan administrative password dengan cat seperti berikut:

![image](https://user-images.githubusercontent.com/99697182/173769933-4db44769-055b-491b-9620-9956d0d85fe2.png)

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

![image](https://user-images.githubusercontent.com/99697182/173770100-b3d6608a-4760-479b-ba2f-babdc7160453.png)

Copy paste Kode tesebut ke jenkins tadi

```
bf329c3346cd43b79a689b23a3dd0c13
```

![image](https://user-images.githubusercontent.com/99697182/173770263-73441f31-d49c-42fc-b19a-027ae867e44b.png)

Kemudian klik continue

5. kemudian kita pilih install suggested plugin

![image](https://user-images.githubusercontent.com/99697182/173770426-ecc783b1-794c-4edf-847c-d298ff1680a4.png)

dan akan loading, usahakan koneksi nya lancar, agar proses loading tidak mengalami resiko gagal ataupun mengulang

![image](https://user-images.githubusercontent.com/99697182/173773767-f2920263-25a6-4fb3-aab2-06f703ba44bb.png)

disini saya dapat failed , dan akan saya retry 

![image](https://user-images.githubusercontent.com/99697182/173774067-0ab1a332-93b3-40e7-afbd-973704b85d46.png)

![image](https://user-images.githubusercontent.com/99697182/173774901-bde9632a-d23f-4f33-9cc2-4ac358bbe6a6.png)

dan disini saya gagal lagi, akan saya retry lagi 

![image](https://user-images.githubusercontent.com/99697182/173774984-edcf7ad6-9ce5-412d-83a4-f8c080e740d3.png)

gagal lagi, akan saya retry lagi

![image](https://user-images.githubusercontent.com/99697182/173775908-f0ba81bd-5051-4b19-80e6-2741ce5c178e.png)

### Cat : Dari ada instruksi untuk instalasi jenkins nya menggunakan docker


