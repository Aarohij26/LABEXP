# 🚀 Experiment 4: Docker Essentials

This experiment demonstrates Docker basics: containerizing apps, building images, running containers, multi-stage builds, and publishing to Docker Hub.

--------------------------------------------------

## 🐍 Part 1: Flask Application

### Create App
mkdir my-flask-app
cd my-flask-app

app.py
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello from Docker!"

@app.route('/health')
def health():
    return "OK"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)

requirements.txt
Flask==2.3.3

### Dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY app.py .
EXPOSE 5000
CMD ["python", "app.py"]

--------------------------------------------------

## 🚫 Part 2: .dockerignore

__pycache__/
*.pyc
.env
venv/
.vscode/
.git/
.DS_Store
*.log
tests/

Why:
- Reduces image size
- Faster builds
- Better security

--------------------------------------------------

## 🏗️ Part 3: Build Images

docker build -t my-flask-app .
docker build -t my-flask-app:1.0 .
docker build -t my-flask-app:latest -t my-flask-app:1.0 .
docker images

--------------------------------------------------

## ▶️ Part 4: Run Containers

docker run -d -p 5000:5000 --name flask-container my-flask-app
curl http://localhost:5000
docker logs flask-container

Manage:
docker stop flask-container
docker start flask-container
docker rm flask-container
docker rm -f flask-container

--------------------------------------------------

## ⚡ Part 5: Multi-stage Build

FROM python:3.9-slim AS builder
WORKDIR /app
COPY requirements.txt .
RUN python -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
RUN pip install -r requirements.txt

FROM python:3.9-slim
WORKDIR /app
COPY --from=builder /opt/venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
COPY app.py .
RUN useradd -m appuser
USER appuser
EXPOSE 5000
CMD ["python", "app.py"]

Build:
docker build -t flask-regular .
docker build -f Dockerfile.multistage -t flask-multistage .
docker images | grep flask

--------------------------------------------------

## ☁️ Part 6: Docker Hub

docker login
docker tag my-flask-app username/my-flask-app:1.0
docker push username/my-flask-app:1.0

Pull:
docker pull username/my-flask-app:latest
docker run -d -p 5000:5000 username/my-flask-app:latest

--------------------------------------------------

## 🟢 Part 7: Node.js Example

docker build -t my-node-app .
docker run -d -p 3000:3000 --name node-container my-node-app
curl http://localhost:3000

--------------------------------------------------

## 🧪 Part 8: Practice

docker build -t myapp:latest -t myapp:v2.0 -t username/myapp:production .
docker build --no-cache -t clean-app .

--------------------------------------------------

## 📌 Docker Cheatsheet

docker build     -> Build image
docker run       -> Run container
docker ps        -> List containers
docker images    -> List images
docker tag       -> Tag image
docker push      -> Push image
docker pull      -> Pull image
docker rm        -> Remove container
docker rmi       -> Remove image
docker logs      -> View logs
docker exec      -> Run command

--------------------------------------------------

## 🔄 Workflow

Development:
docker build -t myapp .
docker run -p 8080:8080 myapp
docker tag myapp myapp:v1.0
docker push myapp:v1.0

Production:
docker pull myapp:v1.0
docker run -d -p 80:8080 myapp:v1.0
docker logs -f myapp

--------------------------------------------------

## 🎯 Key Takeaways

- Dockerfile builds images
- .dockerignore improves speed & security
- Tagging helps versioning
- Multi-stage reduces size
- Docker Hub for sharing
- Always test locally

--------------------------------------------------

## 🧹 Cleanup

docker container prune
docker image prune
docker system prune -a