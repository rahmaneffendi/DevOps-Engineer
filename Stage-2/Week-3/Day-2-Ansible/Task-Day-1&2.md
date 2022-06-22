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
- hosts: all
  become: yes
  gather_facts: yes
  tasks:
         - name: 'update'
           apt:
            update_cache: yes

         - name: 'upgrade'
           apt:
            upgrade: dist

         - name: 'install dependencies'
           apt:
             name:
             - ca-certificates
             - curl
             - gnupg
             - lsb-release

         - name: 'add docker gpg key'
           apt_key:
            url: https://download.docker.com/linux/ubuntu/gpg

         - name: 'add repository docker'
           apt_repository:
             repo: deb  https://download.docker.com/linux/ubuntu focal stable

         - name: 'install docker engine'
           apt: 
            name:
             - docker-ce
             - docker-ce-cli
             - containerd.io
             - docker-compose-plugin

         - name: 'update'
           apt:
            update_cache: yes

         - name: 'install docker-compose'
           shell: curl -SL https://github.com/docker/compose/releases/download/v2.6.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose


         - name: 'set permision for docker'
           shell: sudo chmod +x /usr/local/bin/docker-compose
        
         - name: 'docker without sudo'
           shell: sudo usermod -aG docker moni

```

![image](https://user-images.githubusercontent.com/99697182/174814097-b002f15e-f57f-48c6-8376-8a42812c342c.png)

![image](https://user-images.githubusercontent.com/99697182/174814256-1ce6a714-af2b-4daa-8d7e-327b37b89701.png)

kita cek syntaxnya 

![image](https://user-images.githubusercontent.com/99697182/174813975-b655733a-16e3-4273-8e44-156c724ba9f5.png)

kemudian kita install 

![image](https://user-images.githubusercontent.com/99697182/174815308-3f5aaa0f-612e-4393-b0cd-beb2cd577143.png)

![image](https://user-images.githubusercontent.com/99697182/174815409-fc54b535-0861-4d49-9c52-bf896fef2871.png)

Kemudian Kita cek pada server moni

![image](https://user-images.githubusercontent.com/99697182/174816140-693ee132-0a51-4475-b820-299c977aaa75.png)

![image](https://user-images.githubusercontent.com/99697182/174827706-c07d845a-1692-4ffe-b1f6-6f222c1eac73.png)

## Kemudian Kita install pada Server App

ket: Sebetulnya kita bisa install sekaligus, hanya saja saya lupa, jadi disini saya akan mencoba lagi dengan install sekligus

pertama kita edit File Inventory kita 

![image](https://user-images.githubusercontent.com/99697182/174817141-95a076a3-8249-4a9d-889e-a570b9f29dc6.png)

![image](https://user-images.githubusercontent.com/99697182/174817821-ea03b791-f561-433f-b04b-c742f8f8400a.png)

Kemudian Kita atur scripting nya di bagi 2 antara monitoring dan app

Disini kita sesuaikan aja nama hosts nya dan permission sudo docker nya

```
- hosts: monitoring
  become: yes
  gather_facts: yes
  tasks:
         - name: 'update'
           apt:
            update_cache: yes

         - name: 'upgrade'
           apt:
            upgrade: dist

         - name: 'install dependencies'
           apt:
             name:
             - ca-certificates
             - curl
             - gnupg
             - lsb-release

         - name: 'add docker gpg key'
           apt_key:
            url: https://download.docker.com/linux/ubuntu/gpg

         - name: 'add repository docker'
           apt_repository:
             repo: deb  https://download.docker.com/linux/ubuntu focal stable

         - name: 'install docker engine'
           apt: 
            name:
             - docker-ce
             - docker-ce-cli
             - containerd.io
             - docker-compose-plugin

         - name: 'update'
           apt:
            update_cache: yes

         - name: 'install docker-compose'
           shell: curl -SL https://github.com/docker/compose/releases/download/v2.6.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose


         - name: 'set permision for docker'
           shell: sudo chmod +x /usr/local/bin/docker-compose
        
         - name: 'docker without sudo'
           shell: sudo usermod -aG docker moni

