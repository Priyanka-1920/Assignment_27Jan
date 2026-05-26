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

<<<<<<< HEAD
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
=======
## Getting Started
## 🛠 Prerequisites & Setup
#### 1. Setup Tools**: [docs/TOOLS-SETUP-GUIDE.md](docs/TOOLS-SETUP-GUIDE.md)
#### 2. AWS ECR Registry Setup 
# Setup AWS credentials first
aws configure
# Enter your AWS Access Key ID, Secret Access Key, region (us-east-1), and output format (json)
# Or use environment variables
export AWS_ACCESS_KEY_ID=your-access-key
export AWS_SECRET_ACCESS_KEY=your-secret-key
export AWS_DEFAULT_REGION=us-east-1

# If above credentials are already set, run below command to verify
aws sts get-caller-identity

# Create ECR repositories either via the aws cli as mentioned below or via console (Has to be done once to create the ECR repo, skip this step when you are rebuilding the docker images):

like:
aws ecr create-repository --repository-name <your-username>-shopnow/frontend --region <region>
aws ecr create-repository --repository-name <your-username>-shopnow/backend --region <region>
aws ecr create-repository --repository-name <your-username>-shopnow/admin --region <region>

# Get login token (run this command everytime as the docker credentials are persisted only on the terminal)
aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <account-id>.dkr.ecr.<region>.amazonaws.com
>>>>>>> 59f2ef6 (added artefacts)

## Validate Helm Chart

<<<<<<< HEAD
=======
#### 3. Update Configurations in below mentioned files

## 🔧 Personalization Required

**For Multi-User Kubernetes Clusters**: To avoid conflicts when multiple learners use the same cluster, each user must personalize their deployment with unique identifiers.

**IMPORTANT**: This project contains hardcoded references that you must update with your own values:

3.1. Replace "aryan" with your username in these locations:

  **Ingress Paths** (in both Kubernetes manifests and Helm charts):
   - `kubernetes/k8s-manifests/ingress/ingress-shopnow.yaml`
     - Change `/aryan` to `/<your-username>`
     - Change `/aryan-admin` to `/<your-username>-admin`
   
   - `kubernetes/helm/charts/frontend/values.yaml`
     - Change `path: /aryan` to `path: /<your-username>`
   
   - `kubernetes/helm/charts/admin/values.yaml`
     - Change `path: /aryan-admin` to `path: /<your-username>-admin`

  **Nginx ConfigMaps**
   - All references with 'aryan' to <your-username> in following files:
   - `kubernetes/k8s-manifests/frontend/cm-nginx.yaml`   
   - `kubernetes/k8s-manifests/admin/cm-nginx.yaml`

  **Helm Chart Nginx Configurations**:
   - All references with 'aryan' in the 'nginx.config' section to <your-username> in following files:
   - `kubernetes/helm/charts/frontend/values.yaml` 
   - `kubernetes/helm/charts/admin/values.yaml`

  **Dockerfiles** (Build Arguments):
   - `frontend/Dockerfile`
     - Change `ARG USER_NAME=aryan` to `ARG USER_NAME=<your-username>`
   
   - `admin/Dockerfile`
     - Change `ARG USER_NAME=aryan` to `ARG USER_NAME=<your-username>`

  **Build Script** (optional):
   - `scripts/build-and-push.sh`
     - Update the example usage comments that reference "aryan"

3.2. **ECR Repository Names** - Update to your username:
   - All `kubernetes/k8s-manifests/*/deployment.yaml` files
   - All `kubernetes/helm/charts/*/values.yaml` files
   - All `jenkins\Jenkinsfile.*.*` files
   - Change `shopnow/frontend` to `<your-username>-shopnow/frontend`
   - Change `shopnow/backend` to `<your-username>-shopnow/backend`
   - Change `shopnow/admin` to `<your-username>-shopnow/admin`

3.3. **Update Namespace** on these locations:
  - `kubernetes/k8s-manifests/namespace/namespace.yaml` - Change namespace name
  - All files in `kubernetes/k8s-manifests/*/` - Update namespace references
  - `kubernetes/argocd/apps/*.yaml` - Update destination namespace
  - All kubectl commands in this README - Replace `shopnow-demo` with your namespace

3.4. **Update ArgoCD Repository URL**:
  - In `kubernetes/argocd/umbrella-application.yaml` and all `kubernetes/argocd/apps/*.yaml` files:
  - Change `repoURL: 'https://github.com/aryanm12/shopNow'` 
  - To `repoURL: 'https://github.com/<your-github-username>/<your-repo-name>'`


