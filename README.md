
# 🚀 Multi-Tier Reverse Proxy Architecture using Kubernetes on AWS EKS

## 📌 Project Overview

This project demonstrates a **cloud-native multi-tier architecture** using Kubernetes on AWS EKS.
It implements an **NGINX-based reverse proxy** that routes incoming traffic to multiple backend pods, showcasing **load balancing, scalability, and containerized deployment**.

---

## 🏗️ Architecture

```
Internet
   ↓
AWS LoadBalancer (Service)
   ↓
Reverse Proxy Pods (NGINX - 2 replicas)
   ↓
Backend Service (ClusterIP)
   ↓
Backend Pods (3 replicas)
```

---

## ⚙️ Technologies Used

* AWS EKS (Elastic Kubernetes Service)
* Kubernetes (Deployments, Services, ConfigMap)
* NGINX (Reverse Proxy)
* Docker Images (nginx, hashicorp/http-echo)
* eksctl (Cluster creation)
* kubectl (Cluster management)
* AWS CLI (Authentication)

---

## 📁 Project Structure

```
reverse-proxy-project/
│
├── backend-deployment.yaml
├── backend-service.yaml
├── nginx-configmap.yaml
├── reverse-proxy-deployment.yaml
├── reverse-proxy-service.yaml
└── README.md
```

---

## 🚀 Setup & Deployment

### 1️⃣ Create EKS Cluster

```bash
eksctl create cluster \
--name reverse-proxy-cluster \
--region ap-south-1 \
--node-type t3.small \
--nodes 2
```

---

### 2️⃣ Verify Cluster

```bash
kubectl get nodes
```

---

### 3️⃣ Deploy Application

```bash
kubectl apply -f backend-deployment.yaml
kubectl apply -f backend-service.yaml
kubectl apply -f nginx-configmap.yaml
kubectl apply -f reverse-proxy-deployment.yaml
kubectl apply -f reverse-proxy-service.yaml
```

---

### 4️⃣ Verify Pods

```bash
kubectl get pods -o wide
```

---

### 5️⃣ Get LoadBalancer URL

```bash
kubectl get svc
```

Look for:

```
reverse-proxy-service   EXTERNAL-IP
```

---

### 6️⃣ Test Application

Open in browser:

```
http://<EXTERNAL-IP>
```

Refresh multiple times to observe **load balancing across backend pods**.

---

## 🔄 How It Works

1. User sends request to LoadBalancer.
2. LoadBalancer forwards request to one of the reverse proxy pods.
3. NGINX reverse proxy routes request to backend-service.
4. Kubernetes service distributes traffic across backend pods.
5. Backend pod responds with a message.

---

## 🎯 Key Features

* Multi-tier architecture
* Reverse proxy using NGINX
* Load balancing (Service + LoadBalancer)
* Scalable backend (replicas)
* Config management using ConfigMap
* Cloud-native deployment on AWS EKS

---

## 🧠 Learning Outcomes

* Understanding Kubernetes Deployments and Services
* Implementing reverse proxy in Kubernetes
* Working with AWS EKS
* Managing configuration using ConfigMap
* Observing real-time load balancing behavior

---

## 🧹 Cleanup (Important)

```bash
eksctl delete cluster --name reverse-proxy-cluster
```

---

## 📌 Future Enhancements

* Implement Kubernetes Ingress Controller
* Use custom Docker images
* Add CI/CD pipeline (Jenkins / GitHub Actions)
* Integrate monitoring (Prometheus & Grafana)

---

## 👩‍💻 Author

**Neha Kale**
Cloud & DevOps Enthusiast

EKS Cluster

             ── Proxy Deployment (2 replicas)

             ── Proxy Service (LoadBalancer)

             ── Backend Deployment (3 replicas)

             ── Backend Service (ClusterIP) 

 reverse-proxy-project/

        ── reverse-proxy-deployment.yaml

        ── reverse-proxy-service.yaml

         ── backend-deployment.yaml

          ── backend-service.yaml

         ── nginx.conf   (your reverse proxy config)

         --- nginx-configmap.yaml (Kubernetes cannot read nginx.conf directly from your laptop, So we must store it inside Kubernetes, Storage method is called CONFIGMAP)
         (ConfigMap = "pen drive" inside Kubernetes)
