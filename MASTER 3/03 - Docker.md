---
cover: "[[docker.webp]]"
---
# 💠 Table of Contents
```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 2 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```

---

# 💠 What is Docker?

Docker is a **containerization platform** that enables developers to package applications and their dependencies into **lightweight, portable, and self-sufficient containers**. These containers run consistently across different environments, eliminating the "it works on my machine" problem.

**Key Benefits of Docker:**

- **Portability** – Runs the same way on development, testing, and production environments.
- **Lightweight** – Shares the host OS kernel, reducing resource usage compared to VMs.
- **Scalability** – Easily scale applications by running multiple containers.
- **Isolation** – Each container runs independently with its own dependencies.
- **Fast Deployment** – Containers can start in milliseconds.

> 💡 *Docker only works on UNIX kernel. On Windows, Docker Desktop creates Linux VM to run Docker.*

---

# 💠 **Containers vs VM**

|**Feature**|**Virtual Machines (VMs)**|**Containers (Docker)**|
|---|---|---|
|**Size**|Heavy (GBs, includes OS)|Lightweight (MBs, shares OS kernel)|
|**Startup Time**|Slow (minutes)|Fast (seconds or less)|
|**Isolation**|Strong (separate OS)|Process-level isolation|
|**Performance**|Requires more resources|More efficient most of the time (except high I/O), shares OS resources|
|**Portability**|Less portable|High portability across environments|

---

# 💠 **Docker Architecture**

Docker follows a **client-server architecture** consisting of:

- **Docker Client** – CLI (`docker`) or GUI used to interact with Docker.
- **Docker Daemon (`dockerd`)** – Runs in the background, managing containers.
- **Docker Images** – Blueprints for containers, built from `Dockerfile`.
- **Docker Containers** – Running instances of Docker images.
- **Docker Registry (Docker Hub, Private Registries)** – Stores and distributes Docker images.

---

# 💠 **Basic Commands**

| **Command**                      | **Description**                         |
| -------------------------------- | --------------------------------------- |
| `docker --version`               | Check installed Docker version          |
| `docker pull <image>`            | Download an image from Docker Hub       |
| `docker images`                  | List available images on the system     |
| `docker run <image>`             | Run a container from an image           |
| `docker ps`                      | List running containers                 |
| `docker ps -a`                   | List all containers (running & stopped) |
| `docker stop <container>`        | Stop a running container                |
| `docker rm <container>`          | Remove a stopped container              |
| `docker rm $(docker ps -aq)`     | Remove all stopped containers           |
| `docker rm -f <container>`       | Force remove a container                |
| `docker rmi <image>`             | Remove an image                         |
| `docker exec -it <container> sh` | Access a running container via terminal |
### **Example:**

```bash
docker run -d -p 80:8080 nginx
```

This runs an **NGINX** container in detached mode (`-d`) and maps **port 80** of the host to **port 8080** of the container.

---

# 💠 **Images & Dockerfiles**

A **Docker Image** is a lightweight, standalone, and executable software package that includes everything needed to run an application (code, runtime, libraries, dependencies, and configuration files).

