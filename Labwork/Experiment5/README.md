Gemini said
To push this to GitHub using VS Code, you can copy the content below into a new file named README.md. I have formatted it to match the style of your reference while including placeholders for your screenshots.

Experiment 3: Docker Deploy NGINX & Image Layer Comparison
This lab explores deploying NGINX using three different approaches: the Official Image, an Ubuntu-based custom image, and an Alpine-based custom image, followed by a detailed comparison of image sizes and layers.

🛠 Part 1: Deploy NGINX Using Official Image
The recommended approach for standard production deployments.

Step 1: Pull the Image
Bash
docker pull nginx:latest
[INSERT SCREENSHOT: Output of 'docker pull nginx:latest']

Step 2: Run the Container
Bash
docker run -d --name nginx-official -p 8080:80 nginx
[INSERT SCREENSHOT: Output of 'docker run' showing the container ID]

Step 3: Verify
Bash
curl http://localhost:8080
[INSERT SCREENSHOT: NGINX welcome page or terminal curl output]

🐧 Part 2: Custom NGINX Using Ubuntu Base Image
Used when full OS utilities are required for debugging or complex dependencies.

Step 1: Create Dockerfile
Dockerfile
FROM ubuntu:22.04

RUN apt-get update && \
    apt-get install -y nginx && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
[INSERT SCREENSHOT: VS Code editor showing the Ubuntu Dockerfile]

Step 2: Build and Run
Bash
docker build -t nginx-ubuntu .
docker run -d --name nginx-ubuntu -p 8081:80 nginx-ubuntu
[INSERT SCREENSHOT: Terminal output of the 'docker build' process]

🏔 Part 3: Custom NGINX Using Alpine Base Image
The preferred choice for microservices due to its minimal footprint.

Step 1: Create Dockerfile
Dockerfile
FROM alpine:latest

RUN apk add --no-cache nginx

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
[INSERT SCREENSHOT: VS Code editor showing the Alpine Dockerfile]

Step 2: Build and Run
Bash
docker build -t nginx-alpine .
docker run -d --name nginx-alpine -p 8082:80 nginx-alpine
[INSERT SCREENSHOT: Terminal output of the 'docker build -t nginx-alpine' command]

📊 Part 4: Image Size and Layer Comparison
Compare Sizes
Bash
docker images | grep nginx
[INSERT SCREENSHOT: List of nginx, nginx-ubuntu, and nginx-alpine with their sizes]

Image Type	Size (Approx)	Efficiency
nginx:latest	187 MB	Medium
nginx-ubuntu	200+ MB	Large
nginx-alpine	16 MB	Very Small
Inspect History
Bash
docker history nginx-alpine
[INSERT SCREENSHOT: Output of 'docker history' showing image layers]

🧹 Cleanup & Git Push (VS Code Instructions)
1. Cleanup Docker
Bash
docker stop nginx-official nginx-ubuntu nginx-alpine
docker rm nginx-official nginx-ubuntu nginx-alpine
2. Push to GitHub
Open Source Control (Ctrl+Shift+G): Click the Initialize Repository button.

Stage Changes: Click the + icon next to README.md and your Dockerfiles.

Commit: Type Add Experiment 3 Documentation and click Commit.

Publish: Click Publish Branch to sync with your GitHub repository.