- hosts: app
  become: yes
  gather_facts: yes
  tasks:
         - name: 'update'
           apt:
            update_cache: yes

         - name: 'upgrade'
           apt:
            upgrade: dist

         - name: 'install dependencies'
           apt:
             name:
             - ca-certificates
             - curl
             - gnupg
             - lsb-release

         - name: 'add docker gpg key'
           apt_key:
            url: https://download.docker.com/linux/ubuntu/gpg

         - name: 'add repository docker'
           apt_repository:
             repo: deb  https://download.docker.com/linux/ubuntu focal stable

         - name: 'install docker engine'
           apt: 
            name:
             - docker-ce
             - docker-ce-cli
             - containerd.io
             - docker-compose-plugin

         - name: 'update'
           apt:
            update_cache: yes

         - name: 'install docker-compose'
           shell: curl -SL https://github.com/docker/compose/releases/download/v2.6.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose


         - name: 'set permision for docker'
           shell: sudo chmod +x /usr/local/bin/docker-compose
        
         - name: 'docker without sudo'
           shell: sudo usermod -aG docker app
```

![image](https://user-images.githubusercontent.com/99697182/174818951-31b0c90f-eddf-4dd8-a319-ebe40aef5a19.png)

![image](https://user-images.githubusercontent.com/99697182/174818995-3bffac78-4879-496a-9ee2-609d125ca968.png)

![image](https://user-images.githubusercontent.com/99697182/174819223-9061d427-6477-467b-aaf4-508feacbd56a.png)

kemudian kita install

![image](https://user-images.githubusercontent.com/99697182/174820409-4cdaa48f-c3bb-48bd-8b9f-7aa0bdda7a18.png)
 
 dan kita cek pada app server 
 
![image](https://user-images.githubusercontent.com/99697182/174820979-c1245da5-679a-4956-ad26-1e9efdb51b9b.png)

![image](https://user-images.githubusercontent.com/99697182/174827446-b23c2d96-40ec-4dc1-b827-8a3959cc9fd6.png)


### Disini saya akan coba menambah user ke server monitor

ouh iya, disini saya akan edit lagi File Inventory nya 

![image](https://user-images.githubusercontent.com/99697182/174858781-741ce7af-65a6-44ad-bec1-fe13129f232f.png)

sebelumnya install whois untuk generate password menjadi token ( sudo apt install whois )

![image](https://user-images.githubusercontent.com/99697182/174859514-c6d481bf-eaec-41de-9158-0fb0e2c6fdca.png)

dan cek (mkpasswd --help)

![image](https://user-images.githubusercontent.com/99697182/174859694-b0741eca-03f1-4690-a18f-a388bff7b505.png)

membuat password (mkpasswd --method=sha-512)

disini saya membuat password untuk user are = are

![image](https://user-images.githubusercontent.com/99697182/174860133-9e4fdba8-5797-4211-a585-d0a526dd34ed.png)

```
- hosts: monitoring
  become: yes
  gather_facts: yes
  tasks:
       - name: 'Create User'
         user:
           name: are
           password: "$6$l9O/K11I5NJf2Ncv$/EVE2VNUURY5qst4ounFxP62rAFNGElvnth6rRKqTjh8Esjcn00n6XiTlsJnCuQ2IIjvLGH22fh5JSwzo6bc.0"
           groups: sudo
           shell: /bin/bash
           system: no
           createhome: yes
           home: /home/are

       - name: 'Change Pass Authentication'
         lineinfile:
           path: /etc/ssh/sshd_config
           regexp: 'PasswordAuthentication no'
           line: PasswordAuthentication yes

       - name: 'reload'
         systemd:
           name: sshd
           state: reloaded
