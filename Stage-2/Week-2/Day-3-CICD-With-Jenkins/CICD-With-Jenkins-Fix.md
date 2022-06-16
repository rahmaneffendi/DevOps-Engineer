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

# Setup network jenkins

```
docker network create jenkins
```

![image](https://user-images.githubusercontent.com/99697182/174066077-0970c1e9-1ce6-4f56-80d6-5ae610f608c2.png)

```
b79a98ce3a40
```

```
b79a98ce3a40dacae449b7726695b10894ceaf23afae73f60aa362252be65d8e
```

# Setup work direktory dan run jenkins sebagai container

```
docker pull jenkins/jenkins
```

![image](https://user-images.githubusercontent.com/99697182/174066615-39ca3a96-b8dd-4b30-a73d-6e40f75188ad.png)

jalankan

```
docker container start (container id)
```

![image](https://user-images.githubusercontent.com/99697182/174067004-0213f747-e75a-4047-bec4-6b4c40dc0f16.png)


## Setelah ini saya sudah membuat revers proxy dan ssl certbot nya untuk jenkinsnya, dan saya mencoba masuk ke jenkinsnya 

![image](https://user-images.githubusercontent.com/99697182/174069250-5969eef6-9caf-4d97-8325-e843baf1edee.png)

![image](https://user-images.githubusercontent.com/99697182/174071230-27c40804-242d-4b5c-bed3-bedb9dabca9a.png)

![image](https://user-images.githubusercontent.com/99697182/174072291-aa435029-14fb-4799-8ce0-b2d01ae7026b.png)

ini tampilan awal jenkins nya 

![image](https://user-images.githubusercontent.com/99697182/174072380-1fb01704-96e2-4f5b-9fde-106a908f5ce5.png)

# Menghubungkan Github dengan mengirimkan ssh key

![image](https://user-images.githubusercontent.com/99697182/174073054-d1e539b0-3a09-4413-af28-c71cca2d1ab6.png)

buat authorized_keys dulu di lokal

![image](https://user-images.githubusercontent.com/99697182/174073425-463413d2-2b51-47fe-baef-bad7feec2f16.png)

![image](https://user-images.githubusercontent.com/99697182/174073356-c6bc1d5c-73cc-4402-b330-fbdf3ba09a58.png)

kemudian saya akan memberikan ssh dari local menuju server jenkins saya

```
scp -r id_rsa id_rsa.pub authorized_keys jenkins@103.214.113.82:/home/jenkins/.ssh
```

![image](https://user-images.githubusercontent.com/99697182/174074212-1c733fea-9b10-46ef-8aeb-2bbed532a368.png)

![image](https://user-images.githubusercontent.com/99697182/174074361-e106071d-fe4f-4209-9c2a-08e2b173c9c5.png)

# Create a job

![image](https://user-images.githubusercontent.com/99697182/174074602-d1eb9ecd-bc4a-4c14-ba78-be5d6dc61c9d.png)

![image](https://user-images.githubusercontent.com/99697182/174074688-d1e15ca7-472d-4bdc-b00d-e0a6f7b5eb82.png)

# Add Credential

![image](https://user-images.githubusercontent.com/99697182/174075538-cc29343d-13d4-4251-a593-b04a790a54a6.png)

![image](https://user-images.githubusercontent.com/99697182/174075507-6eb2bada-2b1b-42e1-9b7b-e407cbc8c139.png)

# Integrasi dengan git

Langkah pertama saya akan membuat repository baru pada github

![image](https://user-images.githubusercontent.com/99697182/174075928-b3a1e2a4-738c-4a23-b04e-40e7e4ea03a1.png)

![image](https://user-images.githubusercontent.com/99697182/174076437-7b36819b-df1e-4c56-aecb-3a8986e11a55.png)

![image](https://user-images.githubusercontent.com/99697182/174076583-9b779731-5b6d-4a97-8489-035cb02e2fc4.png)

# Build FE

Membuat jenkinsfile

![image](https://user-images.githubusercontent.com/99697182/174076867-2d57534c-adc5-45a4-9152-2330e4a898bd.png)

```
def secret = 'rahman'
def server = 'jenkins@103.214.113.82'
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

![image](https://user-images.githubusercontent.com/99697182/174077234-df09727f-a824-49b9-9dfe-cd14569a6769.png)

![image](https://user-images.githubusercontent.com/99697182/174077306-afb48b4f-a9d4-4f7b-96d0-0e1b2dad9d81.png)

![image](https://user-images.githubusercontent.com/99697182/174079070-207a6617-e21c-4c24-a6f5-b0f3e03d184f.png)

![image](https://user-images.githubusercontent.com/99697182/174078550-8abbc9d3-e59b-4d80-810c-ffe9a838a7b3.png)

![image](https://user-images.githubusercontent.com/99697182/174079017-54cc945e-4322-4876-a94b-66bad56d7db3.png)

![image](https://user-images.githubusercontent.com/99697182/174079189-bdc3e6d2-b353-4c53-8010-b25601eb4583.png)

# Configure Pipeline

![image](https://user-images.githubusercontent.com/99697182/174077588-e4c17eb2-4366-4f63-bfc7-2d5ec62f095d.png)

![image](https://user-images.githubusercontent.com/99697182/174077749-0bb69674-7a0c-44bb-b68a-e4c5df6df7a9.png)

![image](https://user-images.githubusercontent.com/99697182/174077823-cf857851-8126-494f-9eb9-abff5293cd0f.png)

klik build now 

dan saya gagal lagi

![image](https://user-images.githubusercontent.com/99697182/174079562-32a35cdd-ec75-4dda-bb42-ab298e038ca2.png)

disini saya coba install plugin

![image](https://user-images.githubusercontent.com/99697182/174080382-3bfed987-81da-46b2-a37c-82634c5be4f4.png)

![image](https://user-images.githubusercontent.com/99697182/174080888-7a51d7f8-5e1b-4f11-99fa-3638bc416ed6.png)

disini saya blum install compose nya

![image](https://user-images.githubusercontent.com/99697182/174083110-c959e1b1-a55b-4abd-ac21-b5c685e3ce25.png)

![image](https://user-images.githubusercontent.com/99697182/174082115-91484694-3204-4079-8620-bf46bd3b1a57.png)

disini kita berhasil

![image](https://user-images.githubusercontent.com/99697182/174083778-b32dff40-7577-4f84-81eb-7411af2a1619.png)

Sudah berhasil di build dan deploy selanjutnya saya akan cek image yang barusan dibuat pada docker

![image](https://user-images.githubusercontent.com/99697182/174084212-386baff1-af42-4849-b1b6-3569d751e8b1.png)

![image](https://user-images.githubusercontent.com/99697182/174084516-0e4f44b5-59b6-4117-b05d-90117f16204c.png)

Kemudian cek melalui web browser

```
103.214.113.82:3030
```
![image](https://user-images.githubusercontent.com/99697182/174084676-b1eb7a20-091e-4925-8ba4-dfd9797384e5.png)

# Webhook for Jenkins

![image](https://user-images.githubusercontent.com/99697182/174085409-7b7be76c-4f97-4f57-a832-2161bb3fd794.png)

masukan link dan save 

![image](https://user-images.githubusercontent.com/99697182/174085722-c3fb4de6-74d2-4635-af27-2c36dea9685b.png)

![image](https://user-images.githubusercontent.com/99697182/174085810-32b84ae7-fdb3-4049-9da7-db54e1ccf9c7.png)


