# localdev
Minikube on Wsl

Open PowerShell as Administrator and execute:

 wsl --install 

 sudo apt update && sudo apt upgrade 
 sudo apt update && sudo apt install zip unzip -y
 [sudo] password for <userName>:
 t
Install SDKMAN! by running:

 curl -s "https://get.sdkman.io" | bash 

After installation, reload your shell:
bash

 source "$HOME/.sdkman/bin/sdkman-init.sh" 
Install Java 23:
Use SDKMAN!o install the latest Java version:


 sdk install java 23.0.2.fx-zulu

 sudo apt update

 sudo apt upgrade -y

 sudo apt install apt-transport-https ca-certificates curl software-properties-common -y

 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o    /usr/share/keyrings/docker-archive-keyring.gpg

 echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

 sudo apt update

 sudo apt install docker-ce docker-ce-cli containerd.io -y

 sudo service docker start

 sudo docker --version

 sudo usermod -aG docker <yourName>

 newgrp docker

 curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

sudo chmod +x minikube

sudo mv minikube /usr/local/bin/

 minikube start --driver=docker

😄  minikube v1.35.0 on Ubuntu 20.04 (amd64)
✨  Using the docker driver based on user configuration
📌  Using Docker driver with root privileges
👍  Starting "minikube" primary control-plane node in "minikube" cluster
🚜  Pulling base image v0.0.46 ...
💾  Downloading Kubernetes v1.32.0 preload ...
    > preloaded-images-k8s-v18-v1...:  333.57 MiB / 333.57 MiB  100.00% 4.12 Mi
    > gcr.io/k8s-minikube/kicbase...:  500.31 MiB / 500.31 MiB  100.00% 5.03 Mi
🔥  Creating docker container (CPUs=2, Memory=3900MB) ...
🐳  Preparing Kubernetes v1.32.0 on Docker 27.4.1 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring bridge CNI (Container Networking Interface) ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: storage-provisioner, default-storageclass
💡  kubectl not found. If you need it, try: 'minikube kubectl -- get pods -A'
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default


Install kubectl


curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

sudo chmod +x kubectl

 sudo mv kubectl /usr/local/bin/

kubectl version --client

kubectl get nodes

minikube dashboard

✅ WSL2 Installed & Ubuntu Set Up
✅ Ubuntu Updated with Required Packages
✅ Docker Installed Inside WSL2
✅ Minikube Installed and Running
✅ kubectl Installed and Configured
✅ Windows kubectl Configured for IntelliJ


Create a shortcut to run the following script in powershell

"powershell -ExecutionPolicy Bypass -File C:\Scripts\wsl.ps1" 


wsl bash -c "
  sudo service docker start;
  if ! minikube status | grep -q 'Running'; then
    minikube start --driver=docker;
  fi;
  kubectl get nodes;
  exec bash
"

Copy the kube config from wsl to windows mount and the three certs then change the paths
cp ~/.kube/config /mnt/c/Users/pfcit2/.kube/config

apiVersion: v1
clusters:
- cluster:
    certificate-authority: ca.crt
    extensions:
    - extension:
        last-update: Tue, 11 Mar 2025 14:45:36 GMT
        provider: minikube.sigs.k8s.io
        version: v1.35.0
      name: cluster_info
    server: https://127.0.0.1:32771
  name: minikube
contexts:
- context:
    cluster: minikube
    extensions:
    - extension:
        last-update: Tue, 11 Mar 2025 14:45:36 GMT
        provider: minikube.sigs.k8s.io
        version: v1.35.0
      name: context_info
    namespace: default
    user: minikube
  name: minikube
current-context: minikube
kind: Config
preferences: {}
users:
- name: minikube
  user:
    client-certificate: client.crt
    client-key: client.key