```

![image](https://user-images.githubusercontent.com/99697182/174861573-7667b4fe-045e-43ee-9a27-7d809f157e82.png)

kita cek

![image](https://user-images.githubusercontent.com/99697182/174861693-aa636227-2bf6-425c-bebf-a2e815c2b191.png)

kita jalankan 

![image](https://user-images.githubusercontent.com/99697182/174861846-282b1c39-6332-48c0-90b7-975a3bf0f18b.png)

kita coba pakai user baru nya dan berhasil

![image](https://user-images.githubusercontent.com/99697182/174862146-da249abb-20c6-4e8a-b165-54648b063d69.png)

# Instalasi services node exporter, prometheus & Grafana

ref : https://medium.com/nerd-for-tech/tutorial-how-to-deploy-prometheus-and-node-exporter-as-containers-on-a-remote-server-with-5-af5b449be49b

ref : https://www.techgeeknext.com/tools/docker/install-grafana-using-docker

ref : https://docs.google.com/presentation/d/16TGnZI9_ySiHXV7j5M072I80yLxMy3PUNN-GJ12BKX0/edit#slide=id.g98459a2884_1_5

Buat dahulu sebuah folder baru bernama files dan didalamnya buat file-file yang berisi services node exporter, prometheus & Grafana

ket : files disini sudah default

Kita cek dulu File Inventory 

![image](https://user-images.githubusercontent.com/99697182/174858781-741ce7af-65a6-44ad-bec1-fe13129f232f.png)

### Kita buat file konfigurasinya di direktori files(sudah default)

![image](https://user-images.githubusercontent.com/99697182/174925218-1b9f7e42-c17c-465b-8f86-e4fce20ecf89.png)

pertama kita buat node_exporter.service dan masukan konfigurasinya

```
[Unit]
Description=Node Exporter
After=network.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target

```

![image](https://user-images.githubusercontent.com/99697182/174925431-38ae134e-3ce3-40bf-89c0-ee290968cbd8.png)

kemudian kita buat prometheus.service

```
[Unit]
Description=Prometheus
After=network.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
   --config.file /etc/prometheus/prometheus.yml \
   --storage.tsdb.path /var/lib/prometheus/ \
   --web.console.templates=/etc/prometheus/consoles \
   --web.console.libraries=/etc/prometheus/console_libraries
   
[Install]
WantedBy=multi-user.target

```

![image](https://user-images.githubusercontent.com/99697182/174925703-1badccc1-2950-4ebd-b554-15b49bd429c2.png)

kemudian kita buat prometheus.yml (untuk menargetkan ip yang ingin di monitor)

konfigurasi dibawah ini sudah default 

```
global:
 scrape_interval: 10s
scrape_configs:
 - job_name: 'prometheus_metrics'
   scrape_interval: 5s
   static_configs:
     - targets: ['localhost:9090']
 - job_name: 'node_exporter_metrics'
   scrape_interval: 5s
   static_configs:
    - targets: ['localhost:9100','103.55.37.191:9100']
```
![image](https://user-images.githubusercontent.com/99697182/174926976-b3d13278-17f3-4efb-a33a-c27466b72e57.png)

jadi ada 3 file 

![image](https://user-images.githubusercontent.com/99697182/174927046-f4844c06-62bb-4d71-bba9-ef33e368ba02.png)

### Disini Saya akan mencoba install setup monitoring.yml

kita buat file node-exporter.yml

ref : https://hub.docker.com/r/bitnami/node-exporter

setelah itu kita masukan scriptnya untuk instalasi node exporter 

```
- hosts: all
  become: true
  gather_facts: yes
  tasks:
    - name: 'install node exporter'
      shell: "docker run --name node-exporter-node1 --network node-exporter-network bitnami/node-exporter:latest"
```

![image](https://user-images.githubusercontent.com/99697182/174955116-4c2066e4-f97c-46cb-9bf0-dacb4448aec0.png)

![image](https://user-images.githubusercontent.com/99697182/174954971-6c7bbdf8-a917-431a-ad7c-650ebd2e40ac.png)

![image](https://user-images.githubusercontent.com/99697182/174955181-03b9e582-81c9-4f26-a0f0-4ee380a09cd7.png)

dikarenakan saya mengalami failed, saya akan mencoba images lain

ref: https://medium.com/nerd-for-tech/tutorial-how-to-deploy-prometheus-and-node-exporter-as-containers-on-a-remote-server-with-5-af5b449be49b

```
- hosts: all
  become: true
  gather_facts: yes
  tasks:
    - name: 'install node exporter'
      shell: "docker run -d --name=node-exporter --net=\"host\" --pid=\"host\" -v \"/:/host:ro,rslave\" prom/node-exporter:latest --path.rootfs=/host"
