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

Jangan lupa untuk mengubah hak akses file .pemnya menjadi read only kemudian test mengoneksikan ke server

![image](https://user-images.githubusercontent.com/99697182/174777729-5c60f154-0be8-4f7b-b74e-4faa36ce88fb.png)

# Setup Ansible

Buat directory baru dan file baru bernama Inventory yang berisi isi dari server kita nantinya yang akan dilakukan otomisasi

![image](https://user-images.githubusercontent.com/99697182/174775480-79c6174f-254f-4209-bec9-96e4ee70dbd8.png)

![image](https://user-images.githubusercontent.com/99697182/174776587-966a029c-f146-4672-88f5-5bb88eb28c20.png)

Buat file baru yang bernama ansible.cfg, file ini berfungsi untuk sebagai penghubung antara server yang ada di inventory ke local kita dengan private key tadi

```
[defaults]
inventory = Inventory
private_key_file = sshkey.pem
```
![image](https://user-images.githubusercontent.com/99697182/174778578-871c951e-ecc9-49a1-b418-aeb0eb4386f4.png)

![image](https://user-images.githubusercontent.com/99697182/174778754-d9a8ad75-4a57-4544-b680-c3e24eaef433.png)

Cek koneksi ke server tujuan dengan menggunakan perintah berikut:

```
ansible all -m ping
```

sepertinya disini saya dapat error

![image](https://user-images.githubusercontent.com/99697182/174779186-f86e7432-968b-45c5-8d75-13e42bc8e14e.png)




















