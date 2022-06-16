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

## Dan Sekarang kita sambungkan juga dengan server aplikasi di tugas day 1 

Spek Server apk kemarin :

`App-Server : CPU : 2, RAM : 2, Disk : 20

Ip Public = 103.172.204.174

User 1 & Pwnya : ubuntu = Sembarang1

User 2 & Pwnya : app = app`

kita cek lokasi direktori yang akan di tuju 

![image](https://user-images.githubusercontent.com/99697182/173859706-8c486d2a-e6ba-4bfa-b264-8b8e9252d19c.png)

```
scp -r id_rsa id_rsa.pub app@103.172.204.174:/home/app/.ssh
```

![image](https://user-images.githubusercontent.com/99697182/173860054-f7917815-820b-4852-9655-3515cbe5ff28.png)

jika sudah, kita bisa cek dan pastikan ssh key nya terhubung 

![image](https://user-images.githubusercontent.com/99697182/173860401-dfd4d599-9dd0-4943-87c9-e1d185647306.png)

kemudian agar dikenali, kita masukan id_rsa.pub nya ke authorized_keys

![image](https://user-images.githubusercontent.com/99697182/173861013-284c3cd1-e0ee-4d51-a612-6c3e441d056d.png)
 
![image](https://user-images.githubusercontent.com/99697182/173861122-4870f493-7e2a-4975-952f-4deb97d09417.png)

# Step 6 - Membuat Manage Credensial 

Pertama kita masuk ke `dashboard` jenkins kita, kemudian kita klik `manage jenkins`, dan klik `manage credentials`, kemudian klik `jenkins`, klik `global credentials (unrestricted)`, klik `add credentials`,

dan isi yang di perlukan, di bagian bawah masukan private ssh key server aplikasinya

jika sudah klik ok

![image](https://user-images.githubusercontent.com/99697182/173865302-363ae410-8932-422b-ad7a-27c4e3e4492e.png)

nah disini kita sudah punya ssh key untuk masuk ke dalam servernya

![image](https://user-images.githubusercontent.com/99697182/173865725-b74ef42b-fa61-4bd5-b3c6-b9888db1036f.png)


# install ssh

![image](https://user-images.githubusercontent.com/99697182/173989485-e5ac5c2b-dbf0-4509-9327-f40a89c09a99.png)

![image](https://user-images.githubusercontent.com/99697182/173989509-d6c3e5a3-6e75-4209-b28b-217410eb7d95.png)

![image](https://user-images.githubusercontent.com/99697182/173989553-196992ed-33d2-490e-98dc-9eda60cb286a.png)

![image](https://user-images.githubusercontent.com/99697182/173989578-e0812962-38fa-4287-bfde-7e367eb9535e.png)

![image](https://user-images.githubusercontent.com/99697182/173989592-64d331c6-be1e-40ce-a6ab-1b3c60200e69.png)

disini saya restart

![image](https://user-images.githubusercontent.com/99697182/173990021-b4517057-a8bc-4457-9241-e375da036e0b.png)


# Step 7 - Membuat Repository di Github, push & meremotenya  

Pertama kita pastikan dulu server aplikasinya sudah ter-config dengan github

![image](https://user-images.githubusercontent.com/99697182/173867578-f9ad117e-2e63-482c-9286-699b1cc26654.png)

Kemudian Jangan Lupa untuk membuat Repository Untuk Apk Frontendnya 

![image](https://user-images.githubusercontent.com/99697182/173868210-2c8509d1-db48-4530-897a-cd194d99c35c.png)

Jangan Lupa juga untuk mengubah remotenya dan mengganti remotenya menjadi ssh

![image](https://user-images.githubusercontent.com/99697182/173868964-6e843526-4388-4caf-937d-bac8d0e165c9.png)

Kemudian Kita coba buat script yang bernama jenkinsfile

![image](https://user-images.githubusercontent.com/99697182/173869909-5771e9a6-d516-4127-a971-54921f1767e1.png)

dan masukan script ini :

```
def secret = 'server'
def server = 'app@103.172.204.174'
def directory = 'wayshub-frontend'
def branch = 'main'

pipeline{
    agent any
    stages{
        stage ('compose down &  pull'){
            steps{
                sshagent([secret]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker-compose down
                    docker system prune -f
                    git pull origin ${branch}
                    exit
                    EOF"""
                }
            }
        }
        stage ('docker build'){
            steps{
                sshagent([secret]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker-compose build
                    exit
                    EOF"""
                }
            }
        }
        stage ('docker up'){
            steps{
                sshagent([secret]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker-compose up -d
                    exit
                    EOF"""
                }
            }
        }
    }
}
```

![image](https://user-images.githubusercontent.com/99697182/173874834-6b5c6da4-3495-4cd7-b395-d50432b05297.png)

![image](https://user-images.githubusercontent.com/99697182/173874900-a545cbd9-3fea-4adf-ae18-3da3d90970c7.png)

setelah itu kita add, commit & push 

![image](https://user-images.githubusercontent.com/99697182/173875332-e27c5fa9-79b3-41c3-b456-8d182e5f0265.png)

kemudian kita cek

![image](https://user-images.githubusercontent.com/99697182/173875475-6c90a182-30f0-4ba7-a8d5-35b8d8ed851e.png)


# Step 8 - Membuat Pipe line

Kembali ke `dashboard` Jenkins, dan klik `New Item` , beri nama itemnya dan klik `pipeline` lalu klik `OK`

![image](https://user-images.githubusercontent.com/99697182/173872655-50619436-abd7-4f60-9c4a-60089031018f.png)

Kemudian Isi seperti gambar di bawah ini

![image](https://user-images.githubusercontent.com/99697182/173873439-14ffcd82-25b6-4c61-9ae6-01628f6b3448.png)

Kemudian Apply & Save 

![image](https://user-images.githubusercontent.com/99697182/173875056-3faed085-87a9-48ac-aa17-b64d46eb4b4d.png)

kemudian kita klik `Build Now`, dan dia akan otomatis nge-build, Untuk Build pertama harus manual

![image](https://user-images.githubusercontent.com/99697182/173875990-3ce772d0-4bb5-433d-8e8d-227143836562.png)

dan disini saya mendapat error

![image](https://user-images.githubusercontent.com/99697182/173876201-0517034d-6ddc-47a5-9527-2505dc14b718.png)


## Disini Saya Akan Mengalihkan Deploy Apilaksinya, Saya akan Arahkan Ke server jenkins Sesuai Instruksi baru

Pertama, Akan Saya Clone Aplikasinya di server jenkins 

```
git clone https://github.com/dumbwaysdev/wayshub-frontend
```

![image](https://user-images.githubusercontent.com/99697182/174014505-09431a28-c616-4bb2-8fbf-3dcf20419326.png)

Kemudian Saya buat repository baru dan meremotenya 

![image](https://user-images.githubusercontent.com/99697182/174014845-d454e6ea-8738-4f2b-9f66-c147e73c2045.png)

![image](https://user-images.githubusercontent.com/99697182/174015169-b3b2f183-5fba-48e3-b891-1a628e9417b9.png)

git config

![image](https://user-images.githubusercontent.com/99697182/174015866-a086cfa4-86a5-44d7-bc0f-c35dbee55301.png)

buat Script Jenkinsfile

![image](https://user-images.githubusercontent.com/99697182/174016861-d7c1efba-8d66-43e2-8f02-53098c9b9bcb.png)

```
def secret = 'rahman'
def server = 'rahman@103.55.38.183'
def directory = 'wayshub-frontend'
def branch = 'main'

pipeline{
    agent any
    stages{
        stage ('compose down &  pull'){
            steps{
                sshagent([secret]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker-compose down
                    docker system prune -f
                    git pull origin ${branch}
                    exit
                    EOF"""
                }
            }
        }
        stage ('docker build'){
            steps{
                sshagent([secret]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker-compose build
                    exit
                    EOF"""
                }
            }
        }
        stage ('docker up'){
            steps{
                sshagent([secret]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker-compose up -d
                    exit
                    EOF"""
                }
            }
        }
    }
}

```

![image](https://user-images.githubusercontent.com/99697182/174016689-efa4603e-344e-4155-9dcb-b61239c8d850.png)

![image](https://user-images.githubusercontent.com/99697182/174016760-eeef310f-9f12-4742-b917-dfddf25813af.png)

Push Ke github 

![image](https://user-images.githubusercontent.com/99697182/174017017-5348d346-9d1e-41e0-8d3d-11121f440773.png)

![image](https://user-images.githubusercontent.com/99697182/174017070-e4b5f125-7064-4733-9a3e-683f9b7e7707.png)

## Configure Pipline 

![image](https://user-images.githubusercontent.com/99697182/174017308-7bb2326c-fed7-414f-aebb-16a16a116afc.png)

![image](https://user-images.githubusercontent.com/99697182/174017499-e5aafeb0-f446-4fca-b10b-9ac056fa8c8d.png)

![image](https://user-images.githubusercontent.com/99697182/174017663-754d1ed2-a9b7-4816-a4ec-a675c101a50b.png)

Klik Build Now

![image](https://user-images.githubusercontent.com/99697182/174017915-54ba8b12-8803-4ed3-98c3-75daf94d0bf4.png)

Buat dockerfile dan docker-compose nya

![image](https://user-images.githubusercontent.com/99697182/174019206-0eee2a58-d812-4111-98f0-35ea9881ae84.png)

![image](https://user-images.githubusercontent.com/99697182/174019462-d79a8687-aa6e-4295-ad62-60133814f597.png)

![image](https://user-images.githubusercontent.com/99697182/174019630-8c4c4054-1b0a-4f5e-91a1-7373a20f8c6a.png)

![image](https://user-images.githubusercontent.com/99697182/174020230-744c26a6-1af5-4c08-b63e-dada23a5eeb7.png)

jangan lupa untuk push lagi

dan saya coba build ulang 

dan masih gagal

![image](https://user-images.githubusercontent.com/99697182/174020673-ba252069-8ff0-4fe2-a562-3c124e2cdffb.png)

dari sini saya mencari tau bisa gagal dari mana

saya coba2 buat network

```
ef681f9da3a852d481c6ac247b4699fbe27dd6088eaaf0c5e535dfbb91e200de
```

![image](https://user-images.githubusercontent.com/99697182/174046715-75c11fa5-da9d-471b-93af-6017ef61d8ee.png)