```

![image](https://user-images.githubusercontent.com/99697182/174952827-5f4d805e-76a2-4d33-84cf-0cf4097372db.png)

![image](https://user-images.githubusercontent.com/99697182/174953134-d008c18b-ede9-46da-a9db-15f6dff6262a.png)

Setelah ini kita cek browser di port 9100

```
103.55.37.194:9100
```

![image](https://user-images.githubusercontent.com/99697182/174954062-984c1f79-f448-453f-a7fc-7f41c5b478f7.png)

```
103.55.37.191:9100
```

![image](https://user-images.githubusercontent.com/99697182/174954141-117e7968-826c-4b3b-b4ef-1fa8d180a1f0.png)

kita juga bisa cek di server monitoringnya 

![image](https://user-images.githubusercontent.com/99697182/174955416-acf2ca1e-a84d-4ce0-8cce-5cbd7924b721.png)

kita juga bisa cek di server appnya 

![image](https://user-images.githubusercontent.com/99697182/174955641-bff6fb15-396b-4909-83ac-f69b22453326.png)

Setelah itu kita buat file monitoring.yml nya

![image](https://user-images.githubusercontent.com/99697182/174919585-d751c32c-5ff1-4ac4-81cd-768c54d2ca9b.png)

ref : https://hub.docker.com/r/bitnami/prometheus/

ref : https://hub.docker.com/r/grafana/grafana

dan kita masukan script nya :

```
- hosts: monitoring
  become: true
  gather_facts: yes
  tasks:
    - name: "copy configuration prometheus.yml"
      copy:
        src: files/
        dest: /home/moni/prometheus/
        owner: moni
        group: sudo
        mode: 0664
    - name: "install prometheus"
      command: "docker run --name prometheus \ -v /path/to/prometheus-persistence:/opt/bitnami/prometheus/data \ bitnami/prometheus:latest"
    - name: "install grafana"
      command: "docker run -d --name=grafana -p 3000:3000 grafana/grafana"
```

![image](https://user-images.githubusercontent.com/99697182/174971071-03388231-a59e-400d-9e02-a81634b3b5c4.png)

kita install monitoring.yml nya dan saya mengalami failed

![image](https://user-images.githubusercontent.com/99697182/174971726-94517bc0-2fef-4453-ab77-2bb3494dab35.png)

![image](https://user-images.githubusercontent.com/99697182/174972008-c98e4d3f-6f72-4ce7-a072-7b7ae1e73a75.png)

disini saya akan ganti

ref : https://prometheus.io/docs/prometheus/latest/installation/#:~:text=All%20Prometheus%20services%20are%20available%20as%20Docker%20images,sample%20configuration%20and%20exposes%20it%20on%20port%209090.

```
- hosts: monitoring
  become: true
  gather_facts: yes
  tasks:
    - name: "copy configuration prometheus.yml"
      copy:
        src: files/
        dest: /home/moni/prometheus/
        owner: moni
        group: sudo
        mode: 0664
    - name: "install prometheus"
      command: "docker run -d --name=prometheus -p 9090:9090 -v /home/moni/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml prom/prometheus"
    - name: "install grafana"
      command: "docker run -d --name=grafana -p 3000:3000 grafana/grafana"
```

![image](https://user-images.githubusercontent.com/99697182/174972521-23ffa8e4-e579-4b3a-a4f0-ccc23e9e6651.png)

akan saya coba install lagi dan mengalami error 

![image](https://user-images.githubusercontent.com/99697182/174973264-d982caf3-2108-44d8-88aa-ccc0f50ef269.png)

dan jika saya cek 

![image](https://user-images.githubusercontent.com/99697182/174974026-28b52576-4061-4a9f-9ca2-34ed108b6a5d.png)

![image](https://user-images.githubusercontent.com/99697182/174974168-7f6fbbe4-38be-4722-b823-0ae51bde7392.png)

disini saya akan menghapus container , image & foldernya dulu

![image](https://user-images.githubusercontent.com/99697182/174978189-959bdda1-3e2d-4da4-803c-32a0cfe5857f.png)

![image](https://user-images.githubusercontent.com/99697182/174979279-03250fb3-3b86-48d2-91f5-8ce4b055dd07.png)

![image](https://user-images.githubusercontent.com/99697182/174980025-dac62f50-428b-488f-98c3-acd678715072.png)

disini saya akan mempelajari lagi ansible nya

ref : https://docs.ansible.com/ansible/2.5/modules/docker_container_module.html

disini saya akan mengulang script nya kembali 




















