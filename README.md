# Docker Notes for DevOps Engineering

## **Table of Contents**

### **1. Introduction to Docker**  
- [1.1 What is Docker?](#what-is-docker)  
- [1.2 Installation](#installation)  
- [1.3 Docker Container and Images](#docker-container-and-images)  
- [1.4 Docker Hub](#docker-hub)  

### **2. Docker Command Line Interface (CLI)**  
- [2.1 Introduction to Docker CLI](#introduction-to-docker-cli)  
- [2.2 Docker Image CLI](#docker-image-cli)  
- [2.3 Docker Container CLI](#docker-container-cli)  

### **3. Docker Custom Images**  
- [3.1 Dockerfile](#dockerfile)  
- [3.2 Containerize a Node.js Application](#containerize-a-nodejs-application)  
- [3.3 Automatic Port Mapping](#automatic-port-mapping)  
- [3.4 Pushing to Docker Hub](#pushing-to-docker-hub)  

### **4. Docker Networking**  
- [4.1 Bridge Mode Networking](#bridge-mode-networking)  
- [4.2 Host Mode Networking](#host-mode-networking)  
- [4.3 Overlay Mode Networking](#overlay-mode-networking)  
- [4.4 IPvlan and MacVlan Networking](#ipvlan-and-macvlan-networking)  
- [4.5 None Mode Networking](#none-mode-networking)  

### **5. Docker Volumes**  
- [5.1 Attaching Host Volumes](#attaching-host-volumes)  
- [5.2 Custom Volumes](#custom-volumes)  

### **6. Docker Compose**  
- [6.1 Introduction to Docker Compose](#introduction-to-docker-compose)  
- [6.2 Defining Docker Compose Files](#defining-docker-compose-files)  

---

## Docker Notes for DevOps Engineering

---

### **1. Introduction to Docker**

#### [1.1 What is Docker?](#1.1)
- **Definition:** Docker is a platform for developing, shipping, and running applications inside lightweight, portable containers.
- **Key Benefits:**
  - Consistency across environments
  - Rapid application deployment
  - Resource efficiency compared to traditional VMs

#### [1.2 Installation](#1.2)
- **Steps to Install:**
  - [Windows](https://www.docker.com/products/docker-desktop/) : Use Docker Desktop (CLI + GUI)
  - Linux: Use package managers like `apt` or `yum`
  - MacOS: Docker Desktop or brew install docker
- **Check Installation:** Run `docker --version`.

    <details>	
     <summary><b>image Guide</b></summary><br>
  🚥🚥🚥🚥🚥🚥🚥🚥🚥🚥
      
  ![Screenshot (654)](https://github.com/user-attachments/assets/f2cc64a9-88b3-4f2e-9eed-7584155d59bc)
  ![Screenshot (656)](https://github.com/user-attachments/assets/a12a2241-42ca-45b4-bc4d-f2aa8d6cedb8)
  ![Screenshot (658)](https://github.com/user-attachments/assets/f87b7e8b-d953-4a88-b303-49d61f2b439e)
  ![Screenshot (657)](https://github.com/user-attachments/assets/8fcfd239-7cc9-4b69-a971-e0dff86d2122)
  🚥🚥🚥🚥🚥🚥🚥🚥🚥🚥
  </details>
  
  ### ========================>>> Its automaticly detect the WSL Linux 
  ![Screenshot (665)](https://github.com/user-attachments/assets/a16bdb3e-175c-45a9-babe-389cfd87adcf)

  
#### [1.3 Docker Container and Images](#1.3)
- **Image:** A lightweight, standalone, and executable software package.
- **Container:** An instance of an image running as an isolated process.
- **Commands:**
  ```bash
  docker pull <image-name>
  docker run <image-name>
  ```

![Screenshot (666)](https://github.com/user-attachments/assets/4e6482e7-38d7-42f4-b32f-7680d57042a5)

## 🧫 [Run Docker in WSL](https://github.com/akashdip2001/docker/blob/main/Docker%20in%20WSL-Kali.md)

#### [1.4 Docker Hub](#1.4)
- A cloud-based repository to store and share Docker images.
- **Usage:**
  - Find public images
  - Push custom images using `docker push`

---

### **2. Docker Command Line Interface (CLI)**

#### [2.1 Introduction to Docker CLI](#2.1)
- **Purpose:** Manage images, containers, and Docker resources using the terminal.
- **Basic Commands:**
  - `docker ps` – List running containers
  - `docker images` – List images

#### [2.2 Docker Image CLI](#2.2)
- **Key Commands:**
  - `docker pull <image>` – Download an image
  - `docker rmi <image>` – Remove an image

#### [2.3 Docker Container CLI](#2.3)
- **Key Commands:**
  - `docker run <image>` – Start a container
  - `docker stop <container>` – Stop a running container
  - `docker logs <container>` – View logs from a container

1. [x] [Running Ubuntu img in Containers](./Docker%20in%20WSL-Kali.md)
2. [x] [Multiple Containers](./Docker%20in%20WSL-Kali.md)
3. [ ] [Port Mapping](./Port%20Mapping.md)

---

### **3. Docker Custom Images**

#### [3.1 Dockerfile](#3.1)
- **Definition:** A text file containing instructions to build a Docker image.
- **Sample Dockerfile:**
  ```dockerfile
  FROM node:14
  COPY . /app
  WORKDIR /app
  RUN npm install
  CMD ["node", "app.js"]
  ```
- **Command to Build:**
  ```bash
  docker build -t <image-name> .
  ```

#### [3.2 Containerize a Node.js Application](#3.2)
- Steps to:
  - Create a `Dockerfile`
  - Use `docker build` and `docker run`

#### [3.3 Automatic Port Mapping](#3.3)
- Map ports using `-p` flag:
  ```bash
  docker run -p 3000:3000 <image>
  ```

#### [3.4 Pushing to Docker Hub](#3.4)
- Authenticate: `docker login`
- Push Image:
  ```bash
  docker tag <image> <username>/<repository>
  docker push <username>/<repository>
  ```

---

### **4. Docker Networking**

#### [4.1 Bridge Mode Networking](#4.1)
- Default mode. Containers share the host's networking but are isolated.
- **Command:**
  ```bash
  docker network inspect bridge
  ```

#### [4.2 Host Mode Networking](#4.2)
- Shares the host network namespace.
- Useful for performance-critical apps.

#### [4.3 Overlay Mode Networking](#4.3)
- Enables multi-host container communication.

#### [4.4 IPvlan and MacVlan](#4.4)
- Advanced networking modes for performance and integration.

#### [4.5 None Mode Networking](#4.5)
- Completely disables networking for the container.

---

### **5. Docker Volumes**

#### [5.1 Attaching Host Volumes](#5.1)
- Mount directories from the host into the container.
- **Command:**
  ```bash
  docker run -v /host/path:/container/path <image>
  ```

#### [5.2 Custom Volumes](#5.2)
- Named volumes for persistent storage:
  ```bash
  docker volume create myvolume
  ```

---

### **6. Docker Compose**

#### [6.1 Introduction to Docker Compose](#6.1)
- A tool to define and run multi-container Docker applications.

#### [6.2 Defining Docker Compose Files](#6.2)
- **Sample `docker-compose.yml`:**
  ```yaml
  version: '3'
  services:
    app:
      image: node:14
      ports:
        - "3000:3000"
  ```

- Commands:
  ```bash
  docker-compose up
  docker-compose down
  ```

---

### **Tables for Quick Reference**

| **Command**                | **Description**                              |
|----------------------------|----------------------------------------------|
| `docker pull <image>`      | Download an image                           |
| `docker run <image>`       | Create and start a container                |
| `docker ps`                | List running containers                     |
| `docker stop <container>`  | Stop a running container                    |
| `docker volume create`     | Create a named volume                       |

| **Networking Mode**        | **Description**                              |
|----------------------------|----------------------------------------------|
| Bridge                     | Default mode, isolated container networking |
| Host                       | Shares host's network namespace             |
| Overlay                    | For multi-host communication                |

