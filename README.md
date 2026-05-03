# 🚀 MuchTodo Backend Containerization & Kubernetes Deployment

## 📌 Assessment Overview

This project was completed as part of a DevOps assessment at StartupTech. The goal was to modernize the deployment of an existing backend application by transitioning from traditional server-based deployment to a containerized and orchestrated environment.

The backend application is a Golang-based API that connects to a MongoDB database and provides CRUD operations for user management.

---

## 🎯 Objectives

The key objectives of this assessment were:

- Containerize the backend application using Docker
- Create a local development environment using Docker Compose
- Deploy the application to a Kubernetes cluster using Kind
- Implement configuration management using ConfigMaps and Secrets
- Ensure scalability and reliability using Kubernetes Deployments
- Demonstrate troubleshooting and debugging skills

---

## 🏗️ System Architecture

The system consists of:

- **Backend API** (Golang)
- **MongoDB Database**
- **Docker Containers**
- **Kubernetes Cluster (Kind)**

### Kubernetes Components:

- Namespace → `muchtodo`
- MongoDB:
  - Deployment (1 replica)
  - Service (ClusterIP)
  - Persistent Volume Claim (PVC)
  - Secret (credentials)
  - ConfigMap (database config)

- Backend:
  - Deployment (2 replicas)
  - Service (NodePort)
  - ConfigMap (.env configuration)
  - Secret (JWT key)

- Ingress:
  - Resource defined for routing (not externally active in Kind)

---

## 🐳 Phase 1: Docker Implementation

### 🔹 Dockerfile

A multi-stage Dockerfile was created to:

- Use Golang builder image
- Compile the application
- Use a minimal runtime image
- Run as a non-root user
- Expose port `8080`

### 🔹 Docker Compose

Docker Compose was used to:

- Run backend and MongoDB containers
- Enable service communication via internal network
- Configure environment variables
- Persist MongoDB data
- Automatically restart containers

---

## ☸️ Phase 2: Kubernetes Deployment

### 🔹 Namespace

All resources were deployed inside a dedicated namespace:

```bash
kubectl apply -f kubernetes/namespace.yaml
