## K8S Master & Slave setup
Create 3 GCP instances : 1 Master & 2 Worker Nodes

#### Execute the below commands on all 3 nodes (1 Master & 2 Worker Nodes):
-     sudo su -
- apt update
- apt install docker.io -y
- docker version
- systemctl enable docker
- sudo apt install software-properties-common -y
- curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
- apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
- apt update
- apt install kubeadm -y
- kubeadm version
- vi /etc/docker/daemon.json
-     {
      "exec-opts": ["native.cgroupdriver=systemd"]
      }
- systemctl daemon-reload
- systemctl restart docker.service
- systemctl status docker.service

#### Master Node Alone
- kubeadm init
- systemctl status kubelet
- mkdir -p $HOME/.kube - creating a folder .kube 
- sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
- sudo chown $(id -u):$(id -g) $HOME/.kube/config
- kubectl get nodes
- kubectl get pods --all-namespaces
- kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
- kubectl get pods --all-namespaces
- kubectl get nodes
- kubeadm token create --print-join-command

#### Worker Nodes Alone
- Enter the kubeadm join command

