# ShopNow MERN DevOps Deployment

## Project Overview

This project demonstrates end-to-end DevOps implementation for a MERN (MongoDB, Express.js, React.js, Node.js) application using:
- Docker
- Kubernetes
- Helm
- Jenkins
- DockerHub

The application consists of:
- Frontend → React.js + Nginx
- Backend → Node.js + Express.js
- Database → MongoDB StatefulSet
---
# GitHub Repository

Repository Link:
https://github.com/Priyanka-1920/Assignment_27Jan
---

# Project Structure

Assignment_27Jan/
│
├── backend/
├── frontend/
├── helm/
│   └── shopnow/
├── kubernetes/
│   └── k8s-manifests/
├── Jenkinsfile
├── README.md
└── scripts/

---

# Technologies Used

| Technology | Purpose |
|---|---|
| Docker | Containerization |
| Kubernetes | Container orchestration |
| Helm | Kubernetes package management |
| Jenkins | CI/CD automation |
| MongoDB | Database |
| React.js | Frontend |
| Node.js | Backend API |
| DockerHub | Container image registry |

---

# Docker Images

## Backend Image

```bash
kaushal2052devops/shopnow-backend:v1
```

## Frontend Image

```bash
kaushal2052devops/shopnow-frontend:v3
```

---

# Kubernetes Components

## Backend

- Deployment
- ClusterIP Service
- NodePort Service

## Frontend

- Deployment
- ConfigMap
- NodePort Service

## MongoDB

- StatefulSet
- Headless Service
- Persistent Volume Claim

---

# Helm Chart

Helm chart location:

```bash
helm/shopnow
```

## Validate Helm Chart

```bash
helm lint .
```

## Install Helm Chart

```bash
helm upgrade --install shopnow-release ./helm/shopnow
```

---

# Jenkins CI/CD Pipeline

The Jenkins pipeline automates:

1. GitHub code checkout
2. Backend Docker image build
3. Frontend Docker image build
4. DockerHub login
5. Docker image push
6. Helm validation
7. Kubernetes deployment
8. Deployment verification

---

# Jenkins Pipeline Stages

```bash
Checkout Code
Build Backend Docker Image
Build Frontend Docker Image
Docker Login
Push Backend Docker Image
Push Frontend Docker Image
Helm Lint
Deploy using Helm
Verify Kubernetes Deployment
```

---

# Jenkins Configuration

## Required Plugins

- Git Plugin
- Docker Pipeline Plugin
- Kubernetes CLI Plugin
- Pipeline Plugin

---

# DockerHub Credentials

Credential ID used in Jenkins:

```bash
dockerhub-creds
```

---

# Kubernetes Cluster

Docker Desktop Kubernetes was used for deployment.

---

# Application Deployment

## Verify Pods

```bash
kubectl get pods -n shopnow-demo
```

## Verify Services

```bash
kubectl get svc -n shopnow-demo
```

## Verify Helm Releases

```bash
helm list
```

---

# Application Access

## Frontend

```bash
http://localhost:3000
```

## Backend API

```bash
http://localhost:31590/api/health
```

---

# Docker Commands

## Build Backend Image

```bash
docker build -t kaushal2052devops/shopnow-backend:v1 ./backend
```

## Build Frontend Image

```bash
docker build -t kaushal2052devops/shopnow-frontend:v3 ./frontend
```

## Push Images

```bash
docker push kaushal2052devops/shopnow-backend:v1

docker push kaushal2052devops/shopnow-frontend:v3
```

---

# Challenges Faced

## MongoDB DNS Resolution Issue

### Error

```bash
getaddrinfo ENOTFOUND mongo-0.mongo-headless.shopnow-demo.svc.cluster.local
```

### Solution

Updated MongoDB connection string to:

```bash
mongodb://mongo-headless.shopnow-demo.svc.cluster.local:27017/shopnow
```

---

## MongoDB Authentication Issue

### Error

```bash
MongoServerError: Authentication failed
```

### Solution

Removed incorrect MongoDB credentials and used proper cluster service endpoint.

---

## Frontend PUBLIC_URL Issue

### Issue

Frontend was loading assets from:

```bash
/aryan/static/
```

### Solution

Rebuilt React frontend after removing PUBLIC_URL configuration from Dockerfile.

---

## NodePort Access Issue

### Issue

NodePort service was not accessible using localhost directly.

### Solution

Used Docker Desktop Kubernetes port forwarding.

---

## Jenkins Kubernetes Authentication Issue

### Issue

Jenkins was unable to authenticate with Kubernetes cluster.

### Solution

Configured kubeconfig as Jenkins Secret Text credential and injected it during deployment stage.

---

# Learning Outcomes

This project helped in understanding:

- Docker containerization
- Kubernetes deployments
- StatefulSets
- Persistent storage
- Helm charts
- Jenkins CI/CD pipelines
- DockerHub integration
- Kubernetes troubleshooting
- DevOps automation

---

# Author

## Priyanka Malik

DevOps / Platform Engineering Enthusiast

GitHub:

https://github.com/Priyanka-1920
