# 📦 Docker Notes

---

## 1. Introduction to Docker

Docker is an open-source platform that automates the deployment, scaling, and management of applications using containerization. It allows developers to package applications along with dependencies into containers, ensuring consistency across environments.

---

## 2. Key Features of Docker

- **Lightweight** – Uses host OS kernel, unlike virtual machines.
- **Portability** – Runs the same across different environments.
- **Isolation** – Each container runs independently.
- **Scalability** – Easily scalable using orchestration tools (Docker Swarm, Kubernetes).
- **Faster Deployment** – Containers start in seconds.

---

## 3. Docker vs Virtual Machines

| Feature        | Docker Containers            | Virtual Machines             |
|----------------|------------------------------|------------------------------|
| Performance    | Faster, lightweight           | Slower, consumes more resources |
| Boot Time      | Seconds                       | Minutes                      |
| OS Support     | Shares host OS kernel         | Each VM has a separate OS    |
| Isolation      | Process-level isolation       | Full OS isolation            |
| Storage        | Uses layered storage (UnionFS)| Uses virtual disks           |

---

## 4. Docker Architecture

- **Docker Client**: CLI/GUI to interact with Docker Daemon
- **Docker Daemon**: Manages Docker containers and images
- **Docker Images**: Read-only templates used to create containers
- **Docker Containers**: Running instances of Docker images
- **Docker Registry**: Stores Docker images (e.g., Docker Hub, AWS ECR, GCR)
- **Docker Compose**: Tool for defining multi-container apps (`docker-compose.yml`)

---

## 5. Basic Docker Commands

```bash
apt update -y                          # Update system
apt install docker.io -y              # Install Docker

docker --version                      # Check Docker version
docker pull IMAGE_NAME:latest         # Download image from Docker Hub
docker images                         # List all downloaded images
docker image ls                       # List all images (alternative)
```

---

## 6. Building and Running Docker Images

### Build Image from Dockerfile
```bash
docker build -t <IMAGE_NAME> <PATH_TO_DOCKERFILE>
# Example:
docker build -t user_image .
```

### Run a Container
```bash
docker run -dit -p 80:80 IMAGE_NAME
# Options:
# -d: Detached mode
# -i: Interactive
# -t: Terminal
```

---

## 7. Managing Containers and Images

```bash
docker ps                             # List running containers
docker ps -a                          # List all containers
docker exec -it CONTAINER /bin/bash  # Access a running container
docker container start CONTAINER     # Start stopped container
docker stop CONTAINER                # Graceful stop
docker kill CONTAINER                # Force stop
docker rm CONTAINER                  # Remove container
docker rmi IMAGE_ID                  # Remove image
```

---

## 8. Create Custom Docker Image with Commit

```bash
docker commit CONTAINER_ID USERNAME/IMAGE_NAME
```

---

## 9. COPY vs ADD in Dockerfile

| COPY | ADD |
|------|-----|
| Static files from host to container | Adds from local or URL sources |

---

## 10. Dockerfile Example

```dockerfile
FROM ubuntu
RUN apt update -y
RUN apt install apache2 -y
RUN apt install git -y
RUN apt install nano -y
COPY ./index.html /var/www/html
ADD https://get.jenkins.io/war-stable/2.375.3/jenkins.war /var/www/html
USER ubuntu
```

---

## 11. RUN vs CMD in Dockerfile

- **RUN**: Executes during image build. Used for installing packages.
- **CMD**: Executes at container startup. Used for default commands.

```dockerfile
# RUN example
RUN apt update && apt install -y apache2

# CMD example
CMD ["echo", "Hello from the container!"]
```

---

## 12. CMD vs ENTRYPOINT

| Property      | CMD                     | ENTRYPOINT           |
|---------------|--------------------------|-----------------------|
| Overridable   | Yes                      | No (unless manually)  |
| Usage         | Default command          | Always runs as base   |

```dockerfile
# CMD
CMD ["echo", "Hello!"]

# ENTRYPOINT
ENTRYPOINT ["ping"]
CMD ["localhost"]
```

---

## 13. ENV in Dockerfile (Environment Variables)

```dockerfile
ENV MY_NAME="DockerUser"
CMD ["bash", "-c", "echo Hello, $MY_NAME"]
```

```bash
# Override at runtime
docker run -e MY_NAME="CustomUser" env-demo
```

---

## 14. Troubleshooting

```bash
docker container logs CONTAINER_ID  # View container logs
```

---

## 15. Summary of Key Docker Commands

| Action                     | Command Example                          |
|---------------------------|-------------------------------------------|
| Build Image               | `docker build -t myapp .`                |
| Run Container             | `docker run -d -p 80:80 myapp`           |
| Access Container          | `docker exec -it container_id /bin/bash`|
| List Running Containers   | `docker ps`                              |
| Remove Container          | `docker rm container_id`                 |
| Remove Image              | `docker rmi image_id`                    |

---

## 16. Configuration Management (Overview)

**Definition**: Automates infrastructure setup and ensures consistency.

### ✅ Benefits:
- Saves Time
- Reduces Errors
- Ensures Consistency
- Fast Recovery
- Scalable

### ⚙️ Popular Tools:
- **Ansible** – Simple, YAML, agentless
- **Puppet** – Advanced, large enterprises
- **Chef** – Uses Ruby
- **Terraform** – Cloud infrastructure as code

### Ansible Example:

```yaml
- name: Install Apache on All Servers
  hosts: all
  become: yes
  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present
```

---

## ✅ Docker Assignment
*(Add your Docker assignment here if needed)*
