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















