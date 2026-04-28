# Lab 7: Docker Volume and Bind Mount with Nginx

## Docker Run Command Explanation

```bash
docker run -d \
--name nginx-lab7 \
-p 8080:80 \
-v nginx_logs:/var/log/nginx \
-v $(pwd)/nginx-bind/html:/usr/share/nginx/html \
nginx
```

---

## Overview

This command starts an Nginx container in background mode with:

* Custom container name
* Port mapping
* Docker volume for logs
* Bind mount for website files

---

## Command Breakdown

### 1. Run Container

```bash
docker run
```

Creates and starts a new container from image.

---

### 2. Detached Mode

```bash
-d
```

Runs container in background.

You can continue using terminal.

---

### 3. Container Name

```bash
--name nginx-lab7
```

Sets container name to:

```text
nginx-lab7
```

Useful commands:

```bash
docker stop nginx-lab7
docker logs nginx-lab7
docker exec -it nginx-lab7 bash
```

---

### 4. Port Mapping

```bash
-p 8080:80
```

Maps ports:

| Host Port | Container Port |
| --------- | -------------- |
| 8080      | 80             |

Access website from browser:

```text
http://localhost:8080
```

---

### 5. Docker Volume for Logs

```bash
-v nginx_logs:/var/log/nginx
```

Mounts Docker volume:

| Volume Name | Container Path |
| ----------- | -------------- |
| nginx_logs  | /var/log/nginx |

Used for persistent logs:

* access.log
* error.log

Logs remain even if container is removed.

---

### 6. Bind Mount for HTML Files

```bash
-v $(pwd)/nginx-bind/html:/usr/share/nginx/html
```

Maps host folder to container folder:

| Host Path                      | Container Path        |
| ------------------------------ | --------------------- |
| Current Folder/nginx-bind/html | /usr/share/nginx/html |

Used for website files such as:

```text
index.html
```

Any file change on host updates website instantly.

---

### 7. Current Directory Variable

```bash
$(pwd)
```

Means current working directory.

Example:

```text
/home/hossam/lab7
```

So full path becomes:

```text
/home/hossam/lab7/nginx-bind/html
```

---

### 8. Image Name

```bash
nginx
```

Uses official Nginx image from Docker Hub.

---

## Architecture Flow

```text
Browser
   |
localhost:8080
   |
   v
Nginx Container (Port 80)
   |                |
   |                |
Logs Volume     Bind Mount HTML
```

---

## Verification

Check running container:

```bash
docker ps
```

Test page:

```bash
curl http://localhost:8080
```

---

## Benefits

| Feature       | Benefit           |
| ------------- | ----------------- |
| Detached Mode | Run in background |
| Port Mapping  | Access website    |
| Volume        | Persistent logs   |
| Bind Mount    | Live file editing |

---

## Cleanup

```bash
docker stop nginx-lab7
docker rm nginx-lab7
docker volume rm nginx_logs
```

---

## Result

Successfully deployed Nginx using:

* Docker Volume for logs
* Bind Mount for website content
* Port publishing for browser access
