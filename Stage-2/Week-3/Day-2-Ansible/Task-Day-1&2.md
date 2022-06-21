# Ansible 

Ansible adalah sebuah tool Automation. Ansible dapat membantu melakukan instalasi, deployment, bahkan mengupdate server. ansible dapat membantu seorang devops atau sistem administrator untuk melakukan otomasi di servernya.



# Buat Server

Disini saya membuat 2 buah server

1. Server Monitoring

user : Moni, PW : Sembarang1, IP : 103.55.37.194

2. Server App

user : app, PW : Sembarang1, IP : 103.55.37.191

![image](https://user-images.githubusercontent.com/99697182/174741093-d53cefc6-cac2-4421-9735-b4274b1f927d.png)

![image](https://user-images.githubusercontent.com/99697182/174741032-041c5948-0e9e-4e1a-bd59-92d1d09cfc57.png)

# Install Ansible Di Local

kita bisa menginstalnya dengan perintah berikut

```
sudo apt update; sudo apt upgrade
```

```
sudo apt install software-properties-common
```

```
sudo add-apt-repository --yes --update ppa:ansible/ansible
```

```
sudo apt install ansible
```

disini saya sudah mengintallnya, jadi kita langsung cek saja

```
ansible --version
```

![image](https://user-images.githubusercontent.com/99697182/174758817-983db6b8-9d22-44ec-b73e-f87a54399432.png)

# Sebar ssh key ke lokal dan server lain

Pertama Buat directory baru di lokal khusus untuk ansible

![image](https://user-images.githubusercontent.com/99697182/174772794-5c83fee2-6952-45a6-8177-c9fa13772c39.png)

Pertama install ssh key nya di server 

![image](https://user-images.githubusercontent.com/99697182/174770403-6247656f-a4f4-4fd0-a3f3-da8b8b72b7a6.png)

Copas id_rsa.pub di file authorized_keys

![image](https://user-images.githubusercontent.com/99697182/174770920-6e284c38-7fd0-46df-99b3-5a26211cb8a6.png)

![image](https://user-images.githubusercontent.com/99697182/174770875-6cc133bc-3056-47f2-8f94-f2edf564beb6.png)

![image](https://user-images.githubusercontent.com/99697182/174771216-d946d768-b408-4f75-a46d-0b4b82da6632.png)

Kirim private key ke setiap server agar manage lebih mudah

```
scp -r .ssh app@103.55.37.191:/home/app
```

![image](https://user-images.githubusercontent.com/99697182/174772136-692d2ed4-333b-4b8d-82c1-201df136f2f5.png)

![image](https://user-images.githubusercontent.com/99697182/174772299-9b935b40-9d0c-41e1-a892-68bec855c67c.png)

Copy private key server dan paste di direktori ansible di file baru yang bernama sshkey.pem di local/ansible

![image](https://user-images.githubusercontent.com/99697182/174773543-916a1ea2-5b59-41b7-948a-1222b3a52d5a.png)

![image](https://user-images.githubusercontent.com/99697182/174773740-9525ddb7-b27b-4571-be36-f8a5199740df.png)

![image](https://user-images.githubusercontent.com/99697182/174773673-19b5ec47-d322-483d-850b-f9e1d7ec53e0.png)

# Setup Ansible

Buat directory baru dan file baru bernama Inventory yang berisi isi dari server kita nantinya yang akan dilakukan otomisasi

![image](https://user-images.githubusercontent.com/99697182/174775480-79c6174f-254f-4209-bec9-96e4ee70dbd8.png)

![image](https://user-images.githubusercontent.com/99697182/174776587-966a029c-f146-4672-88f5-5bb88eb28c20.png)



















