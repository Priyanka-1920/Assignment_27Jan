ShopNow MERN DevOps Deployment
Project Overview
This project demonstrates end-to-end DevOps implementation for a MERN (MongoDB, Express.js, React.js, Node.js) application using:


Docker


Kubernetes


Helm


Jenkins CI/CD


DockerHub


The application consists of:


Frontend → React.js + Nginx


Backend → Node.js + Express.js


Database → MongoDB StatefulSet



GitHub Repository
Assignment_27Jan Repository

Project Structure
Assignment_27Jan/│├── backend/├── frontend/├── helm/│   └── shopnow/├── kubernetes/│   └── k8s-manifests/├── Jenkinsfile├── README.md└── scripts/

Technologies Used
TechnologyPurposeDockerContainerizationKubernetesContainer orchestrationHelmKubernetes package managementJenkinsCI/CD pipelineMongoDBDatabaseReact.jsFrontendNode.jsBackend APIDockerHubContainer image registry

Docker Images
Backend Image
kaushal2052devops/shopnow-backend:v1
Frontend Image
kaushal2052devops/shopnow-frontend:v3

Kubernetes Components
Backend


Deployment


ClusterIP Service


NodePort Service


Frontend


Deployment


ConfigMap


NodePort Service


MongoDB


StatefulSet


Headless Service


Persistent Volume Claim



Helm Chart
Helm chart location:
helm/shopnow
Validate Helm Chart
helm lint .
Install Helm Chart
helm upgrade --install shopnow-release ./helm/shopnow

Jenkins CI/CD Pipeline
The Jenkins pipeline automates:


GitHub code checkout


Backend Docker image build


Frontend Docker image build


DockerHub login


Docker image push


Helm validation


Kubernetes deployment


Deployment verification



Jenkins Pipeline Stages
Checkout CodeBuild Backend Docker ImageBuild Frontend Docker ImageDocker LoginPush Backend Docker ImagePush Frontend Docker ImageHelm LintDeploy using HelmVerify Kubernetes Deployment

Jenkins Configuration
Required Plugins


Git Plugin


Docker Pipeline Plugin


Kubernetes CLI Plugin


Pipeline Plugin



DockerHub Credentials
Credential ID used in Jenkins:
dockerhub-creds

Kubernetes Cluster
Docker Desktop Kubernetes was used for deployment.

Application Deployment
Verify Pods
kubectl get pods -n shopnow-demo
Verify Services
kubectl get svc -n shopnow-demo
Verify Helm Releases
helm list

Application Access
Frontend
http://localhost:3000
Backend API
http://localhost:31590/api/health

Docker Commands
Build Backend Image
docker build -t kaushal2052devops/shopnow-backend:v1 ./backend
Build Frontend Image
docker build -t kaushal2052devops/shopnow-frontend:v3 ./frontend
Push Images
docker push kaushal2052devops/shopnow-backend:v1docker push kaushal2052devops/shopnow-frontend:v3

Challenges Faced
MongoDB DNS Resolution Issue
Error
getaddrinfo ENOTFOUND mongo-0.mongo-headless.shopnow-demo.svc.cluster.local
Solution
Updated MongoDB connection string to:
mongodb://mongo-headless.shopnow-demo.svc.cluster.local:27017/shopnow

MongoDB Authentication Issue
Error
MongoServerError: Authentication failed
Solution
Removed incorrect MongoDB credentials and used proper cluster service endpoint.

Frontend PUBLIC_URL Issue
Issue
Frontend was loading assets from:
/aryan/static/
Solution
Rebuilt React frontend after removing PUBLIC_URL configuration from Dockerfile.

NodePort Access Issue
Issue
NodePort service was not accessible using localhost directly.
Solution
Used Docker Desktop Kubernetes port forwarding.

Jenkins Kubernetes Authentication Issue
Issue
Jenkins was unable to authenticate with Kubernetes cluster.
Solution
Configured kubeconfig as Jenkins Secret Text credential and injected it during deployment stage.

Learning Outcomes
This project helped in understanding:


Docker containerization


Kubernetes deployments


StatefulSets


Persistent storage


Helm charts


Jenkins CI/CD pipelines


DockerHub integration


Kubernetes troubleshooting


DevOps automation



Author
Priyanka Malik
DevOps / Platform Engineering Enthusiast
GitHub:
Priyanka GitHub Profile
