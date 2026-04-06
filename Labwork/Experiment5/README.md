📂 Part 1: Docker Volumes (Data Persistence)
Volumes are used to persist data beyond the lifecycle of a container.

1. Named Volumes
Bash
# Create a named volume
docker volume create my-persistent-data

# Run a container using the volume
docker run -d -v my-persistent-data:/app/data --name storage-container nginx

# Verify volume creation
docker volume ls
[INSERT SCREENSHOT: Output of 'docker volume ls']

2. Bind Mounts
Bash
# Create a local directory and mount it
mkdir ~/docker-lab
docker run -d -v ~/docker-lab:/usr/share/nginx/html:ro --name web-bind nginx
[INSERT SCREENSHOT: 'docker inspect web-bind' showing Source and Destination]

⚙️ Part 2: Environment Variables
Configuring applications dynamically without modifying the image.

Bash
# Run a container with custom environment variables
docker run -d \
  --name config-app \
  -e APP_COLOR=blue \
  -e VERSION=1.0 \
  alpine sleep 3600

# Check variables inside the container
docker exec config-app printenv
[INSERT SCREENSHOT: Terminal output of 'printenv']

📊 Part 3: Docker Monitoring
Real-time tracking of container performance and health.

Bash
# View real-time resource usage
docker stats --no-stream

# View container logs with timestamps
docker logs -t config-app
[INSERT SCREENSHOT: The 'docker stats' dashboard]

🌐 Part 4: Docker Networks
Enabling secure communication via a private bridge network.

Bash
# Create a custom bridge network
docker network create lab-network

# Run containers on the same network for DNS resolution
docker run -d --name db-server --network lab-network redis
docker run -d --name app-server --network lab-network alpine sleep 3600

# Test connectivity
docker exec app-server ping -c 2 db-server
[INSERT SCREENSHOT: Successful ping response between containers]

🚀 Part 5: Full Stack Example
Implementation of a Web App + Database + Cache architecture.

Bash
# 1. Database with Volume
docker run -d --name postgres-db --network lab-network -v pgdata:/var/lib/postgresql/data -e POSTGRES_PASSWORD=secret postgres:15

# 2. Redis Cache
docker run -d --name redis-cache --network lab-network redis:7-alpine

# 3. Web App
docker run -d --name flask-web -p 5000:5000 --network lab-network -e DB_URL="postgres://postgres:secret@postgres-db:5432/db" nginx
[INSERT SCREENSHOT: 'docker ps' showing all three services running]

🧹 Cleanup
Bash
# Reset the environment
docker stop $(docker ps -aq)
docker rm $(docker ps -aq)
docker volume prune -f
docker network prune -f
[INSERT SCREENSHOT: Empty Docker environment]

🛠 How to Push to GitHub (VS Code)
Initialize Git: Open the VS Code terminal and run git init.

Add Files: Run git add README.md (or use the Source Control icon on the left and click +).

Commit: Type your message (e.g., "Add Experiment 5 README") and click Commit.

Connect to GitHub: ```bash
git remote add origin 
git branch -M main

Push: Click Sync Changes in VS Code or run git push -u origin main.