A **Dockerfile** is a script that contains instructions to build a Docker image. Official images can be found on **Docker Hub** ([https://hub.docker.com/](https://hub.docker.com/)).

### Example `Dockerfile`:
```docker
# Use a base image
FROM node:18-alpine

# Set the working directory
WORKDIR /app

# Copy package.json and install dependencies
# Allows to use cache and only running npm install when package.json changes
COPY package.json .
RUN npm install

# Copy the source code
COPY . .

# Expose container's port 3000
EXPOSE 3000

# Start the application
ENTRYPOINT ["npm", "start"]
```

> 💡 *Use an `alpine` or `slim` version for a lightweight image.*

> ⚠️ *Always specify a version tag of the image, otherwise it uses `latest` and can broke with later versions.*

### Building and Running an Image

```bash
docker build -t myapp .
docker run -d -p 3000:3000 myapp
```

---

# 💠 **Volumes & Persistent Data**

By default, when a container stops, its data is lost. **Docker Volumes** allow data to persist across container restarts. There are 2 types of volumes:

1. **Named Volumes** – Managed by Docker, designed for containerized applications.
2. **Bind Mounts** – Maps a specific host directory to a container directory.

## 1. Named Volumes

```bash
# Create a named volume
docker volume create mydata

# Run a container with a volume attached
docker run -d --name mycontainer -v mydata:/app/data myapp

# Inspect a volume
docker volume inspect mydata

# List existing volume
docker volume ls

# Remove a volume
docker volume rm mydata
```

> ⚠️ *A volume cannot be removed if it is currently being used by any running container.*

## 2. Bind Mounts

```bash
# Run a container with a bind mount attached
docker run -d --name mycontainer -v /home/user/data:/app/data:ro myapp
```

>💡*Use `:ro` when the containers doesn’t need to write in the bind mount.*

In this case:

- **`/home/user/data`** (host directory) is mounted into **`/app/data`** (inside the container).
- Changes made in **`/home/user/data`** on the host will reflect inside the container.

## 3. Bind Mounts vs Named Volumes

| **Feature**     | **Bind Mount**               | **Named Volume**                               |
| --------------- | ---------------------------- | ---------------------------------------------- |
| **Location**    | Any host path                | Managed by Docker (`/var/lib/docker/volumes/`) |
| **Persistence** | Exists outside container     | More reliable                                  |
| **Performance** | Slower on some platforms     | Optimized by Docker                            |
| **Use Case**    | Development and config files | Production, databases and stateful apps        |
## 4. When to Use?

|**Scenario**|**Recommended Option**|
|---|---|
|Database storage (PostgreSQL, MySQL)|**Named Volume**|
|Sharing data between containers|**Named Volume**|
|Storing logs, configuration files|**Named Volume**|
|Development with live code updates (hot-reload)|**Bind Mount**|
|Accessing specific system files|**Bind Mount**|

---

# 💠 **Networking**

Docker provides several networking options to manage communication between containers and the outside world.

## 1. Types of Docker Networks

|**Network Type**|**Description**|
|---|---|
|**Bridge (default)**|Containers communicate internally|
|**Host**|Shares the host’s networking stack (no isolation)|
|**None**|No networking for the container|
|**Overlay**|Enables networking between multiple Docker hosts (for Swarm mode)|

## 2. Creating and Using Networks

```bash
docker network create mynetwork
docker run -d --network=mynetwork --name=app1 myapp
docker run -d --network=mynetwork --name=app2 myapp
```

This allows `app1` and `app2` to communicate using their **container names** instead of IP addresses.

---

# 💠 **Docker Compose**

## 1. Example File

A **`docker-compose.yml`** file describes the **services**, **networks**, and **volumes** used by an application. Below is a detailed example:

```yaml
services:
  app:
	  build: . # Location of the Dockerfile building the image
    image: app
    ports:
      - "8080:80"  # Maps port 8080 on host to 80 in the container
    depends_on:
      - database  # Ensures database starts before the web service
    networks:
      - app_network

  database:
    image: postgres
    restart: unless-stopped  # Automatically restart unless manually stopped
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydb
    volumes:
      - db_data:/var/lib/postgresql/data  # Persist database data
    networks:
      - app_network

volumes:
  db_data:  # Named volume for database persistence

networks:
  app_network:  # Custom bridge network for isolated communication

```

> ⚠️ *Some `docker-compose.yml` might have a `version: "3.x"` on the first line. This is now depreciated.*

## 2. Services

Each service defines a container **running an application**. Key options:

- **`build`** – Specifies the location of the Dockerfile to build (not needed if the image is fetched from an image repository)
- **`image`** – Specifies the base image (e.g., `nginx`, `postgres`).
- **`ports`** – Maps container ports to the host.
- **`environment`** – Defines environment variables for the container.
- **`env_file`** – Defines environment file for the container, instead of **`environment`**
- **`volumes`** – Attaches persistent storage to a service.
- **`depends_on`** – Ensures the **order of service startup** but does not guarantee readiness (use health checks for that).
- **`restart`** – Defines container restart policy:
    - `no` (default) – Do not restart automatically.
    - `always` – Restart the container unconditionally.
    - `unless-stopped` – Restart unless manually stopped.
    - `on-failure` – Restart only on failure.

## 3. Volumes

Defines **persistent storage** to avoid data loss when containers restart.

## 4. Networks

By default, services **share a common network**.

- A **custom network** (e.g., `app_network`) isolates communication between services.
- You can specify network types:
    ```yaml
    networks:
      app_network:
        driver: bridge  # Default network driver
    ```

## 5. Common Docker Compose Commands

|**Command**|**Description**|
|---|---|
|`docker-compose up -d`|Start all services in detached mode (background).|
|`docker-compose up --build`|Rebuild images before starting containers.|
|`docker-compose up --force-recreate`|Restarts all services|
|`docker-compose restart <service>`|Restarts a specific service.|
|`docker-compose down`|Stop and remove all services defined in the file.|
|`docker-compose down -v`|Stop services and delete volumes (data will be lost).|
|`docker-compose ps`|Lists all running services.|
|`docker-compose logs`|Displays logs from all services.|
|`docker-compose exec <service> bash`|Open an interactive shell in a running container.|
|`docker-compose scale <service>=3`|Scale a service to multiple instances.|

## 6. Using `docker-compose.override.yml` for Environment-Specific Configurations

Instead of modifying the main `docker-compose.yml` file for different environments (development, testing, production), **Docker Compose allows overriding configurations** using a `docker-compose.override.yml` file :

- The `docker-compose.override.yml` file **automatically applies changes** when running `docker-compose up`.
- Useful for **adding dev-specific settings**, **debugging**, or **modifying configurations without changing the main file**.

**Example: `docker-compose.override.yml` (Development Setup)**
```yaml
services:
  app:
    build:
      context: .
      dockerfile: Dockerfile.dev  # Use a development Dockerfile
    volumes:
      - .:/app  # Mounts source code for live editing
    environment:
      DEBUG: "true"
      
  database:
    environment:
      POSTGRES_PASSWORD: devpassword  # Different password for development
```

**Running with an Override**
```bash
docker-compose up -d
```
- **No extra flags needed** – Compose **automatically detects** and applies overrides.
- You can specify a different override file:
```bash
docker-compose -f docker-compose.yml -f docker-compose.prod.yml up -d
```

## 7. Best Practices for Docker Compose

- Use **health checks** to wait for services to be ready and healthy.
```yaml
  database:
    healthcheck:
      test: ["CMD", "pg_isready", "-U", "user"]
      interval: 10s
      retries: 5
```

- Use **named volumes** instead of bind mounts in production.
- **Separate environment variables** into `.env` files instead of hardcoding:
- Use **`docker-compose.override.yml`** to customize different environments without modifying the main file.
- **Keep Compose files readable & modular** by using external YAML files for complex configurations.

---

# 💠 **Environment Variables**

Environment variables in Docker provide a way to **configure applications dynamically** without modifying the container image. They allow applications to adapt to different environments (e.g., development, staging, production) while keeping sensitive information (like API keys and credentials) **out of the image and source code**.

## 1. Passing Variables at Runtime

You can pass environment variables directly when running a container:
```bash
docker run -e APP_ENV=production -e DEBUG=false myapp
```

## 2. Defining Environment Variables in `docker-compose.yml`

You can define default values inside the `docker-compose.yml`:
```yaml
services:
  app:
    image: myapp
    environment:
      APP_ENV: production
```

## 3. Using an `.env` File

For better management, store variables in an `.env` file:

Then, reference it in `docker-compose.yml`:
```yaml
services:
  app:
    image: myapp
    env_file:
      - .env # .env est l'option par défaut
```

> ⚠️ *`.env` should **never** be sent on a Git repository. Add it to `.gitignore` and create a template file `.env.sample` with empty values.*

## 4. Set project prefix

You can add a prefix to your project containers, volumes and networks by setting the environment variable `COMPOSE_PROJECT_NAME` :

```bash
COMPOSE_PROJECT_NAME=my-project
```

The containers would for example become `my-project-app`, `my-project-db`, etc.

---

# 💠 **Sensitive Environment Variables**

Storing sensitive data like **passwords, API keys, and credentials** in plain-text environment variables or `.env` files **poses security risks**. To handle sensitive information securely in Docker, consider these approaches:

## 1. Use Docker Secrets (For Swarm Mode)

Docker Secrets is a built-in feature for securely storing and managing sensitive data in **Docker Swarm**.
```bash
echo "my-secret-password" | docker secret create db_password -
```

Reference it in `docker-compose.yml` (Swarm mode only):
```yaml
services:
  database:
    image: postgres
    secrets:
      - db_password
secrets:
  db_password:
    external: true
```

Inside the container, the secret will be available as a **file** in `/run/secrets/db_password`, making it more secure than environment variables.

## 2. Use External Secret Management Tools

For **non-Swarm deployments**, use **external secret managers**:

- **HashiCorp Vault** – Securely store, access, and dynamically generate secrets.
- **AWS Secrets Manager** – Manage credentials securely in AWS-based environments.
- **Azure Key Vault** or **Google Secret Manager** – Similar managed solutions for cloud environments.

## 3. Avoid Exposing Sensitive Data

- **Never store secrets inside Docker images** (`Dockerfile`, `.env`, or `docker-compose.yml`).
- **Use runtime-only injection** (`docker run -e API_KEY=$API_KEY myapp`) instead of hardcoding.
- **Check environment variables inside a running container**:
    ```bash
    docker exec mycontainer printenv
    ```
- **Restrict access** to environment files (`chmod 600 .env`).

---

# 💠 Containers Repository ✍️

To be completed…

---

# 💠 Setup HTTPS ✍️

To be completed…

---

# 💠 **Orchestration**

For managing large-scale container deployments, **container orchestration** tools are used.

- **Docker Swarm** – Native clustering and orchestration tool for Docker.
- **Kubernetes (K8s)** – A more advanced orchestration tool, widely used for managing containerized applications in production.

### **Example of a Docker Swarm Cluster Setup**

```bash
docker swarm init
docker service create --name web -p 80:80 nginx
```

### **Example of a Kubernetes Setup (Using `kubectl`)**

```bash
kubectl create deployment web --image=nginx
kubectl expose deployment web --port=80 --type=LoadBalancer
```

> ⚠️ *Docker Swarm is simpler than Kubernetes but not recommanded for a production environment. Kubernetes offers advanced features like auto-scaling, rolling updates, self-healing capabilities, etc.*

---

# 💠 **Security Best Practices**

## 1. Use Trusted & Minimal Images

- Prefer **official images** with an alpine or slim version (`nginx:alpine` > `nginx:latest`).
- Regularly **update images** to patch vulnerabilities.
- Scan images with **Trivy**, **Grype**, or **Docker Scan**:
    ```bash
    trivy image myapp
    ```

## 2. Limit Privileges & Isolate Containers

- Avoid running as `root`, use a **non-root user** in the `Dockerfile`:
    ```docker
    RUN adduser --system appuser
    USER appuser
    ```
    
- Use `-read-only` and `-cap-drop` to **restrict permissions:**
    ```bash
    docker run --read-only --cap-drop=ALL myapp
    ```
    
> *💡`--read-only` runs the container in read-only mode, meaning no files can be modified inside the container*
    
> *💡`-cat-drop=ALL` drops all Linux capabilities, ensuring least privilege execution*

- Run **rootless Docker** for added security:
    ```bash
    dockerd --rootless
    ```

## 3. Restrict Networking & Limit Exposure

- Use **custom bridge networks** instead of `default`:
    ```bash
    docker network create secure_net
    docker run --network=secure_net myapp
    ```
    
- Avoid exposing unnecessary ports (`p` flag).
- Block outbound traffic if not required:
    ```bash
    docker network create --internal secure_net
    ```

## 4. Enforce Resource Limits

- Prevent resource exhaustion:
    ```bash
    docker run --memory=500m --cpus=1 myapp
    ```
    
- Use `-tmpfs` for temporary files:
    ```bash
    docker run --tmpfs /tmp myapp
    ```

## 5. Secure the Docker Daemon

- **Disable the daemon socket exposure** (`/var/run/docker.sock`):
    ```bash
    sudo chmod 600 /var/run/docker.sock
    ```
    
- Enable **TLS authentication** for secure API access.

## 6. Remove Unused Resources

- Regular cleanup prevents attack vectors:
    ```bash
    docker system prune -a
    docker volume prune
    ```

---
# 💠 Tips and Tricks

- Install [https://github.com/jesseduffield/lazydocker](https://github.com/jesseduffield/lazydocker) on Linux terminal to manage Docker containers