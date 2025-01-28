# KubeFlower Setup Guide

This guide outlines the steps to set up and run the KubeFlower project, which facilitates federated learning using Kubernetes. Follow the instructions below to build, deploy, and manage the KubeFlower components.

---

## Prerequisites

Ensure your system has the following tools installed:
- Docker
- Kubernetes CLI (kubectl)
- Minikube or any other Kubernetes cluster

---

## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/hpn-bristol/kubeFlower
cd kubeFlower
```

### 2. Build the Docker Image
```bash
docker build -t kubeflower .
docker images
```

### 3. Deploy the Flower Server

#### a. Create the Server Service
```bash
kubectl apply -f descriptors/serverService.yaml
```

#### b. Deploy the Flower Server
```bash
kubectl apply -f descriptors/serverDeploy.yaml
```

#### c. Verify Deployment
```bash
kubectl get all -o wide
```

### 4. Deploy the Flower Clients
```bash
kubectl apply -f descriptors/clientDeploy.yaml
```

#### Verify Deployment
```bash
kubectl get all
```

---

## Monitoring Logs

### 1. Check the Logs on the Flower Server Pod
Replace the pod name with the actual name from `kubectl get pods`.
```bash
kubectl logs flower-server-<pod-name> -f
```

### 2. Check the Logs on the Flower Client Pods
Repeat the process for all client pods.
```bash
kubectl logs flower-client-<pod-name> -f
```

---

## Cleanup

After the federated learning process is complete, clean up the resources as follows:

### 1. Delete Deployments
```bash
kubectl delete deploy flower-client flower-server
```

### 2. Delete Services
```bash
kubectl delete service service-server
```

### 3. Stop the Kubernetes Cluster (if using Minikube)
```bash
minikube stop
```

---

## Additional Commands

### Check Cluster Status
```bash
kubectl get nodes
```

### Describe Pods (for Debugging)
```bash
kubectl describe pod <pod-name>
```

### List All Kubernetes Resources
```bash
kubectl get all
```

### Delete All Resources (if needed)
```bash
kubectl delete all --all
```

---

For more details, refer to the [KubeFlower GitHub Repository](https://github.com/hpn-bristol/kubeFlower).
