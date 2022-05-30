# Day 3
# Build dan Running aplikasi NodeJS, Golang dan Python3 dan Jalankan Secara Daemon Menggunakan PM2

Apa Itu Aplikasi ?
![Img 1](assets/apk.jpg)
![Img 1](assets/apk1.jpg)

aplikasi merupakan suatu sub-class perangkat lunak yang menjalankan beberapa tugas dan fungsi untuk memudahkan user dalam suatu hal.


## Step 1 -  Instalasi, Build dan Run Aplikasi NodeJS

1. Install terlebih dahulu engine NodeJS dengan cara perintah berikut:
  
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```

![Img 1](assets/1.png)

keterangan : disini kita menggunakan nvm

nvm merupakan singkatan dari Node Version Manager. nvm adalah sebuah program yang akan membantu kita untuk menggunakan lebih dari satu versi Nodejs di dalam satu komputer.

```
exec bash
```

keterangan : Jika nvm belum terdeteksi gunakan perintah di atas ini

```
nvm install 16
```

![Img 1](assets/2.png)

keterangan : perintah di atas berguna untuk menginstall node.js dengan versi 16. Jika kalian ingin menggunakan node.js dengan version 14, maka Jalankan perintah nvm install 14.

```
nvm use 16  
```

![Img 1](assets/3.png)

keterangan : Untuk menggunakan node.js dengan versi 16

Jika tahapan di atas sudah kalian lakukan, maka kalian sudah berhasil untuk melakukan instalasi node.js. Untuk melakukan pengecekan kalian bisa menggunakan perintah di bawah ini.

```
node -v
```

```
npm -v
```

![Img 1](assets/4.png)

Selanjutnya buat direktori my-app-nodejs, kemudian kita akan menjalankan perintah npm init gunanya untuk menginisiasi project, Hasil dari kalian menjalankan perintah akan membuat file baru dengan nama package.json, package.json ini berisikan isi informasi dari aplikasi yang akan kalian buat.

```
npm init -y
```

![Img 1](assets/5.png)

Selanjutnya kita akan menginstall Express JS. Express JS adalah framework dari NodeJS yang dirancang secara fleksibel dan sederhana untuk membantu tahap pengembangan aplikasi back end. Menginstall express js dapat dilakukan menggunakan NPM dengan perintah berikut:

```
npm install express --save
```

![Img 1](assets/6.png)

Jika sudah buat file dengan nama index.js, lalu masukan script dibawah ini

```
nano index.js
```

```
const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`);
});
```

![Img 1](assets/7.1.png)

![Img 1](assets/7.2.png)

Jika sudah sekarang kita akan coba untuk menjalankan aplikasi sederhana yang sudah kita buat. Untuk menjalankan dapat menggunakan perintah berikut ini.

```
node index.js
```
 
![Img 1](assets/8.png)

Sekarang coba akses web browser kalian setelah itu kalian coba akses dengan localhost:3000

![Img 1](assets/9.png)

Selamat Praktek Nodejsnya Sudah Selesai



## Step 2 -  Instalasi, Build dan Run Aplikasi Golang

Pertama-tama sama seperti sebelumnya, Buat direktori baru untuk Golang dan kita harus mendownload engine-nya terlebih dahulu.

```
wget https://golang.org/dl/go1.16.5.linux-amd64.tar.gz && sudo su
```
kemudian masukan code server kamu sendiri, 

kemudian masukan script berikut ke nya

```
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.16.5.linux-amd64.tar.gz && exit
```

![Img 1](assets/10.png)

Selanjutnya masukkan path go pada .bashrc

```
sudo nano .bashrc
```

![Img 1](assets/11.png)

```
export PATH=$PATH:/usr/local/go/bin
```

![Img 1](assets/12.png)

Jika sudah sekarang dapat verifikasi go dengan cara berikut.

```
go version
```

di karenakan setelah mengecek dengan go version masih tidak terinstall, kemudian sistem menyaran kan untuk install dengan perintah berikut 

```
sudo apt install golang-go
```

setelah itu , go version bisa di lakukan 

![Img 1](assets/13.png)

Sekarang kita akan membuat aplikasi sederhana menggunakan go. Kalian dapat menjalankan beberapa perintah berikut ini.

