# Docker Notes for DevOps Engineering

Table of Contents

1. Introduction to Docker
1.1 What is Docker?
1.2 Installation
1.3 Docker Container and Images
1.4 Docker Hub


2. Docker Command Line Interface (CLI)
2.1 Introduction to Docker CLI
2.2 Docker Image CLI
2.3 Docker Container CLI


3. Docker Custom Images
3.1 Dockerfile
3.2 Containerize a Node.js Application
3.3 Automatic Port Mapping
3.4 Pushing to Docker Hub


4. Docker Networking
4.1 Bridge Mode Networking
4.2 Host Mode Networking
4.3 Overlay Mode Networking
4.4 IPvlan and MacVlan Networking
4.5 None Mode Networking


5. Docker Volumes
5.1 Attaching Host Volumes
5.2 Custom Volumes


6. Docker Compose
6.1 Introduction to Docker Compose
6.2 Defining Docker Compose Files



Docker Notes for DevOps Engineering


---

1. Introduction to Docker

1.1 What is Docker?

Definition: Docker is a platform for developing, shipping, and running applications inside lightweight, portable containers.

Key Benefits:

Consistency across environments

Rapid application deployment

Resource efficiency compared to traditional VMs



1.2 Installation

Steps to Install:

Windows: Use Docker Desktop

Linux: Use package managers like apt or yum

MacOS: Docker Desktop or brew install docker


Check Installation: Run docker --version.


1.3 Docker Container and Images

Image: A lightweight, standalone, and executable software package.

Container: An instance of an image running as an isolated process.

Commands:

docker pull <image-name>
docker run <image-name>


1.4 Docker Hub

A cloud-based repository to store and share Docker images.

Usage:

Find public images

Push custom images using docker push




---

2. Docker Command Line Interface (CLI)

2.1 Introduction to Docker CLI

Purpose: Manage images, containers, and Docker resources using the terminal.

Basic Commands:

docker ps – List running containers

docker images – List images



2.2 Docker Image CLI

Key Commands:

docker pull <image> – Download an image

docker rmi <image> – Remove an image



2.3 Docker Container CLI

Key Commands:

docker run <image> – Start a container

docker stop <container> – Stop a running container

docker logs <container> – View logs from a container




---

3. Docker Custom Images

3.1 Dockerfile

Definition: A text file containing instructions to build a Docker image.

Sample Dockerfile:

FROM node:14
COPY . /app
WORKDIR /app
RUN npm install
CMD ["node", "app.js"]

Command to Build:

docker build -t <image-name> .


3.2 Containerize a Node.js Application

Steps to:

Create a Dockerfile

Use docker build and docker run



3.3 Automatic Port Mapping

Map ports using -p flag:

docker run -p 3000:3000 <image>


3.4 Pushing to Docker Hub

Authenticate: docker login

Push Image:

docker tag <image> <username>/<repository>
docker push <username>/<repository>



---

4. Docker Networking

4.1 Bridge Mode Networking

Default mode. Containers share the host's networking but are isolated.

Command:

docker network inspect bridge


4.2 Host Mode Networking

Shares the host network namespace.

Useful for performance-critical apps.


4.3 Overlay Mode Networking

Enables multi-host container communication.


4.4 IPvlan and MacVlan

Advanced networking modes for performance and integration.


4.5 None Mode Networking

Completely disables networking for the container.



---

5. Docker Volumes

5.1 Attaching Host Volumes

Mount directories from the host into the container.

Command:

docker run -v /host/path:/container/path <image>


5.2 Custom Volumes

Named volumes for persistent storage:

docker volume create myvolume



---

6. Docker Compose

6.1 Introduction to Docker Compose

A tool to define and run multi-container Docker applications.


6.2 Defining Docker Compose Files

Sample docker-compose.yml:

version: '3'
services:
  app:
    image: node:14
    ports:
      - "3000:3000"

Commands:

docker-compose up
docker-compose down



---
