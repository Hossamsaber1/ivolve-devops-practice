# Lab 9: Containerized Node.js and MySQL Stack Using Docker Compose

## Objective

Deploy a Node.js application connected to MySQL using Docker Compose, verify health endpoints, inspect logs, and push the Docker image to DockerHub.

---

## Project Structure

```text
lab9/
│── frontend/
│── db.js
│── Dockerfile
│── docker-compose.yml
│── package.json
│── server.js
│── README.md
```

---

## Step 1: Clone the Project

```bash
git clone https://github.com/Ibrahim-Adel15/kubernets-app.git
cd kubernets-app
```

---

## Step 2: Run Docker Compose

```bash
docker compose up -d --build
```

### Explanation

* `up` → Start containers
* `-d` → Run in background
* `--build` → Rebuild image before start

---

## Step 3: Verify Running Containers

```bash
docker ps
```

Expected:

* Node.js App container
* MySQL container

---

## Step 4: Verify App is Working

Open in browser:

```text
http://localhost:3000
```

Or use curl:

```bash
curl http://localhost:3000
```

---

## Step 5: Verify Health Endpoint

```bash
curl http://localhost:3000/health
```

Expected output:

```text
OK
```

---

## Step 6: Verify Ready Endpoint

```bash
curl http://localhost:3000/ready
```

Expected output:

```text
READY
```

---

## Step 7: Verify Access Logs

Enter app container:

```bash
docker exec -it ivolve-node-app sh
```

Check logs:

```bash
ls -la /app/logs
cat /app/logs/*
```

Exit:

```bash
exit
```

---

## Step 8: Build Docker Image

Replace `yourdockerhubusername` with your DockerHub username:

```bash
docker build -t yourdockerhubusername/ivolve-node-app:v1 .
```

---

## Step 9: Login to DockerHub

```bash
docker login
```

---

## Step 10: Push Image to DockerHub

```bash
docker push yourdockerhubusername/ivolve-node-app:v1
```

---

## Step 11: Stop Containers

```bash
docker compose down
```

---

## Step 12: Remove Containers + Volumes

```bash
docker compose down -v
```

---

## Useful Commands

### Show Logs

```bash
docker compose logs
```

### Show App Logs Only

```bash
docker compose logs app
```

### Show Database Logs Only

```bash
docker compose logs db
```

### Show Docker Images

```bash
docker images
```

---

## Architecture

```text
Browser
   |
localhost:3000
   |
Node.js App Container
   |
Docker Network
   |
MySQL Container
   |
Volume: db_data
```

---

## Skills Learned

* Docker Compose
* Multi-container Applications
* Node.js Containerization
* MySQL Containerization
* Volumes
* Environment Variables
* Health Checks
* DockerHub Push

---

## Author

Hossam Saber
