# 3. Docker Images

## 1. **Understanding Docker Images and Containers**

### **Docker Images:**

- A Docker image is a lightweight package that includes everything needed to run a software, including the code and the depedencies.

- Images are the blueprints for containers. When you run an image, it becomes a container.

### **Docker Containers:**

- A container is a runtime instance of a Docker image.

- Containers are created from Docker images and run the software in a consistent environment.

## 2. **Docker Image Layers and How They Work**

### **Docker Image Layers:**

- Docker images are built in a series of layers. Each layer represents an instruction in the image’s Dockerfile.
- Layers are stacked on top of each other, and each layer is a delta (difference) of the file system.
- When you change a layer, Docker only needs to rebuild that layer and the layers above it.

### **How Layers Work:**

- The Union File System (UnionFS) allows files and directories of separate file systems (layers) to be transparently overlaid, forming a single coherent file system.
- Layers are read-only, and when a container is created from an image, Docker adds a read-write layer on top.

### 3. **Creating Custom Docker Images Using Dockerfile**

**Dockerfile Basics:**

- A Dockerfile is a text file that contains a series of instructions on how to build a Docker image.
- Each instruction in a Dockerfile creates a new layer in the image.

**Sample Dockerfile:**

```dockerfile
# Use an official Python runtime as a parent image
FROM python:3.8-slim-buster

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

### 4. **Best Practices for Writing Dockerfiles**

**Best Practices:**

- **Use Official Images**: Start with official base images to ensure stability and security.
- **Minimize the Number of Layers**: Combine multiple `RUN` statements into a single statement to reduce the number of layers.
- **Use `.dockerignore`**: Create a `.dockerignore` file to exclude files and directories that are not needed in the Docker image.
- **Leverage Build Cache**: Order your instructions from least to most frequently changing to take advantage of Docker’s build cache.
- **Run Containers as Non-Root Users**: Avoid running containers as root to enhance security.
- **Use Multi-Stage Builds**: This helps in creating smaller and more efficient images.

### 5. **Managing Images with Docker Hub and Private Registries**

**Docker Hub:**

- Docker Hub is a cloud-based repository where Docker users and partners create, test, store, and distribute container images.
- You can push and pull images to and from Docker Hub using Docker CLI commands.

**Commands:**

```bash
# Login to Docker Hub
docker login

# Tag an image
docker tag my-image myusername/my-image:tag

# Push an image to Docker Hub
docker push myusername/my-image:tag

# Pull an image from Docker Hub
docker pull myusername/my-image:tag
```

**Private Registries:**

- A private Docker registry is a server application that lets you store and manage your own Docker images privately.
- You can use Docker’s own `docker registry` or third-party services like JFrog Artifactory, Google Container Registry, or Azure Container Registry.

**Commands:**

```bash
# Run a private Docker registry
docker run -d -p 5000:5000 --name registry registry:2

# Tag an image for your private registry
docker tag my-image localhost:5000/my-image:tag

# Push an image to your private registry
docker push localhost:5000/my-image:tag

# Pull an image from your private registry
docker pull localhost:5000/my-image:tag
```

With these foundational concepts covered, you'll be well on your way to mastering Docker images. Feel free to ask if you need more detailed explanations or examples on any of these topics!
