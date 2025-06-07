---
title: Docker Commands
description: This is a blog contains some useful and common docker commands.
date: 03/18/2024
---

Here’s a comprehensive list of **Docker** and **Docker Compose** commands with explanations and examples:

---

## **Docker Commands**

### **1. Docker Version & Info**

-   `docker --version` → Check Docker version
    ```sh
    docker --version
    ```
-   `docker info` → Display system-wide Docker information
    ```sh
    docker info
    ```

### **2. Docker Image Commands**

-   `docker images` → List all locally stored images
    ```sh
    docker images
    ```
-   `docker pull <image>` → Download an image from Docker Hub
    ```sh
    docker pull nginx
    ```
-   `docker rmi <image>` → Remove an image
    ```sh
    docker rmi nginx
    ```

### **3. Docker Container Commands**

-   `docker ps` → List running containers
    ```sh
    docker ps
    ```
-   `docker ps -a` → List all containers (including stopped ones)
    ```sh
    docker ps -a
    ```
-   `docker run <image>` → Run a container from an image
    ```sh
    docker run nginx
    ```
-   `docker run -d -p <host-port>:<container-port> <image>` → Run container in detached mode with port mapping
    ```sh
    docker run -d -p 8080:80 nginx
    ```
-   `docker run --name <name> <image>` → Run container with a custom name
    ```sh
    docker run --name mynginx nginx
    ```
-   `docker stop <container>` → Stop a running container
    ```sh
    docker stop mynginx
    ```
-   `docker start <container>` → Start a stopped container
    ```sh
    docker start mynginx
    ```
-   `docker restart <container>` → Restart a container
    ```sh
    docker restart mynginx
    ```
-   `docker rm <container>` → Remove a container
    ```sh
    docker rm mynginx
    ```

### **4. Docker Logs & Exec Commands**

-   `docker logs <container>` → View logs of a container
    ```sh
    docker logs mynginx
    ```
-   `docker exec -it <container> <command>` → Execute a command inside a running container
    ```sh
    docker exec -it mynginx bash
    ```
-   `docker attach <container>` → Attach to a running container
    ```sh
    docker attach mynginx
    ```

### **5. Docker Networks**

-   `docker network ls` → List all networks
    ```sh
    docker network ls
    ```
-   `docker network create <name>` → Create a custom network
    ```sh
    docker network create mynetwork
    ```
-   `docker network connect <network> <container>` → Connect a container to a network
    ```sh
    docker network connect mynetwork mynginx
    ```
-   `docker network disconnect <network> <container>` → Disconnect a container from a network
    ```sh
    docker network disconnect mynetwork mynginx
    ```
-   `docker network rm <name>` → Remove a network
    ```sh
    docker network rm mynetwork
    ```

### **6. Docker Volumes**

-   `docker volume ls` → List all volumes
    ```sh
    docker volume ls
    ```
-   `docker volume create <name>` → Create a new volume
    ```sh
    docker volume create myvolume
    ```
-   `docker volume rm <name>` → Remove a volume
    ```sh
    docker volume rm myvolume
    ```

### **7. Docker Build & Compose**

-   `docker build -t <name>:<tag> <path>` → Build an image from a Dockerfile
    ```sh
    docker build -t myapp:latest .
    ```
-   `docker compose up -d` → Start services in the background
    ```sh
    docker compose up -d
    ```
-   `docker compose down` → Stop and remove containers
    ```sh
    docker compose down
    ```

---

## **Docker Compose Commands**

### **1. Start and Stop Containers**

-   `docker compose up` → Start containers defined in `docker-compose.yml`
    ```sh
    docker compose up
    ```
-   `docker compose up -d` → Start in detached mode
    ```sh
    docker compose up -d
    ```
-   `docker compose down` → Stop and remove containers
    ```sh
    docker compose down
    ```

### **2. Managing Services**

-   `docker compose start` → Start services
    ```sh
    docker compose start
    ```
-   `docker compose stop` → Stop services
    ```sh
    docker compose stop
    ```
-   `docker compose restart` → Restart services
    ```sh
    docker compose restart
    ```
-   `docker compose pause` → Pause services
    ```sh
    docker compose pause
    ```
-   `docker compose unpause` → Resume paused services
    ```sh
    docker compose unpause
    ```

### **3. Logs & Monitoring**

-   `docker compose logs` → View logs of all services
    ```sh
    docker compose logs
    ```
-   `docker compose logs -f` → Follow logs in real time
    ```sh
    docker compose logs -f
    ```

### **4. Executing Commands in Containers**

-   `docker compose exec <service> <command>` → Run a command in a running container
    ```sh
    docker compose exec web ls
    ```

### **5. Managing Volumes & Networks**

-   `docker compose ps` → List running containers in the compose setup
    ```sh
    docker compose ps
    ```
-   `docker compose config` → Validate and view compose file configuration
    ```sh
    docker compose config
    ```
-   `docker compose rm` → Remove stopped service containers
    ```sh
    docker compose rm
    ```
-   `docker compose build` → Build images defined in `docker-compose.yml`
    ```sh
    docker compose build
    ```

---

This list covers most **Docker** and **Docker Compose** commands you need! 🚀 Let me know if you need more details. 😊
