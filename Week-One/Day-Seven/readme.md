# task

# Instruksi

`CAUTION
Pastikan untuk melakukan screenshot step by step yang dilakukan, untuk digunakan sebagai dokumentasi tugas.`

Setelah mempelajari terkait web server, reverse proxy dan load balancing maka buatlah konfigurasi dengan ketentuan sebagai berikut:

![image](https://user-images.githubusercontent.com/99697182/171768607-6e752ff8-bd1a-4bba-9dd3-a75644e40166.png)

# Ketentuan

Jalankan 1 aplikasi yang sama pada 2 buah server

Buatlah sebuah konfigurasi reverse proxy pada server gateway (nginx)

Buatlah sebuah konfigurasi load balancing pada server gateway (nginx)

Aplikasi dapat di akses menggunakan domain virtual dan otomatis load balance ke 2 aplikasi tersebut

# Pengumpulan

Pastikan untuk mengerjakan tugas mingguan pada medium.com.

Tulis step-by-step yang telah Anda lakukan secara detail dan sertakan screenshot setiap prosesnya.

Setelah menyelesaikan tugas, silakan publish artikel yang sudah dibuat.

Referensi:

Medium = https://ebook-devops.vercel.app/Getting-Started/Medium/Medium

# Project Management
Tambahkan deskripsi berikut ke dalam kanban pada project management Anda

Konfigurasi web server dengan reverse proxy dan load balancing hingga dapat di akses melalui browser.

```
- [ ] Definisikan apa itu Web Server menurut pemahamanmu
- [ ] Buatlah 3 buah server (server gateway, server aplikasi1, server aplikasi2)
- [ ] Instal web server nginx pada server gateway
- [ ] Instal aplikasi nodejs pada server aplikasi1 dan server aplikasi2
- [ ] Buatlah sebuah konfigurasi reverse proxy pada server gateway yang mengarah ke server aplikasi1 dengan domain dumbways.xyz
- [ ] Buatlah sebuah konfigurasi load balancing pada server gateway yang mengarah ke server aplikasi2 dengan domain loadbalance.dumbways.xyz
```

Referensi:

Membuat GitHub Project = https://ebook-devops.vercel.app/Getting-Started/Project-Management/Make-Project-Management

Manage GitHub Issue = https://ebook-devops.vercel.app/Getting-Started/Project-Management/Issue-Dan-Status-Project

# Diskusi
Silakan diskusikan terkait kendala atau kesulitan selama pembelajaran pada platform diskusi (slack/talk.ink) dengan membuat thread, misalnya "Introduction DevOps: problem cannot connect to network in VMware"
