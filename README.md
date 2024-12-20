# Amazon Elastic Kubernetes Service (EKS)

Amazon Elastic Kubernetes Service (EKS) is a managed Kubernetes service that makes it easy to run Kubernetes on AWS without needing to install and operate your own Kubernetes control plane. EKS provides a scalable and secure platform for deploying, managing, and scaling containerized applications.

---



# EKS Cluster Setup

This README provides step-by-step instructions to create, manage, and delete an Amazon EKS Cluster using `eksctl`, `kubectl`, and `AWS CLI`.

---

## Prerequisites

Ensure you have the following tools installed on your system:
- eksctl
- kubectl
- AWS CLI

## Steps

### 1. Install eksctl CLI Tool

Download and install the `eksctl` CLI tool for creating EKS Clusters on AWS:

```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
```

Verify the installation:

```bash
eksctl version
```

---

### 2. Install kubectl

Download the latest release of `kubectl`:

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

Validate the binary:

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
```

Install `kubectl`:

```bash
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

If you do not have root access, install it locally:

```bash
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
```

Verify the installation:

```bash
kubectl version --client
```

---

### 3. Install AWS CLI on Ubuntu

Download and install the AWS CLI:

```bash
sudo apt install unzip -y
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

---

### 4. Configure AWS CLI

Connect to AWS using the CLI by configuring your AWS credentials:

```bash
aws configure
```

---

### 5. Create Amazon EKS Cluster

Use `eksctl` to create an Amazon EKS cluster:

```bash
eksctl create cluster --name demo-ekscluster --region ap-south-1 --version 1.27 --nodegroup-name linux-nodes --node-type t2.micro --nodes 2
```

---

### 6. Log In to EKS Cluster

Update the kubeconfig file to log into the EKS cluster:

```bash
aws eks update-kubeconfig --name demo-ekscluster
```

---

### 7. Delete EKS Cluster

Use `eksctl` to delete the EKS cluster:

```bash
eksctl delete cluster --name demo-ekscluster --region ap-south-1
```

---

## Notes

- Ensure you have appropriate permissions set in your AWS account for creating and managing EKS clusters.
- Replace region and cluster names as per your requirement.

---

## Author

Created by [Rutugandh Shete](https://github.com/Rutugandh-shete).