Buat sebuah file dengan nama index.go.

Setelah itu masukkan script dibawah ini di dalam file index.go

```
package main

import "fmt"

func main() {
    fmt.Println("Hello World!")
}
```

![Img 1](assets/14.png)

Sekarang jalankan aplikasi go dengan menggunakan perintah berikut.

```
go run index.go
```

![Img 1](assets/15.png)

Jika aplikasi kalian ingin di build, maka jalankan perintah berikut ini.

```
go build index.go
```

![Img 1](assets/16.png)

Jika sudah jalankan aplikasi dengan menggunakan perintah berikut.

```
./index
```

![Img 1](assets/17.png)

Selamat, Praktek Golang Sudah Selesai

# Step 3 - Instalasi, Build dan Run Aplikasi Python3

Aplikasi python telah di install secara default pada Ubuntu, maka kita tidak perlu mendownload nya lagi, untuk mengecek apakah python3 sudah ada gunakan perintah berikut:

```
python3 --version
```

![Img 1](assets/18.png)

Sekarang kita install package manager dari python3. Kalian dapat menggunakan perintah berikut ini.

```
sudo apt install python3-pip
```

![Img 1](assets/19.png)

```
pip install flask
```

![Img 1](assets/20.png)

PIP adalah sebuah package management system yang biasa digunakan untuk mengatur dan menginstall package yang berisi modul-modul Python. PIP digunakan untuk menginstall Flask karena Flask ditulis dan dikembangkan dengan bahasa dan modul-modul pemrograman Python. Dengan menggunakan PIP, semua hal yang dibutuhkan untuk instalasi Flask akan diunduh dan dipasang dalam satu perintah.

Sekarang kita akan membuat aplikasi sederhana menggunakan Python3.

Kalian buat terlebih dahulu file dengan nama index.py. Lalu masukan script dibawah ini.

```
nano index.py
```

didalamnya masukan script ini 

```
from flask import Flask
app = Flask(__name__)
@app.route("/")
def helloworld():
    return "Hello World"
if __name__ == "__main__":
    app.run() 
```    

Jika sudah sekarang jalankan aplikasi dengan menggunakan perintah berikut ini.

```
python3 index.py
```

![Img 1](assets/21.1.png)

![Img 1](assets/21.2.png)



# Step 4 - Menjalankan Aplikasi Secara Daemon Menggunakan PM2

Lakukan instalasi PM2 dengan perintah berikut:

```
npm install pm2 -g
```

![Img 1](assets/23.png)


Kemudian masuk ke directory NodeJS dan start aplikasi NodeJS kita secara daemon dengan perintah berikut:

```
pm2 start index.js
```

![Img 1](assets/24.png)

Dan aplikasi NodeJS kita berhasil dijalankan di PM2 secara daemon seperti gambar berikut:

![Img 1](assets/25.png)



Sekarang kita akan menjalankan aplikasi python kita dengan cara masuk terlebih dahulu ke directory python dan masukkan perintah berikut:

```
pm2 start index.py --interpreter python3
```

Dan aplikasi Python3 kita berhasil dijalankan di PM2 secara daemon seperti gambar berikut:

![Img 1](assets/26.png)



Sekarang kita akan masuk ke aplikasi Golang kita dan menjalankannya secara daemon dengan perintah berikut:

```
pm2 start index.go
```

![Img 1](assets/27.png)


Sekarang kita akan mengecek status keseluruhan dengan perintah berikut apakah berjalan dengan baik atau tidak

```
pm2 status
```

![Img 1](assets/28.png)



# Step 5 - Localtunnel

install localtunnel dengan perintah berikut

```
npm install -g localtunnel 
```

Untuk Aplikasi python disini menggunakan port 5000 dengan perintah:

```
lt --port 5000
```

Untuk Aplikasi NodeJS disini menggunakan port 3000 dengan perintah:

```
lt --port 3000
```

![Img 1](assets/29.png)



![Img 1](assets/lt.js1.png)
![Img 1](assets/lt.js2.png)


![Img 1](assets/lt.py1.png)
![Img 1](assets/lt.py2.png)


# DONE















