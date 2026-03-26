#  DevOps Full-Stack App (Docker + AWS ECR)

##  Overview

This project demonstrates how to containerize a Node.js backend using **multi-stage Docker builds**, orchestrate services with **Docker Compose**, and push images to **AWS ECR**.

It follows production-level DevOps practices including security, optimization, and modular deployment.

---

##  Architecture

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

##  Key Features

* Multi-stage Docker build (optimized image)
* Non-root user inside container (security best practice)
* Docker Compose orchestration (App + DB)
* MySQL with persistent volume
* AWS ECR integration
* Health check endpoint (`/health`)

---

##  Docker Optimization

| Feature           | Benefit                              |
| ----------------- | ------------------------------------ |
| Multi-stage build | Smaller image size (~400MB → <100MB) |
| Alpine base image | Lightweight & fast                   |
| .dockerignore     | Faster builds                        |
| Non-root user     | Improved security                    |



## Run Locally (Without Docker)

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

## Run with Docker

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

##  Run with Docker Compose (Recommended)

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

##  Push to AWS ECR

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

## Security Best Practices

* Container runs as non-root user
* Sensitive files excluded via `.dockerignore`
* Environment variables used for DB credentials
* Minimal base image (Alpine)

---

##  Testing Endpoints

```bash
curl http://localhost:3000
curl http://localhost:3000/health
```

---

## Image Analysis

```bash
docker history myapp-backend:v1
docker scout cves myapp-backend:v1
```
<img width="1172" height="437" alt="Screenshot" src="https://github.com/user-attachments/assets/8a845fbc-4e38-477a-b82b-ebb74839bab3" />

---
<img width="1452" height="402" alt="Screenshot1" src="https://github.com/user-attachments/assets/d2cf1919-c97a-4f28-bd6b-3cbe1c2f578f" />

## Key Learnings

* Docker multi-stage builds
* Container security practices
* Docker Compose orchestration
* AWS ECR usage
* Debugging container issues

---



## Author

Sudheer
DevOps Engineer 
