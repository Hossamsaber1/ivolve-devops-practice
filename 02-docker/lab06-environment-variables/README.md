# Lab 6: Managing Docker Environment Variables Across Build and Runtime

This lab explains how to build and run a Flask Python application using Docker, and how to manage environment variables at runtime using:

1. Environment variables directly in the `docker run` command.
2. Environment variables from a separate `.env` file.
3. Environment variables defined inside the `Dockerfile`.

---

## Lab Requirements

- Clone the application code:
  ```bash
  git clone https://github.com/Ibrahim-Adel15/Docker-3.git
  ```

- Write a `Dockerfile`:
  - Use a Python base image.
  - Install Flask.
  - Expose port `8080`.
  - Run the application using `python app.py`.

- Build the Docker image.
- Run 3 containers with different values for:
  - `APP_MODE`
  - `APP_REGION`

---

## 1. Clone the Repository

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-3.git
cd Docker-3
```

---

## 2. Create the Dockerfile

Create a file named `Dockerfile`:

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY . .

RUN pip install flask

ENV APP_MODE=production
ENV APP_REGION=canada-west

EXPOSE 8080

CMD ["python", "app.py"]
```

---

## 3. Build the Docker Image

```bash
docker build -t flask-env-app .
```

Check the image:

```bash
docker images
```

---

## 4. Run Container 1 Using Environment Variables in the Command

Values:

- `APP_MODE=development`
- `APP_REGION=us-east`

```bash
docker run -d --name container-dev -p 8081:8080 \
  -e APP_MODE=development \
  -e APP_REGION=us-east \
  flask-env-app
```

Test the application:

```bash
curl http://localhost:8081
```

---

## 5. Run Container 2 Using an Environment File

Create a file named `staging.env`:

```env
APP_MODE=staging
APP_REGION=us-west
```

Run the container:

```bash
docker run -d --name container-staging -p 8082:8080 \
  --env-file staging.env \
  flask-env-app
```

Test the application:

```bash
curl http://localhost:8082
```

---

## 6. Run Container 3 Using Environment Variables from the Dockerfile

The following values are already defined inside the `Dockerfile`:

```dockerfile
ENV APP_MODE=production
ENV APP_REGION=canada-west
```

Run the container without passing any environment variables:

```bash
docker run -d --name container-prod -p 8083:8080 flask-env-app
```

Test the application:

```bash
curl http://localhost:8083
```

---

## 7. Check Running Containers

```bash
docker ps
```

---

## 8. Check Environment Variables Inside Each Container

Development container:

```bash
docker exec container-dev env | grep APP
```

Staging container:

```bash
docker exec container-staging env | grep APP
```

Production container:

```bash
docker exec container-prod env | grep APP
```

Expected output examples:

```bash
APP_MODE=development
APP_REGION=us-east
```

```bash
APP_MODE=staging
APP_REGION=us-west
```

```bash
APP_MODE=production
APP_REGION=canada-west
```

---

## 9. Stop and Delete Containers

```bash
docker stop container-dev container-staging container-prod
docker rm container-dev container-staging container-prod
```

---

## 10. Delete the Docker Image Optional

```bash
docker rmi flask-env-app
```

---

## Full Command Summary

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-3.git
cd Docker-3

cat > Dockerfile <<'EOF'
FROM python:3.12-slim

WORKDIR /app

COPY . .

RUN pip install flask

ENV APP_MODE=production
ENV APP_REGION=canada-west

EXPOSE 8080

CMD ["python", "app.py"]
EOF

docker build -t flask-env-app .

docker run -d --name container-dev -p 8081:8080 \
  -e APP_MODE=development \
  -e APP_REGION=us-east \
  flask-env-app

cat > staging.env <<'EOF'
APP_MODE=staging
APP_REGION=us-west
EOF

docker run -d --name container-staging -p 8082:8080 \
  --env-file staging.env \
  flask-env-app

docker run -d --name container-prod -p 8083:8080 flask-env-app

curl http://localhost:8081
curl http://localhost:8082
curl http://localhost:8083

docker exec container-dev env | grep APP
docker exec container-staging env | grep APP
docker exec container-prod env | grep APP

docker stop container-dev container-staging container-prod
docker rm container-dev container-staging container-prod
```

---

## Notes

- `-e` is used to pass environment variables directly in the `docker run` command.
- `--env-file` is used to load environment variables from a separate file.
- `ENV` inside the Dockerfile defines default environment variables inside the image.
- Runtime environment variables override Dockerfile `ENV` values.
- Each container uses a different host port:
  - Development: `8081`
  - Staging: `8082`
  - Production: `8083`
