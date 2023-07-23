# Minikube & kubectl set-up on Ubuntu 22.04

### Steps to Install Minukube to run Kubernetes Version 1.25.3 on Ubuntu 22.04

Install latest stable Kubectl

```
sudo apt-get install curl

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
```

List all available versions of kubectl so that you can choose the version that you need
```
sudo apt list kubectl* -a

```

Let us install latest kubectl version for our Lab exercises

```
sudo apt-get install kubectl
```
### Note : For specific versions of kubectl, specify the version as below

sudo apt-get install kubectl=1.25.0-00

Check kubectl version
```
kubectl version --client -o json
kubectl version --client -o yaml
```

Minikube Documentation : https://minikube.sigs.k8s.io/docs/start/

Install Minikube latest version 

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube
sudo install minikube /usr/local/bin

```

Start Minikube single node cluster by specifying docker Driver and with latest Kubernetes version 
```
minikube start --vm-driver=docker 
```


Get cluster info using kubectl
```
kubectl get nodes
kubectl get po -A
```

## Congratulations, your minikube set-up is Successfull!!!

### Additional Settings from Autocompletion

```
source <(kubectl completion bash) 
echo "source <(kubectl completion bash)" >> ~/.bashrc 

alias k=kubectl
complete -o default -F __start_kubectl k
```

Kubectl Cheat Sheet reference : https://kubernetes.io/docs/reference/kubectl/cheatsheet/
