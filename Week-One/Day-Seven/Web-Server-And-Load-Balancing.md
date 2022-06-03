# Task

## Apa itu Web Server?

Menurut Saya, Web server merupakan suatu software yang memberikan layanan berbasis data dan berfungsi untuk menerima request dari client berupa http atau htpps yang dusebut juga web browser kemudian memberikan respond dengan memberikan halaman web yang secara umum berupa halaman html.

# Step 1 - Install VM

Kita install Virtual Machine kita terlebih dahulu, disini saya mencoba menggunakan multipass, kita bisa menggunakan link `https://multipass.run/` ini untuk melihat langkah-langkahnya.

![image](https://user-images.githubusercontent.com/99697182/171821089-da74b4fd-ab8b-459a-b548-134e5e93fa07.png)

Kemudian Kita buat servernya menggunakan perintah `multipass launch --name foo`

![image](https://user-images.githubusercontent.com/99697182/171837821-a2a2e59a-ce50-41e8-8725-d96abdd04cfd.png)

kemudian kita switch atau berpindah ke servernya dengan perintah `multipass shell .....`

![image](https://user-images.githubusercontent.com/99697182/171840561-d40dc4fa-4bc2-477b-86b0-d826f38fcf7e.png)






# Step 2 - 

# Ketentuan

Jalankan 1 aplikasi yang sama pada 2 buah server

Buatlah sebuah konfigurasi reverse proxy pada server gateway (nginx)

Buatlah sebuah konfigurasi load balancing pada server gateway (nginx)

Aplikasi dapat di akses menggunakan domain virtual dan otomatis load balance ke 2 aplikasi tersebut

