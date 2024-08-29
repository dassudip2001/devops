# 1. Introduction to Docker

## 1.1. What & Why of virtualization & containerization?

### What is Virtual Machine (VM).?

**Virtual Machine (VM)** is like a computer within a computer. It's a software-based emulation of a physical computer that runs an operating system and applications as if they were on a physical machine. This allows you to run multiple operating systems on a single physical machine, making it a versatile tool for testing, development, and running applications in isolated environments. It's like having a **computerception**!

### What is virtualization.?

- virtualization refers to the process of creating a virtual instance of a physical machine.

### What is containerization?

**Containerization** is just a method of packing the application and is dependencies inside an isolated closed environment called container.

### Why do we need containerization?

- **Traditionally**, software applications were deployed using a **monolithic** approach where each application ran on a dedicated server or virtual machine (VM), which often resulted in wastage of resources due to underutilization.

- So, With Containerization, multiple containers to run on a single host without extra resources, thereby improving resource utilization and efficiency.

## 1.2. What is Docker.?

Docker is a containerization tool.

### Benefits of using Docker

Docker offers several advantages for software development and deployment:

- **Isolation:** Containers encapsulate applications and dependencies, preventing conflicts.
- **Portability:** Consistent environments across development, testing, and production.
- **Scalability:** Easily scale applications by running multiple containers.

### Docker Container Vs. Docker Image

- **Container**: It is the running instance of the image, containers are made with image, that actually takes resources.
- **Image**: Its static, they are the ones that are shared so anyone can run them and make containers from them. They are immutable.

## 1.3 Docker Architecture: Docker Engine, Docker Client, Docker Registry

- **Docker Engine**: Central component managing containers, consists of three main parts:

  - **Docker Daemon**: runs on host, manages containers.
  - **Docker REST API**: Docker provides a REST API that allows interaction with the Docker daemon.
  - **Docker CLI**: command-line tool for user interaction.

- **Docker Client**: Interface enabling users to interact with Docker Engine, issuing commands through the Docker CLI.

- **Docker Registry**: Repository storing Docker images, facilitating sharing and distribution. Docker Hub is a popular example, but private registries can also be set up for organizational use.

## 1.4. Docker Workflow

- Developers write Dockerfiles to define containerized applications.
- Docker Engine builds images from Dockerfiles.
- Docker Hub serves as a repository for sharing and pulling Docker images.
- Docker Compose orchestrates the deployment of multi-container applications.

#### Core Concepts:

- **Containers:** Lightweight, standalone, and executable packages that include everything needed to run a piece of software, including the code, runtime, libraries, and system tools.

- **Images:** A snapshot or a template of a container. It's a lightweight, stand-alone, and executable package that includes everything needed to run a piece of software, including the code, runtime, libraries, and system tools.

- **Dockerfile:** A script that contains instructions for building a Docker image. It defines the base image to use, any additional components or customization, and the commands needed to run the application.

← Previous || [Index](../README.md) || Next→
