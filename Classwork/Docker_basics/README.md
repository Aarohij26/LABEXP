# 🐳 Docker Commands & Flags – HandsOn

A practical guide covering essential Docker commands with examples and screenshots.

---

## 📌 1. Docker Basics

### Check Docker Version

```bash
docker version
```

📸 Screenshot:
![docker version](images/docker-version.png)

```bash
docker info
```

📸 Screenshot:
![docker info](images/docker-info.png)

---

## 📦 2. Image Management

### List Images

```bash
docker images
```

📸
![docker images](images/docker-images.png)

### Pull Image

```bash
docker pull ubuntu
docker pull ubuntu:22.04
```

📸
![docker pull](images/docker-pull.png)

### Remove Image

```bash
docker rmi ubuntu
```

📸
![docker rmi](images/docker-rmi.png)

---

## 🔄 3. Container Lifecycle

### Run Container

```bash
docker run -it --name test ubuntu bash
```

📸
![docker run](images/docker-run.png)

### List Containers

```bash
docker ps
```

📸
![docker ps](images/docker-ps.png)

### Start / Stop / Restart

```bash
docker start test
docker stop test
docker restart test
```

📸
![docker lifecycle](images/docker-start-stop.png)

### Remove Container

```bash
docker rm test
```

📸
![docker rm](images/docker-rm.png)

---

## 💻 4. Execute Commands Inside Container

```bash
docker exec -it test bash
```

📸
![docker exec](images/docker-exec.png)

---

## 🌐 5. Networking & Ports

### Port Mapping

```bash
docker run -d -p 8080:80 nginx
```

📸
![port mapping](images/docker-port.png)

### List Networks

```bash
docker network ls
```

📸
![network list](images/docker-network-ls.png)

### Create Network

```bash
docker network create mynet
```

📸
![network create](images/docker-network-create.png)

---

## 💾 6. Volumes & Data Persistence

```bash
docker volume create mydata
docker run -v mydata:/data ubuntu
```

📸
![volume](images/docker-volume.png)

---

## 📊 7. Logs & Monitoring

### View Logs

```bash
docker logs test
```

📸
![logs](images/docker-logs.png)

### Resource Usage

```bash
docker stats
```

📸
![stats](images/docker-stats.png)

---

## 🔍 8. Inspect & Metadata

```bash
docker inspect test
```

📸
![inspect](images/docker-inspect.png)

---

## 🏗️ 9. Build Docker Image

```bash
docker build -t myapp .
```

📸
![build](images/docker-build.png)

### Example Dockerfile

```Dockerfile
FROM ubuntu:22.04
RUN apt update && apt install -y nginx
CMD ["nginx", "-g", "daemon off;"]
```

📸
![dockerfile](images/dockerfile.png)

---

## 🧹 10. Cleanup Commands

```bash
docker container prune
docker image prune
docker system prune
```

📸
![cleanup](images/docker-cleanup.png)

---

## ⚙️ 11. Docker Compose

```bash
docker compose up -d --build
docker compose down
```

📸
![compose](images/docker-compose.png)

---

## 🚀 12. Important Run Flags

| Flag      | Meaning              |
| --------- | -------------------- |
| -it       | Interactive terminal |
| -d        | Detached mode        |
| --rm      | Auto remove          |
| --name    | Container name       |
| -p        | Port mapping         |
| -v        | Volume               |
| -e        | Environment variable |
| --network | Custom network       |

---

## 🧪 13. Minimal Lab Example

```bash
docker pull nginx
docker run -d --name web -p 8080:80 nginx
docker ps
docker logs web
docker stop web
docker rm web
```

📸
![lab](images/docker-lab.png)

---

## 🧠 14. Key Concepts

* **Image** → Blueprint
* **Container** → Running instance
* **Volume** → Persistent storage
* **Network** → Communication
* **Dockerfile** → Build instructions

---

## 📁 Folder Structure

```
project/
│── README.md
│── images/
    ├── docker-version.png
    ├── docker-info.png
    ├── docker-images.png
    ├── ...
```

---

## 💡 Tip

Take screenshots using:

* `Win + Shift + S` (Windows)
* Save inside `/images` folder
* Match file names exactly as above

---
