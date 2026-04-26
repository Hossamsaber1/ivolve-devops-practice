## Lab 5: Multi-Stage Build for Java Spring Boot App

### Objective

Build and run a Java Spring Boot application using Docker Multi-Stage Build to reduce final image size.

---

## Step 1: Clone Repository

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1
```

---

## Step 2: Create Dockerfile

```bash
nano Dockerfile
```

Paste the following:

```dockerfile
# ===============================
# Stage 1 - Build Stage
# ===============================
FROM maven:3.9.6-eclipse-temurin-17 AS build

WORKDIR /app

COPY . .

RUN mvn clean package -DskipTests

# ===============================
# Stage 2 - Runtime Stage
# ===============================
FROM eclipse-temurin:17-jre

WORKDIR /app

COPY --from=build /app/target/demo-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]
```

Save and exit.

---

## Step 3: Build Docker Image

```bash
docker build -t app3 .
```

Check image size:

```bash
docker images app3
```

---

## Step 4: Run Container

```bash
docker run -d --name container3 -p 8080:8080 app3
```

---

## Step 5: Test Application

Browser:

```text
http://localhost:8080
```

Or using curl:

```bash
curl http://localhost:8080
```

---

## Step 6: View Running Container

```bash
docker ps
```

---

## Step 7: Stop Container

```bash
docker stop container3
```

---

## Step 8: Remove Container

```bash
docker rm container3
```

---

## Step 9: Remove Image (Optional)

```bash
docker rmi app3
```

---

## Full Commands Summary

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1

nano Dockerfile

docker build -t app3 .

docker images app3

docker run -d --name container3 -p 8080:8080 app3

curl http://localhost:8080

docker stop container3

docker rm container3
```

---

## Expected Result

* Multi-stage image built successfully
* Smaller final image size than single-stage build
* Application accessible on port **8080**
