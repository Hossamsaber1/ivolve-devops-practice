# Lab 3: Run Java Spring Boot App in a Container

## Objective
Clone a Java Spring Boot application, create a Docker image, run the container, test the application, then remove the container.

---

## Step 1: Clone the Application Source Code

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1
```

---

## Step 2: Create Dockerfile

```bash
nano Dockerfile
```

Paste the following content:

```dockerfile
FROM maven:3.9.6-eclipse-temurin-17

WORKDIR /app

COPY . .

RUN mvn package

EXPOSE 8080

CMD ["java", "-jar", "target/demo-0.0.1-SNAPSHOT.jar"]
```

---

## Step 3: Build Docker Image

```bash
docker build -t app1 .
docker images
```

---

## Step 4: Run Container

```bash
docker run -d --name container1 -p 8080:8080 app1
docker ps
docker ps -a
```

---

## Step 5: Test Application

```bash
curl http://localhost:8080
```

Open browser:

http://localhost:8080

---

## Step 6: View Logs

```bash
docker logs container1
docker logs -f container1
```

---

## Step 7: Access Container Shell

```bash
docker exec -it container1 bash
```

---

## Step 8: Stop and Remove Container

```bash
docker stop container1
docker rm container1
```

---

## Step 9: Remove Docker Image

```bash
docker rmi app1
```

---

## Full Cleanup

```bash
docker stop container1
docker rm container1
docker rmi app1
```
