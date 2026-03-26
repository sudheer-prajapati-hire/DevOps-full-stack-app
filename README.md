# 🚀 DevOps Full-Stack App (Docker + MySQL + AWS ECR)

## 📌 Overview

This project demonstrates how to containerize a Node.js backend using **multi-stage Docker builds**, orchestrate services with **Docker Compose**, and push images to **AWS ECR**.

It follows production-level DevOps practices including security, optimization, and modular deployment.

---

## 🏗️ Architecture

```
                Internet
                   |
            ----------------
            |   EC2 Host   |
            ----------------
                   |
            ----------------
            |   Docker     |
            ----------------
            |  Backend     |
            |  Container   |
            ----------------
                   |
            ----------------
            |   MySQL DB   |
            |  Container   |
            ----------------
                   |
            ----------------
            |  AWS ECR     |
            ----------------
```

---

## 🧠 Key Features

* Multi-stage Docker build (optimized image)
* Non-root user inside container (security best practice)
* Docker Compose orchestration (App + DB)
* MySQL with persistent volume
* AWS ECR integration
* Health check endpoint (`/health`)

---

## 🐳 Docker Optimization

| Feature           | Benefit                              |
| ----------------- | ------------------------------------ |
| Multi-stage build | Smaller image size (~400MB → <100MB) |
| Alpine base image | Lightweight & fast                   |
| .dockerignore     | Faster builds                        |
| Non-root user     | Improved security                    |

---

## 📂 Project Structure

```
devops-full-stack-app/
├── backend/
│   ├── index.js
│   ├── package.json
│   ├── Dockerfile
│   └── .dockerignore
├── docker-compose.yml
└── README.md
```

---

## ⚙️ Run Locally (Without Docker)

```bash
cd backend
npm install
npm start
```

Test:

```bash
curl http://localhost:3000/health
```

---

## 🐳 Run with Docker

### Build Image

```bash
docker build -t myapp-backend:v1 ./backend
```

### Run Container

```bash
docker run -p 3000:3000 myapp-backend:v1
```

### Test

```bash
curl http://localhost:3000/health
```

---

## 🧩 Run with Docker Compose (Recommended)

```bash
docker-compose up -d
```

Check services:

```bash
docker-compose ps
```

View logs:

```bash
docker-compose logs backend
```

Stop:

```bash
docker-compose down
```

---

## ☁️ Push to AWS ECR

### 1. Create Repository

```bash
aws ecr create-repository --repository-name myapp-backend --region ap-south-1
```

### 2. Authenticate Docker

```bash
aws ecr get-login-password --region ap-south-1 | \
docker login --username AWS --password-stdin <account-id>.dkr.ecr.ap-south-1.amazonaws.com
```

### 3. Tag Image

```bash
docker tag myapp-backend:v1 <account-id>.dkr.ecr.ap-south-1.amazonaws.com/myapp-backend:v1
```

### 4. Push Image

```bash
docker push <account-id>.dkr.ecr.ap-south-1.amazonaws.com/myapp-backend:v1
```

---

## 🔐 Security Best Practices

* Container runs as non-root user
* Sensitive files excluded via `.dockerignore`
* Environment variables used for DB credentials
* Minimal base image (Alpine)

---

## 🧪 Testing Endpoints

```bash
curl http://localhost:3000
curl http://localhost:3000/health
```

---

## 📊 Image Analysis

```bash
docker history myapp-backend:v1
docker scout cves myapp-backend:v1
```

---

## 💡 Key Learnings

* Docker multi-stage builds
* Container security practices
* Docker Compose orchestration
* AWS ECR usage
* Debugging container issues

---

## 🚀 Future Enhancements

* Add frontend (React)
* Deploy on Kubernetes (EKS)
* Add CI/CD pipeline (GitHub Actions)
* Add Nginx reverse proxy

---

## 👨‍💻 Author

Sudheer
DevOps & Cloud Enthusiast 🚀
