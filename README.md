# Monitoring Kubernetes Cluster Using Prometheus And Grafana

In this project, we'll deploy a Kubernetes cluster using Minikube for efficient container management. We'll enhance it with Prometheus and Grafana for monitoring. Prometheus gathers metrics, while Grafana offers visualization. Together, they ensure the health, performance, and scalability of our containerized applications.

## Table Of Contents

1. [Prerequisites](#prerequisites)
2. [Installation](#installation)
3. [Usage](#usage)
4. [Outputs](#outputs)
5. [Cleanup](#cleanup)

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

### Application Files

These files are common in both applications.
- **main.tf:** Defines the main infrastructure components and references modules.
- **providers.tf:** Configures the backend for storing the Terraform state file and implements locking.
- **variables.tf:** Defines input variables for the main module and modules.
- **terraform.tfvars:** Variables file specifying values for the project.

### Modules

In order to emphasize the concept of modularity. This project is divided into modules leveraging Terraform modules to encapsulate infrastructure code for reusability and it is partitioned as follows:
1. **EC2 Module**: This part is related with the managing of the EC2 instances.
2. **S3 Module**: It is concerned with the managing of S3 bucket.
3. **DynamoDB Module**: It manages the DynamoDB table.
4. **Networks Module**: It is responsible for managing VPC, Security groups, Internet
gateway, Subnets, and Routing tables.


## Usage

### Prerequisites

1. [Terraform](https://www.terraform.io/) installed.
2. AWS credentials configured with the necessary permissions.

### Configuration
3. Clone the repository:
```bash
git clone https://github.com/hazem-fathi98/terraform-project.git
```
4. Update `terraform.tfvars` with the desired values for your project.
5. Change to the project directory of app1:
```bash
cd 'Terraform Project'/app1
```
6. Initialize Terraform:
```bash
terraform init
```
7. Plan the Terraform configuration:
```bash
terraform plan
```
8. Apply the Terraform configuration:
```bash
terraform apply
```
9. Confirm the changes and enter `yes` when prompted.
10. Walk through the same sequence applied previously to deploy the second application app2.



## Outputs

Concerning the first application (app1) Terraform will successfully provision and initialize our infrastructure within the selected region including:
1. EC2 Instance.
2. S3 Bucket including the state file and another bucket initiated by the configuration.
3. DynamoDB table.
4. Network components including VPC, Security group, Subnets and Internet gateway.

For the second application (app2) will be resulting the same resources but in a different region.

## Cleanup

1. To destroy the deployed resources, run:
```bash
terraform destroy
```
2. Confirm the deletion and enter `yes` when prompted.
3. Verify that changes are submitted successfully by checking resources through the AWS Management Console or using the AWS CLI.
