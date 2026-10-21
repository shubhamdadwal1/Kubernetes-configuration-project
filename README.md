# 🚀 Kubernetes Configuration Project

A containerized web application deployed on Kubernetes using Docker, Kubernetes Deployments, and Services.

![Kubernetes](https://img.shields.io/badge/Kubernetes-Orchestration-326CE5?logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Containers-2496ED?logo=docker&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-Runtime-339933?logo=nodedotjs&logoColor=white)
![React](https://img.shields.io/badge/React-Frontend-61DAFB?logo=react&logoColor=black)

---

## 📌 Project Overview

This project demonstrates how to containerize a web application using Docker and deploy it to a Kubernetes cluster.

Kubernetes manages application containers through Deployments and exposes the application using a Service.

### ✨ Key Features

- Dockerized web application.
- Kubernetes Deployment with multiple replicas.
- Kubernetes Service using NodePort.
- Docker Hub image integration.
- YAML-based Kubernetes configuration.
- Application deployment and scaling.
- Container management using kubectl.
- Source code management using Git and GitHub.

---

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| React.js | Frontend |
| Node.js | JavaScript runtime |
| Docker | Containerization |
| Kubernetes | Container orchestration |
| Docker Hub | Container image registry |
| Git | Version control |
| GitHub | Source code hosting |
| YAML | Kubernetes configuration |

---

## 🏗️ Architecture Diagram

```text
                 USER / BROWSER
                       |
                       v
                NodePort :30001
                       |
                       v
             KUBERNETES SERVICE
                kube-service
                       |
                       v
              DEPLOYMENT: my-node
                 Replicas: 4
                       |
          +------------+------------+
          |            |            |
          v            v            v
        Pod 1        Pod 2        Pod 3 ... Pod 4
          |
          v
     Docker Container
          |
          v
       Docker Hub
          |
          v
shubhamdadwal/profile-website:01
```

---

## 📂 Project Structure

```text
kube/
├── public/
├── src/
│   ├── App.css
│   ├── App.js
│   ├── App.test.js
│   ├── index.css
│   ├── index.js
│   └── logo.svg
├── .gitignore
├── Dockerfile
├── deployment.yml
├── service.yml
├── package.json
├── package-lock.json
└── README.md
```

---

## 🐳 Docker Configuration

The Dockerfile defines how the application image is built.

### Build Docker Image

```bash
docker build -t shubhamdadwal/profile-website:01 .
```

### Login to Docker Hub

```bash
docker login
```

### Push Image to Docker Hub

```bash
docker push shubhamdadwal/profile-website:01
```

Docker image:

`shubhamdadwal/profile-website:01`

---

## ☸️ Kubernetes Deployment

The Deployment manages the application Pods and maintains the desired number of replicas.

### Example deployment.yml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-node
spec:
  replicas: 4
  selector:
    matchLabels:
      app: node-app
  template:
    metadata:
      labels:
        app: node-app
    spec:
      containers:
        - name: prof-cont
          image: shubhamdadwal/profile-website:01
          ports:
            - containerPort: 3000
```

**Note:** This is an example configuration. Keep your existing YAML if it differs, and ensure the image and container port match your application.

---

## 🌐 Kubernetes Service

The Service exposes the application through a NodePort.

### Example service.yml

```yaml
apiVersion: v1
kind: Service
metadata:
  name: kube-service
spec:
  type: NodePort
  selector:
    app: node-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3000
      nodePort: 30001
```

The Service selector must match the labels in `deployment.yml`.

---

## 📋 Prerequisites

Install the following tools:

- Docker Desktop
- Kubernetes cluster
- kubectl
- Node.js and npm
- Git

Check the installed versions:

```bash
docker --version
kubectl version --client
node --version
npm --version
git --version
```

Check Kubernetes:

```bash
kubectl cluster-info
kubectl get nodes
```

---

## 📥 Clone the Repository

```bash
git clone https://github.com/shubhamdadwal1/Kubernetes-configuration-project.git
```

Navigate to the project:

```bash
cd Kubernetes-configuration-project
```

---

## 🚀 Deploy the Application

### Step 1: Start Kubernetes

Ensure your Kubernetes cluster is running.

```bash
kubectl cluster-info
```

### Step 2: Apply the Deployment

```bash
kubectl apply -f deployment.yml
```

### Step 3: Apply the Service

```bash
kubectl apply -f service.yml
```

### Step 4: Verify Resources

```bash
kubectl get deployments
kubectl get pods
kubectl get services
```

### Step 5: Check Application Logs

```bash
kubectl logs deployment/my-node
```

---

## 🌍 Access the Application

If your local Kubernetes cluster supports NodePort access, open:

**http://localhost:30001**

For remote Kubernetes clusters, use the appropriate node IP and network configuration.

---

## 📊 Useful Kubernetes Commands

| Task | Command |
|---|---|
| View all resources | `kubectl get all` |
| View Pods | `kubectl get pods` |
| View Deployments | `kubectl get deployments` |
| View Services | `kubectl get services` |
| Describe Deployment | `kubectl describe deployment my-node` |
| View application logs | `kubectl logs deployment/my-node` |
| Scale Deployment | `kubectl scale deployment my-node --replicas=4` |
| Restart Deployment | `kubectl rollout restart deployment/my-node` |
| Check rollout status | `kubectl rollout status deployment/my-node` |
| View cluster nodes | `kubectl get nodes` |
| View Kubernetes events | `kubectl get events` |

---

## 🔍 Troubleshooting

### 1. Pods Are Not Starting

```bash
kubectl get pods
kubectl describe pod <pod-name>
kubectl get events
```

Check the events for image-pull errors, invalid configuration, or resource problems.

### 2. Application Logs

```bash
kubectl logs deployment/my-node
```

### 3. Service Is Not Accessible

```bash
kubectl get services
kubectl describe service kube-service
kubectl get endpoints kube-service
```

Ensure the Service selector matches the Pod labels and the target port matches the application's listening port.

### 4. Validate YAML Files

```bash
kubectl apply --dry-run=client -f deployment.yml
kubectl apply --dry-run=client -f service.yml
```

---

## 🎯 Learning Outcomes

- Understanding Docker containerization.
- Building and publishing Docker images.
- Deploying applications on Kubernetes.
- Managing replicas with Kubernetes Deployments.
- Exposing applications using Kubernetes Services.
- Writing Kubernetes YAML configuration files.
- Managing application resources using kubectl.
- Using Git and GitHub for version control.

---

## 👨‍💻 Author

**Shubham Dadwal**

GitHub: [shubhamdadwal1](https://github.com/shubhamdadwal1)

---

## 📄 License

This project is intended for educational and learning purposes.
