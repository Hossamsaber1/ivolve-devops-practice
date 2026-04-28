# Lab 8: Custom Docker Network for Microservices

## Objective
Build frontend and backend containers, connect them using a custom Docker network, and verify communication.

## 1. Clone Repository
```bash
git clone https://github.com/Ibrahim-Adel15/Docker5.git
cd Docker5
```

## 2. Frontend Dockerfile
Create `frontend/Dockerfile`

```dockerfile
FROM python:3.10-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python","app.py"]
```

## 3. Backend Dockerfile
Create `backend/Dockerfile`

```dockerfile
FROM python:3.10-slim
WORKDIR /app
COPY . .
RUN pip install flask
EXPOSE 5000
CMD ["python","app.py"]
```

## 4. Build Images
```bash
cd frontend && docker build -t frontend-image . && cd ..
cd backend && docker build -t backend-image . && cd ..
```

## 5. Create Network
```bash
docker network create ivolve-network
```

## 6. Run Containers (PowerShell)
```powershell
docker run -d --name backend --network ivolve-network backend-image
docker run -d --name frontend1 --network ivolve-network -p 5001:5000 frontend-image
docker run -d --name frontend2 -p 5002:5000 frontend-image
```

## 7. Verify
```bash
docker ps
docker network inspect ivolve-network
docker exec -it frontend1 curl http://backend:5000
```

## 8. Cleanup
```bash
docker stop backend frontend1 frontend2
docker rm backend frontend1 frontend2
docker network rm ivolve-network
```
