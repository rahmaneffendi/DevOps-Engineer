# Setup Manual Kubernetes & Deploy Microservices

![image](https://user-images.githubusercontent.com/99697182/175046147-596a12e3-02cb-4a91-ad92-f739f7562783.png)

#### Apa itu Kubernetes ?

Apa yang anda perlu ketahui tentang Kubernetes, keuntungan yang bisa di dapat dan bagaimana dengan arsitektur, komponen dan cara kerjanya.
Apa itu Kubernetes (K8S) dan bagaimana cara kerjanya?

Kubernetes adalah sebuah open source Orchestration platform yang membantu mengelola distributed Container dalam skala besar. Anda hanya perlu memberi instruksi kepada Kubernetes di mana Anda ingin aplikasi Anda dijalankan, maka platform ini akan menangani semua hal-hal yang lainnya.

Kubernetes menyediakan application programming interface (API) terpadu untuk mendeploy aplikasi web, batch task, dan database di dalamnya.

Aplikasi di dalam Kubernetes dikemas dalam Container dan diisolasi dari lingkungannya. Kubernetes mengotomatisasi konfigurasi aplikasi anda. Serta mencatat dan melacak semua pengalokasian resource di dalamnya.

# Buat Server

Disini saya buat 3 server di idch:

1. Server Manager (manager-rahman)

user : menej, pw : Sembarang1, Ip : 103.226.139.195

2. Server Worker 1(worker1-rahman)

user : wor1, pw : Sembarang1, Ip : 103.181.143.28 

3. Server Worker 2(worker2-rahman)

user : wor2, pw : Sembarang1, Ip : 103.171.85.240

# Install & Setup Kubernetes

ref : https://gist.github.com/sgnd/9d624a1b4034de7304f7eae71cb0e28b

terlebih dahulu login ke server manager dan masuk ke root, kemudian nonaktifkan firewall

```
sudo su
```

```
ufw disable
```

![image](https://user-images.githubusercontent.com/99697182/175050979-f9a333c9-a76c-42ef-8aae-b2516abf967a.png)

kemudian nonaktifkan swap

```
swapoff -a; sed -i '/swap/d' /etc/fstab
```

![image](https://user-images.githubusercontent.com/99697182/175051343-c662574d-7175-4909-8320-c3d78d866ef3.png)

kemudian update kernel system

```
cat >>/etc/sysctl.d/kubernetes.conf<<EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
```

![image](https://user-images.githubusercontent.com/99697182/175051653-88bb6828-0de3-40af-a531-7edc39e6b32d.png)

kemudian restart

```
sysctl --system
```

![image](https://user-images.githubusercontent.com/99697182/175051877-86f06cb9-092d-47d7-8372-72717a382282.png)

kemudian dikarenakan saya sudah setup docker dan docker-compose nya pada pembuatan server, 

![image](https://user-images.githubusercontent.com/99697182/175052541-a5471907-03ce-4eb3-925e-cb8017b0bb32.png)

maka kita langsung setup docker daemonnya saja

```
cat <<EOF | sudo tee /etc/docker/daemon.json
{
"exec-opts": ["native.cgroupdriver=systemd"],
"log-driver": "json-file",
"log-opts": {
"max-size": "100m"
},
"storage-driver": "overlay2"
}
EOF
```

![image](https://user-images.githubusercontent.com/99697182/175053013-17162245-a3eb-44c8-adbe-d310cce56bdc.png)

```
sudo systemctl enable docker
sudo systemctl daemon-reload
sudo systemctl restart docker
```

![image](https://user-images.githubusercontent.com/99697182/175053924-6ce39731-b7e8-4fbd-a625-110f48be1a2f.png)

Install kubelet, kubeadm, kubectl

```
sudo apt -y install curl apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt update -y; sudo apt -y install kubelet kubeadm kubectl
```

![image](https://user-images.githubusercontent.com/99697182/175056134-da2bff56-99d6-4e48-a86c-8b574afe7d56.png)

![image](https://user-images.githubusercontent.com/99697182/175056366-aef5781a-e2aa-4351-a35b-cd94967f6c79.png)

![image](https://user-images.githubusercontent.com/99697182/175056462-52257727-cae1-4e7c-a341-6fa38c744a88.png)

![image](https://user-images.githubusercontent.com/99697182/175056747-2054bf27-79c3-453a-b16f-08160b87ce49.png)

Konfigurasi kubeadm untuk menginisiasi server manager

```
ip a = 103.226.139.195(saya)
```

```
sudo kubeadm init --apiserver-advertise-address=103.226.139.195 --pod-network-cidr=192.168.0.0/16  --ignore-preflight-errors=all
```

![image](https://user-images.githubusercontent.com/99697182/175059676-1332db37-0d2b-4a01-a8ab-ae0d4421fcd7.png)

![image](https://user-images.githubusercontent.com/99697182/175059795-f0123782-79a5-4582-8697-8154feb52d1f.png)

saya cek

```
systemctl status kubelet
```

![image](https://user-images.githubusercontent.com/99697182/175060460-a56b7b67-5a4a-4dd2-86b7-2efb231ff906.png)

```
journalctl -xeu kubelet
```

![image](https://user-images.githubusercontent.com/99697182/175061302-d79ded7c-eec5-447c-a678-7a86afff3391.png)

disini ada error

saya cek esok harinya

![image](https://user-images.githubusercontent.com/99697182/175215102-af43dd1b-0a4c-4cc0-87a3-5e6d1036f427.png)

![image](https://user-images.githubusercontent.com/99697182/175215334-8418cc10-4837-4bdd-866c-8b2d042795fb.png)

disini saya akan mengulangi inisiasi kubeadm, dan masih gagal lagi, kemudian saya coba reset

```
kubeadm reset
```

![image](https://user-images.githubusercontent.com/99697182/175217988-bad01b46-7bd7-404e-9f03-16efc211fbbe.png)

dan akan saya coba lagi insiasi kubeadm nya, dan masih error juga

kemudian saya cek di stack overflow, dan megikuti instruksinya [ini](https://stackoverflow.com/questions/54424269/how-to-fix-the-kubelet-is-unhealthy-due-to-a-misconfiguration-of-the-node-in-so)

![image](https://user-images.githubusercontent.com/99697182/175233724-6c3c06d7-5f21-47ca-b236-e2aa15f6ced4.png)

saya reset kubeadm nya lagi dan coba mulai init lagi, dan masih tetap error

Sekarang saya mencob membuat server lagi dan memulai dari awal denga server:

Server Manager (manager-rahman), user = menej, pw = Sembarang1, Ip: 103.186.1.60

dan setelah saya coba ternyata masih gagal,  kemudian saya coba update & upgrade, dan masih tetap gagal

#### Mencoba cara lain

ref : https://www.billysoftacademy.com/learn-how-to-install-kubernetes-on-linux-ubuntu-20-04-lts-in-the-cloud-on-aws/

disini saya akan membuat server lagi dengan ubuntu 20.04 : Server Manager (manager-rahman), user = menej, pw = Sembarang1, Ip: 103.183.74.181

kemudian sampe di tahap kubeadm ini, saya berhasil, dan saya akan copy ini di perintah selanjutnya

![image](https://user-images.githubusercontent.com/99697182/175252217-3a0f09c4-f2e0-4e7d-a6b3-bc66e2ca50b5.png)

```
mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

![image](https://user-images.githubusercontent.com/99697182/175252522-f3a9e6bb-4020-4d46-b87f-0cf86798b45a.png)

Instalasi CNI Flannel (disini saya ngga pake calico)

```
sudo kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

![image](https://user-images.githubusercontent.com/99697182/175252953-3c0088c1-83a2-4c94-9529-551e8ed4569a.png)

```
sudo kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/k8s-manifests/kube-flannel-rbac.yml
```

![image](https://user-images.githubusercontent.com/99697182/175253491-a008b493-ffa9-4dd0-a468-e25aac96f963.png)

```
sudo kubectl get pods --all-namespaces
```

![image](https://user-images.githubusercontent.com/99697182/175254000-74ccd60d-e75f-4e60-9323-23648f7fe089.png)

#### Disini Pastikan server worker 1 & 2 sudah terinstall kubernetes juga, dan ngga usah init kubeadm nya

Lakukan join cluster dengan perintah berikut:

```
kubeadm token create --print-join-command
```

![image](https://user-images.githubusercontent.com/99697182/175276662-3f6a28aa-8e9a-4c04-830a-f9dd05a47d9a.png)

Lalu copy hasil output berikut ke server worker 1 dan 2

```
kubeadm join *****
```

Worker 1

![image](https://user-images.githubusercontent.com/99697182/175277220-52268b7a-2eee-4949-a3cf-f94d9a3bd385.png)

Worker 2

![image](https://user-images.githubusercontent.com/99697182/175277494-ee5a9727-7719-4b07-927c-24e7c4ea19c8.png)

Cek koneksi nya apakah sudah terkoneksi dengan cluster menggunakan perintah:

```
kubectl get nodes
```

![image](https://user-images.githubusercontent.com/99697182/175277752-781c70bb-a2f1-4736-bd98-cf56703a136f.png)

![image](https://user-images.githubusercontent.com/99697182/175277878-a5f5f37c-0574-415e-b698-e681f64dcc82.png)

# Deploy Simple Aplication (Nginx)

Deploy nginx, create terlebih dahulu

```
kubectl create deploy nginx --image nginx
```

Kemudian jika sudah berhasil di build maka jalankan

```
kubectl expose deploy nginx --port 80 --type NodePort
```

jika sudah , cek

```
kubectl get svc
```

![image](https://user-images.githubusercontent.com/99697182/175307751-1d799da7-12be-4203-ad36-72993498509e.png)

# Deploy Aplikasi Microservice

Clone aplikasi microservices

```
git clone https://github.com/dumbwaysdev/dumbways-microservices.git
```

![image](https://user-images.githubusercontent.com/99697182/175316838-0659b0fd-f519-462f-9694-9afb649e80b2.png)

Masuk ke directory aplikasi microservices dan edit docker-compose dan kubernetes.yml nya

![image](https://user-images.githubusercontent.com/99697182/175317202-1b9af2e6-e6fa-4c62-945a-065ec1520449.png)

disitu saya ganti sgnd dan suganda menjadi arahmane (username di github saya)

disini kita login ke docker nya

![image](https://user-images.githubusercontent.com/99697182/175320082-9ec91705-2d46-4791-9335-c6676d949212.png)

build docker compose

```
docker-compose build
```

![image](https://user-images.githubusercontent.com/99697182/175321160-729a6a92-5412-4bbd-926b-00c53e1f5889.png)

![image](https://user-images.githubusercontent.com/99697182/175321319-8468e83f-23ea-40ae-8561-2ebdd05dbc62.png)

![image](https://user-images.githubusercontent.com/99697182/175322764-ab3cfe69-2402-4a45-affe-3da38b411fc5.png)

Jika sudah selesai di build sekarang push ke dockerhub

![image](https://user-images.githubusercontent.com/99697182/175323024-eede6e53-45a7-4ff4-b600-6af741e59874.png)

```
docker push arahmane/todo-user:latest; docker push arahmane/todo-todo:latest; docker push arahmane/todo-skill:latest; docker push arahmane/todo-services:latest; docker push arahmane/todo-profile:latest
```

![image](https://user-images.githubusercontent.com/99697182/175325723-20f7445f-f54b-42c8-aaee-7685bdcca6bd.png)

Sekarang jalankan perintah berikut untuk mendeploy:

```
kubectl apply -f kubernetes.yml
```

![image](https://user-images.githubusercontent.com/99697182/175326397-9ef79b2f-581e-4a11-8994-220fc4463ff4.png)

dan ketika saya melihat hasilnya ternyata masih blum jalan

![image](https://user-images.githubusercontent.com/99697182/175326583-9bd48c5b-59c5-4656-a3e2-086b803b1573.png)

![image](https://user-images.githubusercontent.com/99697182/175326976-7cc2f10d-842e-43f8-b1f5-16ed5e528cdf.png)

![image](https://user-images.githubusercontent.com/99697182/175341247-bec7f2f8-e101-4248-982c-dc72b1d4999e.png)

![image](https://user-images.githubusercontent.com/99697182/175341375-46f943e2-cc95-4ae3-870a-2174b75d2f3c.png)

![image](https://user-images.githubusercontent.com/99697182/175328644-4471fa48-4a16-4b04-a72c-5c0422253e59.png)

saya coba cek nginx nya dan ngga bisa juga

![image](https://user-images.githubusercontent.com/99697182/175328050-66e054ef-b4a1-4530-bc5d-e2570029970b.png)







