# Lab 4: Run Java Spring Boot App in a Container

## Objective
Run a Java Spring Boot application inside Docker using a Java 17 base image.

---

## 1. Clone Application Source Code

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1
```

---

## 2. Build the Application

```bash
mvn clean package
```

Verify the JAR file:

```bash
ls target/
```

Expected output:

```bash
demo-0.0.1-SNAPSHOT.jar
```

---

## 3. Create Dockerfile

```bash
nano Dockerfile
```

Paste the following:

```dockerfile
FROM openjdk:17-jdk-slim

WORKDIR /app

COPY target/demo-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]
```

---

## 4. Build Docker Image

```bash
docker build -t app2 .
```

Check image size:

```bash
docker images app2
```

---

## 5. Run Container

```bash
docker run -d --name container2 -p 8080:8080 app2
```

Check running containers:

```bash
docker ps
```

---

## 6. Test Application

Using curl:

```bash
curl http://localhost:8080
```

Or open browser:

```text
http://localhost:8080
```

---

## 7. Stop and Remove Container

```bash
docker stop container2
docker rm container2
```

Verify:

```bash
docker ps -a
```

