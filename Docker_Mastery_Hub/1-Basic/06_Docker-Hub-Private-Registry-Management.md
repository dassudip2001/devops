# 6. Docker Hub and Private Registry Management

## 6.1. Introduction to Docker Hub

[Docker Hub](https://hub.docker.com/) is a cloud-based registry service provided by Docker for sharing and managing Docker images. It serves as a central repository for storing and distributing Docker images.

## 6.2. Pushing and pulling Docker images from Docker Hub

### 6.2.1. `docker login`

- Log in to Docker Hub using the `docker login` command:

```bash
docker login
```

- Enter your dockerHub username and Password.

### 6.2.2. Pushing Image to DockerHub

1. Tag your local image with your Docker Hub username and repository name:

```bash
docker tag my-node-app your-username/my-node-app
```

2. Push the image to Docker Hub:

```bash
docker push your-username/my-node-app
```

### 6.2.3. Pulling docker images for DockerHub

- To pull an image from a registry, use the `docker pull` command:

```bash
docker pull your-registry/your-image
```

## 6.3. Creating Private Docker Registry and their setup

#### <--- In progress --->

---
