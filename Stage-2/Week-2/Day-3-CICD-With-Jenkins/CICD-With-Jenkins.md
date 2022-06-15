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

disini, saya akan stop dulu jenkinsnya :

```
sudo systemctl stop jenkins 
```

![image](https://user-images.githubusercontent.com/99697182/173792142-991a3a87-d2d0-49cb-b8d9-1b4a7b9441df.png)

dan saya akan coba uninstall nya :

```
sudo apt-get remove --purge jenkins
```

![image](https://user-images.githubusercontent.com/99697182/173793755-01c39771-0395-47e2-a546-4a52540fb3e6.png)

kita cek 

```
sudo systemctl status jenkins
```

![image](https://user-images.githubusercontent.com/99697182/173794104-f5a11af1-6af5-41a4-aa20-1f20521d1ede.png)

# Step 3 - Install Docker

Setelah itu saya akan install docker

![image](https://user-images.githubusercontent.com/99697182/173795141-abe97657-ca15-4331-b44f-ce25f90cb663.png)

![image](https://user-images.githubusercontent.com/99697182/173794970-7ab39992-a000-47d6-ba45-30d45be03efc.png)

![image](https://user-images.githubusercontent.com/99697182/173798415-32993d1c-e260-47a9-aa8c-f0bda92038b7.png)

![image](https://user-images.githubusercontent.com/99697182/173798629-22e8c978-fac4-4444-bb96-60ef6b593738.png)

![image](https://user-images.githubusercontent.com/99697182/173798782-978c487e-99a1-43bb-a68c-0707c706c06f.png)

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

```
sudo chmod +x /usr/local/bin/docker-compose
```

```
docker compose --version
```

![image](https://user-images.githubusercontent.com/99697182/173802087-1116ef22-825e-4411-88df-4d60cba75709.png)

# Step 4 -Install Jenkins

Selanjutnya saya akan menginstall jenkins nya dengan tutorial [ini ](https://www.youtube.com/watch?v=pMO26j2OUME) dan artikel [ini](http://www.dimasrio.com/2017/04/setup-dan-install-jenkins-docker.html), dan saya mengambil images dockernya dari [ini](https://hub.docker.com/r/jenkins/jenkins)

```
docker pull jenkins/jenkins
```

![image](https://user-images.githubusercontent.com/99697182/173837538-2149b2b1-a12c-47db-84dd-44225800b383.png)

```
docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```

![image](https://user-images.githubusercontent.com/99697182/173799962-d3ada71f-af5b-4cb2-95dd-c914b7a200be.png)

```
docker ps
```

![image](https://user-images.githubusercontent.com/99697182/173800142-6d31dd83-47d6-4d8e-9482-6fa1ee569818.png)

```
docker logs a0b45e544dc0
```
ket : a0b45e544dc0 = container id

![image](https://user-images.githubusercontent.com/99697182/173800681-52c5eca3-45ed-4770-998f-cf6266200dbd.png)

![image](https://user-images.githubusercontent.com/99697182/173800709-8b74c040-cd09-43c1-949f-a5b7c03887c4.png)

kemudian copy initial setup nya = 7f4ed0dcd2524acbad364ed282e38633

dan kita buka browser `103.55.38.183:8080`, dan pastekan code nya setelah itu klik `continue`

![image](https://user-images.githubusercontent.com/99697182/173802819-464930f9-4278-4b1c-932e-a5041ec3dce8.png)

pilih install sugested plugin

![image](https://user-images.githubusercontent.com/99697182/173802945-5f6bb76a-c523-4bd7-98a4-a5bd1889aa44.png)

dan kita tunggu prosesnya : 

![image](https://user-images.githubusercontent.com/99697182/173804927-34ae245a-10db-4442-9d1a-ddabaf182901.png)

disini saya akan melakukan retry :

![image](https://user-images.githubusercontent.com/99697182/173805024-5d867144-508a-4b55-b8d8-53b9b9fd4cc4.png)

![image](https://user-images.githubusercontent.com/99697182/173805429-5bab78cc-53ba-42c0-8d87-9e4e2494dc7e.png)

dan ketika sudah loading selesai, semuanya berhasil terinstall, kita akan di minta untuk membuat user admin pertama  

![image](https://user-images.githubusercontent.com/99697182/173805853-7c381a7f-8f08-4148-bd03-82162b79e6d8.png)

![image](https://user-images.githubusercontent.com/99697182/173806088-1c689d8b-ac58-49f9-82b9-9b2daa96f8bb.png)

klik save & finish

![image](https://user-images.githubusercontent.com/99697182/173806143-c5bce7c3-bd60-4ad1-8616-710fb325276d.png)

and ready

![image](https://user-images.githubusercontent.com/99697182/173806266-314d09b8-31a8-439b-bbfe-e8a9251048c6.png)

# Step 5 - Menghubungkan Local dengan server jenkins dan dengan server aplikasinya juga, dengan mengirimkan ssh key-nya

Sebelum mengirimkannya, pastikan kalau lokal kita sudah terhubung dengan github kita

![image](https://user-images.githubusercontent.com/99697182/173843371-9e2bdcd3-aa36-4df7-8e51-de6fa51ec513.png)

kita cek lokasi direktori yang akan di tuju

![image](https://user-images.githubusercontent.com/99697182/173844998-81beaa9c-6905-4d2d-90ef-cf4cc810743a.png)

```
scp -r id_rsa id_rsa.pub rahman@103.55.38.183:/home/rahman/.ssh
```
![image](https://user-images.githubusercontent.com/99697182/173845229-4cc95ee2-5514-4a54-8c56-195036eb2a7a.png)

jika sudah, kita bisa cek dan pastikan ssh key nya terhubung

![image](https://user-images.githubusercontent.com/99697182/173845594-24153942-6ead-47ad-8ba0-ff682150cf00.png)

kemudian agar jenkinsnya dikenali, kita masukan id_rsa.pub nya ke authorized_keys 

![image](https://user-images.githubusercontent.com/99697182/173846071-14e65289-15b9-4174-8c60-6cbc5fd35ddf.png)

![image](https://user-images.githubusercontent.com/99697182/173846172-58a05a20-266f-4590-9c37-9dde4f3480c4.png)

`disini, salah satu manfaatnya, agar ketika kita mau meremote tidak usah menggunakan password lagi`

![image](https://user-images.githubusercontent.com/99697182/173847108-f172dc5f-12ff-4675-81b6-7f6e6908c0e5.png)


















