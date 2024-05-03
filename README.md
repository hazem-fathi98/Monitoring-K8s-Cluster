# Monitoring Kubernetes Cluster Using Prometheus And Grafana

In this project, we'll deploy a Kubernetes cluster using Minikube for efficient container management. We'll enhance it with Prometheus and Grafana for monitoring. Prometheus gathers metrics, while Grafana offers visualization. Together, they ensure the health, performance, and scalability of our containerized applications.

## Table Of Contents

1. [Prerequisites](#prerequisites)
2. [Installation](#installation)
3. [Snippets](#snippets)

## Prerequisites

- **Docker**
- **Minikube**
- **Helm**
- **Prometheus**
- **Grafana**

## Installation

## Docker Installation

First you have to uninstall old versions. 
```bash
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```
Then begin the installation process:

1. Install `` yum-utils`` package:
```bash 
$ sudo yum install -y yum-utils 
```
2. Add ``docker-ce.repo`` repository to download Docker:
```bash 
$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo 
```
3. Installing Docker packages:
```bash 
$ sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin 
```
4. Enabling Docker service:
```bash 
$ sudo systemctl enable --now docker
```

## Install and Set Up kubectl

1. Download the latest release with the command:
```bash 
$  curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
```
2. Make the kubectl binary executable:
```bash 
$ chmod +x ./kubectl
```
3. Move the binary into your ``PATH``:
```bash 
$ sudo mv ./kubectl /usr/local/bin/kubectl
```
4. Verifying Installation:
```bash 
$ kubectl version
```

## Minikube Installation

1. Download Minikube last release:
```bash 
$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
2. Install Minikube package:
```bash 
$ sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
3. Start Minikube:
```bash 
$ minikube start --driver=docker --force
```

## Helm Installation

1. Fetch that script:
```bash 
$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
```
2. Provide execute permission to the file:
```bash 
$ chmod 700 get_helm.sh
```
3. Run the script:
```bash 
$ ./get_helm.sh
```
## Prometheus Installation

1. Add the Prometheus repository via Helm: 
```bash 
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```
2. Update the repo:
```bash 
$ helm repo update
```
3.  Install Prometheus packages:
```bash 
$ helm install prometheus prometheus-community/prometheus
```
4. Exposing Prometheus service:
```bash 
$ kubectl expose service prometheus-server --type=NodePort --target-port=9090 --name=prometheus-server-ext
```
5. Accessing Prometheus service via minikube:
```bash 
$ minikube service prometheus-server-ext
```
## Grafana Installation

1. Add the Grafana repository
```bash 
$ helm repo add grafana https://grafana.github.io/helm-charts
```
2. Verify the repository was added:
```bash 
$ helm repo list
```
3.  Download the latest Grafana Helm charts:
```bash 
$ helm repo update
```
4. Exposing Grafana service:
```bash 
$ kubectl expose service grafana --type=NodePort --target-port=3000 --name=grafana-ext
```
5. Accessing Grafana service via helm:
```bash 
$ minikube service grafana-ext
```
6. Retrieve Grafana password:
```bash 
$ kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

## Snippets
![1](https://github.com/hazem-fathi98/Monitoring-K8s-Cluster/assets/161210724/12108fd4-46a2-4920-8887-6b5518e8b32e)
![5](https://github.com/hazem-fathi98/Monitoring-K8s-Cluster/assets/161210724/14744606-785b-42cc-8977-f2eea3d88765)
![4](https://github.com/hazem-fathi98/Monitoring-K8s-Cluster/assets/161210724/f26a35ed-2cf8-42e9-b333-de6985dd17da)