#### 4. Kubernetes Cluster Access (Make sure to have a running Kubernetes cluster, here is an example to connect with EKS)
>>>>>>> 59f2ef6 (added artefacts)
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
<<<<<<< HEAD
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
=======
# Install metrics server (required for resource monitoring and HPA)
kubectl apply -f kubernetes/pre-req/metrics-server.yaml

# Install ingress-nginx controller (for external access)
# For EKS, other cloud provider will have different file
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.12.0-beta.0/deploy/static/provider/aws/deploy.yaml

# For local development (minikube/kind/Docker Desktop)
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.1/deploy/static/provider/kind/deploy.yaml

# Verify installations
kubectl get pods -n kube-system
kubectl get pods -n ingress-nginx
kubectl top nodes  # Should work after metrics server is running
kubectl top pods  # Should work after metrics server is running

# To enable Persistent Storage

# First install the EBS CSI driver as an EKS Addon

-> In the EKS Console, open your cluster → go to Add-ons → click Get more add-ons → select Amazon EBS CSI driver → click Next.
-> On the configuration page, Under Pod identity association, choose Create a new IAM role, and the console will auto-attach the AmazonEBSCSIDriverPolicy.
-> Confirm and click Create. The add-on installs, the IAM role is associated with the SA via Pod Identity, and the driver starts running.
-> Verify under Add-ons tab that the EBS CSI driver is active and under Pod identity associations tab you see the SA <-> IAM role mapping.

# Install storage class for persistent volumes
kubectl apply -f kubernetes/pre-req/storageclass-gp3.yaml

# Verify storage class installation
kubectl get storageclass


## ⚡ Build and Deploy the micro-services
>>>>>>> 59f2ef6 (added artefacts)

## Required Plugins

- Git Plugin
- Docker Pipeline Plugin
- Kubernetes CLI Plugin
- Pipeline Plugin

---

# DockerHub Credentials

Credential ID used in Jenkins:

```bash
<<<<<<< HEAD
dockerhub-creds
```

---
=======
scripts/build-and-push.sh <account-id>.dkr.ecr.<region>.amazonaws.com/<registry-name> <tag-name-number> <your-username> 

# Example for user 'aryan' with tag 'latest' and ECR registry '975050024946.dkr.ecr.ap-southeast-1.amazonaws.com/shopnow':
./scripts/build-and-push.sh 975050024946.dkr.ecr.ap-southeast-1.amazonaws.com/shopnow latest aryan


### 2. Choose Your Deployment Method
>>>>>>> 59f2ef6 (added artefacts)

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
<<<<<<< HEAD
```

## Verify Helm Releases

```bash
helm list
```
=======

# Check daemonsets
kubectl get daemonsets -n shopnow-demo

# Check statefulsets
kubectl get statefulsets -n shopnow-demo

# Check HPA
kubectl get hpa -n shopnow-demo

# Check all of the above at once
kubectl get all -n shopnow-demo

# Check configmaps
kubectl get cm -n shopnow-demo

# Check secrets
kubectl get secrets -n shopnow-demo

# Check ingress
kubectl get ing -n shopnow-demo

# Sequence to debug in case of any issue with the pods
kubectl get pods -n shopnow-demo
kubectl describe pod backend-746cc99cd-cqrgf -n shopnow-demo # Assuming that pod backend-746cc99cd-cqrgf has an error
kubectl logs backend-746cc99cd-cqrgf -n shopnow-demo --previous # If no details are found in the above command or if details like liveness probe failed are coming
>>>>>>> 59f2ef6 (added artefacts)

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


## Jenkins Kubernetes Connectivity Issue

### Issue

Jenkins pipeline was unable to connect to Docker Desktop Kubernetes cluster because kubeconfig server endpoint used localhost:

```bash
https://127.0.0.1:50261
```

Since Jenkins runs in a separate runtime environment, localhost referred to the Jenkins server itself instead of the host machine Kubernetes cluster.

### Resolution Approach

- Configured kubeconfig as Jenkins Secret Text credential
- Injected kubeconfig dynamically during deployment stage
- Successfully authenticated kubeconfig structure
- Deployment logic validated successfully

This issue is specific to local Docker Desktop Kubernetes networking and would typically be resolved in production using:
- EKS
- AKS
- GKE
- Remote Kubernetes cluster
- Shared Jenkins agents

---

# Author

## Priyanka Malik

DevOps / Platform Engineering Enthusiast

GitHub:

https://github.com/Priyanka-1920
