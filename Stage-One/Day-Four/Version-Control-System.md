# Task Version Control System

# Git
Menurut Saya, Git merupakan software untuk mengatur versi aplikasi, yang mana git ini mempunyai platform yaitu Github untuk mempermudah penggunanya. kini github bisa menjadi portofolio kita agar orang lain bisa mengetahui kualitas kita.

# Git Configuration 

## Step 1 - Konfigurasi Git dengan Github
Jika sudah menginstall git , maka selanjutnya masuk ke terminal , kemudian masukan perintah di bawah ini :

```
git config --global user.name ".................."
```

isi titik-titik diatas menggunakan username github 

```
git config --global user.email "................."
```

isi titik-titik diatas dengan menggunakan email di github

```
git config --list
```

perintah diatas untuk mengecek apakah sudah config atau blum 

![Img 1](assets/1.png)



# Step 2 - Menghubungkan SSH

1.SSH memungkinkan kita untuk melakukan push ke repository github tanpa login. Berbeda dengan cara yang biasa (melalui HTTPS), kita harus memasukkan username dan password setiap kali melakukan push. Tapi dengan SSH kita tidak akan melakukan itu lagi.

Untuk generate nya, masukan perintah berikut :

```
ssh-keygen
```

![Img 1](assets/2.png)


## SSH key Location

Jika kalian sudah menjalankan perintah sebelumnya maka kalian sudah berhasil untuk men-generate SSH key yang akan kalian gunakannya. Untuk lokasi SSH key yang sudah kalian generate tadi berada di .ssh/id_rsa.pub. Jika sudah lakukan copy pada SSH-key tersebut.

```
cat .ssh/id_rsa.pub
```
![Img 1](assets/3.png)

## Add new SSH to github settings

Tahap selanjutnya setelah kalian melakukan copy SSH-key adalah memasukkannya kedalam config github dengan membuka https://github.com/settings/keys.

Jika sudah langsung tekan saja di bagian New SSH key.
![Img 1](assets/4.png)

Setelah itu masukkan saja SSH key yang sudah kalian copy tadi kebagian key. Jika sudah Langsung saja save dengan menge-klik bagian Add SSH key.

![Img 1](assets/5.png)

![Img 1](assets/6.png)

## Check Connection

Jika kalian sudah melakukan semua step di atas maka kalian sudah berhasil meng-koneksikan local kalian dengan Github.

Untuk make sure apakah sudah terkoneksi kita bisa menggunakan perintah di bawah ini.

```
ssh -T git@github.com
```

![Img 1](assets/7.png)

Jika muncul teks seperti gambar diatas. maka kalian sudah berhasil mengkoneksikan local kalian dengan Github.



## Step 3 - Membuat 3 Buah Repository Untuk apk NodeJs, Golang & python

1. Pertama kita buat Repository NodeJs Terlebih dahulu dengan membuat direktorinya terlebih dahulu kemudian inisiasi git didalamnya menggunakan perintah berikut :

```
mkdir app-node-js
```

```
cd app-node-js
```

```
git init
```

![Img 1](assets/8.png)

2. Setelahnya kita membuat repository pada github juga, dengan masuk ke profile github dan klik "new repository" dibagian kanan kemudian beri nama repository nya dan klik "create new repository" di bagian bawahnya 

![Img 1](assets/9.png)

![Img 1](assets/10.png)

3. Jika muncul gambar dibawah ini berarti anda berhasil membuat repository NodeJs di Github, Kemudian Copy link " git remote add origin https://github.com/rahmaneffendi/app-node-js.git " untuk me-remote github dari lokal kita : 

![Img 1](assets/11.png)

4. Sekarang kita remote dengan perintah dibawah ini dengan paste kan link ssh tadi

```
git remote add origin https://github.com/rahmaneffendi/app-node-js.git
```

dan masukan perintah di bawah ini untuk mengecek nya 

```
git remote -v
```

![Img 1](assets/12.png)

nah, karena kita disni sudah belajar menggunakan ssh, kita akan remotenya menggunakan ssh, kita ganti yang tadinya menggunakan "https" menjadi ssh dengan perintah berikut :

```
git remote set-url origin git@github.com:rahmaneffendi/app-node-js.git
```

link diatas diambil dari github dengan cara klik pilihan "ssh" nya

![Img 1](assets/13.png)

![Img 1](assets/14.png)

5. Setelah Selesai me-remote, kita akan menambahkan file, aplikasi dan lain sebagainya ke dalam github melalui git,

ada 3 tahapan dalam git, yaitu : modify, staging dan commit.


tahap pertama yaitu modify, kita buat file yang akan kita tambahkan, apabila ada yang tidak perlu ditambahkan ke github, kita bisa menggunakan ".gitignore" dengan cara menuliskan nama filenya dalam git.ignore

![Img 1](assets/15.png)

![Img 1](assets/16.png)

Setelahnya Kita bisa cek Status Nya menggunakan"git status" apakah semuanya berjalan sesuai rencana :

![Img 1](assets/17.png)

6. Setelah Modify semua file, kita masuk ke tahap staging, 

sekarang kita add semua file yang ada dengan perintah 

```
git add .
```

setelah nya kita cek statusnya

![Img 1](assets/18.png)

7. Kemudian untuk tahapan selanjutnya yaitu commit atau production, kita akan menggunakan perintah berikut :

```
git commit -m "................"
```

titik-titik diatas diisi dengan pesan apa yang akan kita isi

```
git status
```

sebelum melakukan push, perintah diatas berfungsi juga untuk mengetahui pada branch apa kita berada


```
git push origin master
```

karena kita berada di branch master, kita push ke branch itu :

![Img 1](assets/19.png)

nah, dari gambar tersebut, dapat disimpulkan bahwa kita berhasil melakukan push

8. Kemudian kita cek github kita pakah benar sudah ter-push 

![Img 1](assets/20.png)

dan dari gambar tersebut itu berarti kita berhasil , yey.


9. Tahap Selanjutnya, kita akan membuat 3 buah branch baru, yaitu : Development, Staging, dan Production

Untuk Membuat Branch, Kita gunakan perintah :

```
git branch development
```

```
git branch staging
```

```
git branch production
```

dan perintah berikut untuk mengecek branch yang tersedia :

```
git branch -a
```

![Img 1](assets/21.png)

10. Setelahnya, Kita akan push ke semua branch, 

kita bisa berpindah branch dengan perintah 

```
git checkout (name branch)
```

Pertama Development 

![Img 1](assets/22.png)


Ke-2 Staging

![Img 1](assets/23.png)


ke-3 Production

![Img 1](assets/24.png)


11. Setelah selesai membuat branch dan push ke semua branch, sekarang kita akan cek di github kita apakah sudah berjalan sesuai rencana

![Img 1](assets/25.png)

dari gambar diatas, sudah terbukti bahwan branch nya sudah ada semua.

![Img 1](assets/26.png)

![Img 1](assets/27.png)

![Img 1](assets/28.png)

dari 3 gambar diatas, sudah terbukti bahwa di masing-masing branch, sudah ter-push juga semua filenya.

## Tugas NodeJs Sudah selesai, Sekarang kita akan melakukan hal yang sama untuk aplikasi Golang dan Python.


Gambar Dibawah ini Bukti untuk aplikasi Python

![Img 1](assets/30.png)


Gambar dibawah ini bukti Untuk aplikasi Golang

![Img 1](assets/29.png)



#Selesai 


















