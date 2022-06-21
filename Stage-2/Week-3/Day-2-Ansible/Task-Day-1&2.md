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

saya akan memperbaikinya di inventory

![image](https://user-images.githubusercontent.com/99697182/174779918-5f837af0-4863-4028-92e8-4a432c203d37.png)

disini saya mengubah usernya 

![image](https://user-images.githubusercontent.com/99697182/174780010-b531cc80-005e-4f68-852c-4c2be6b3deba.png)

kita cek lagi dan bisa

![image](https://user-images.githubusercontent.com/99697182/174780173-e6b92163-90c2-4634-a395-0da25a25fe42.png)

# Install Nginx Pada Server Monitoring

disini saya tidak menghiraukan server app terlebih dulu 

![image](https://user-images.githubusercontent.com/99697182/174781284-1f700801-3cb4-4b2f-9229-6db39264a210.png)

![image](https://user-images.githubusercontent.com/99697182/174781347-1bf4ccca-b82d-40ed-a963-dfd5d555af12.png)

Buat file baru bernama nginx.yml

```
- hosts: all
  become: yes
  gather_facts: true
  tasks:
        - name: 'install nginx'
          apt:
            name:
              - nginx
            state: latest
```

Kemudian saya akan install nginx.yml nya

![image](https://user-images.githubusercontent.com/99697182/174781756-bb0f7c8e-8894-42d6-b8f6-9092de71281c.png)

![image](https://user-images.githubusercontent.com/99697182/174782412-a7eb482b-c4c2-430c-9a5e-42f68ecb5e70.png)

kita cek apakah sudah benar syntaxnya :

```
ansible-playbook --syntax-check nginx.yml
```

disini saya dapat error

![image](https://user-images.githubusercontent.com/99697182/174783489-7b751dba-b81d-40b8-a5e6-2d29abf546a7.png)

ketika saya cek ternyata nama host nya yaitu all

![image](https://user-images.githubusercontent.com/99697182/174800526-87ebe478-688d-446d-82b5-c4698afbf9ab.png)

saya coba ubah

![image](https://user-images.githubusercontent.com/99697182/174800652-a6f7f86d-1068-49f5-be4c-bf0b42837565.png)

dan ternyata masih error, sepertinya bukan disitu masalahnya

![image](https://user-images.githubusercontent.com/99697182/174800788-6ce50719-1e94-4eaf-8990-1163f6688447.png)

Sekarang saya mencoba menambah spasi di name bawah apt

![image](https://user-images.githubusercontent.com/99697182/174801348-cebbf65d-cb6e-4a78-ab4a-8e74edaec6d0.png)

saya cek lagi, dan masih error

![image](https://user-images.githubusercontent.com/99697182/174801507-902e013c-5ed3-41d4-8254-a39eaee8ae4f.png)

setelah melakukan beberapa percobaan dan input ulang menggunakan VSCODE, akhirnya dia bisa 

![image](https://user-images.githubusercontent.com/99697182/174804366-e9cd5a8f-5ab8-46b6-87c5-09cd69b12c49.png)

kemudian install nginx nya 

```
ansible-playbook nginx.yml
```

![image](https://user-images.githubusercontent.com/99697182/174805006-5fe7b1ce-4208-4094-84f8-80e81154ccec.png)

kemudian kita cek pada browser 

![image](https://user-images.githubusercontent.com/99697182/174805913-98f39f55-392b-4de7-9f0a-ea256828ba5b.png)

# Install Docker pada server

Berikut Referensi Docker Yang akan kita lihat

https://docs.docker.com/engine/install/ubuntu/

https://docs.docker.com/compose/install/compose-plugin/#installing-compose-on-linux-systems

buat direktori docker.yml dan masukan script download docker nya

![image](https://user-images.githubusercontent.com/99697182/174811549-a8e0dcdf-c437-44bb-975f-e45fd3c808f8.png)

```

```
























