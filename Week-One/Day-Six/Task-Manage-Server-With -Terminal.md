## Manage Server with Terminal


![image](https://user-images.githubusercontent.com/99697182/171647802-3dc99b4a-6f82-4c21-92ee-17331938cfd2.png)


## Apa itu terminal ?

Menurut saya terminal merupakan interface yang berfungsi sebagai penerjemah antara user dan os dalam menjalankan segala operasi, seperti memanipulasi file, data, folder dls.

## Jelaskan keuntungan menguasai Terminal

Menurut saya, sangat penting menguasai terminal, karena di sini saya sebagai pelajar devops harus bisa mengatur os berdasarkan printah yang berbasis CLI seperti ini, juga jika sudah bisa menguasainya, nantinya akan lebih mudah dalam menjalankan tugas sebagai devops dseperti meremote server dls.

## Buat sebuah file bash sederhana yang bertugas untuk update dan upgrade sistem
1. Kita meremoter server kita terlebih dahulu,

2. Buat file terlebih dahulu

3. masukan scriptnya dalam file tersebut

4. berikan izin dengan `chmod +x (nama file)`

![image](https://user-images.githubusercontent.com/99697182/171650269-3219143f-20cf-4a33-ba84-a62714480864.png)

5.Kemudian script akan berjalan seperti ini :

ini yang update ada echo yang muncul `apdet`

![image](https://user-images.githubusercontent.com/99697182/171650577-1cdf82cf-4be8-401f-8106-5983a0983daa.png)

ini yang upgrade, ada echo yang muncul `apgred`

![image](https://user-images.githubusercontent.com/99697182/171651655-6ab9568b-af43-4446-9b3b-48a591252491.png)

ada echo yang muncul `beres`

![image](https://user-images.githubusercontent.com/99697182/171653962-57ac47c2-ca43-4a0c-821c-3050e7e28fa2.png)



## Buat sebuah file bash sederhana yang bertugas untuk mencari file bernama sysctl.conf

1.buat file sysctl.conf dan taruh di dalam suatu directory

![image](https://user-images.githubusercontent.com/99697182/171678010-acf4e9ba-ef26-410f-b305-e875d5119b82.png)

2.Buat file bash nya untuk mencari

2.masukan script didalamnya

![image](https://user-images.githubusercontent.com/99697182/171678631-0593b696-7877-4371-a0ba-fe0894c911f8.png)

3.berikan izin dengan perintah `chmod +x (nama file)`

4.jalankan dengan `./`






## Buat sebuah file bash serderhana yang bertugas untuk membuat firewall port 22, 80 dan 443

pertama , install firewall terlebih dahulu :

![image](https://user-images.githubusercontent.com/99697182/171659661-eea990ec-34b2-4040-87e7-3ddd9695bf72.png)


1.Buat Sebuah file terlebih dahulu

2.masukan script kedalamnya

![image](https://user-images.githubusercontent.com/99697182/171658571-a8f1e550-a64c-41fb-98ac-1dad37b469fe.png)

3.berikan izin dengan perintah `chmod +x (nama file)`

4.jalankan dengan `./`

![image](https://user-images.githubusercontent.com/99697182/171658790-9fb8cf3b-580a-474d-be86-558ff1eeb169.png)

maka akan muncul berikut

![image](https://user-images.githubusercontent.com/99697182/171658964-51400bbd-d434-4f25-aec3-82287c2bd303.png)

5.kita bisa mengeceknya dengan `sudo ufw status`

![image](https://user-images.githubusercontent.com/99697182/171661729-06369144-70ef-44fb-b671-dd8eac9561e7.png)


# Selesai

# Sekian Dan terimakasih 



