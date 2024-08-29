# 3. Docker Compose

## 3.1 Introduction to Docker Compose

**Docker Compose** is a tool for managing multi-container Docker applications. It uses a YAML file to define and run services, networks, and volumes, simplifying the setup and orchestration of complex application environments.

### 3.1.1. Benefits:

- Easy to start and stop all the containers with a single command.
- Automated Container Lifecycle Management
- Environment Reproducibility
- Docker Compose makes sure everything stays the same across all your setups, so working with your team is a breeze.
- Plus, it's perfect for quickly getting your apps up and running on your own computer, so you can get back to coding in no time

### 3.1.1. Installation and Setup

**1\. Windows:**

- Download the Docker Desktop installer from the Docker website.
- Run the installer and follow the on-screen instructions to install Docker Desktop, which includes Docker Compose.

**2\. macOS:**

- Install Docker Desktop for Mac from the Docker website.
- Once installed, Docker Compose will be available as part of Docker Desktop.

**3\. Linux:**

- Docker Compose can be installed Debian based Ubuntu, Run the following command.

```bash
sudo apt install docker-compose
```

- Alternatively, you can install Docker Compose using the official Docker repository.

#### **Configuration and Setup:**

- After installing Docker Compose, it should automatically work with Docker Engine.
- To verify the installation, open a terminal or command prompt and run `docker-compose --version`. You should see the

## 3.2. Docker Compose File Basics

#### **1\. Syntax and Structure:**

- Docker Compose files use YAML syntax (.yml or .yaml extension).
- They define services, networks, volumes, and other configurations for your Dockerized application.

#### **2\. Key Components:**

- **Services**: Defines the containers that make up your application, along with their configurations (e.g., image, ports, environment variables).
- **Networks**: Specifies custom network configurations for your services, allowing containers to communicate with each other.
- **Volumes**: Defines shared data volumes between containers or with the host machine, ensuring data persistence.
- **Environment Variables**: Allows you to set environment variables for services, influencing their behavior at runtime.

#### **3\. Basic Commands:**

- **Building Services**: Use `docker-compose build` to build the images defined in your Docker Compose file.
- **Starting Services**: Execute `docker-compose up` to start the services defined in your Compose file. Use `-d` flag for detached mode.
- **Stopping Services**: Run `docker-compose down` to stop and remove the containers created by `docker-compose up`.

## 3.3 Docker Compose Directives

There are many directives, here are few common ones:

1.  **version**: Specifies the version of the Docker Compose file format being used.
2.  **services**: Defines the containers that make up the application, along with their configurations.
3.  **networks**: Specifies custom network configurations for the services, allowing containers to communicate with each other.
4.  **volumes**: Defines shared data volumes between containers or with the host machine, ensuring data persistence.

5.  **environment**: Sets environment variables for services.
6.  **secrets**: Specifies secrets to be used by services, which are stored securely.
7.  **build**: Configures the build settings for building custom Docker images.

8.  **ports**: Maps container ports to host ports for accessing services from the host machine.

9.  **depends_on**: Specifies dependencies between services, ensuring that one service starts only after another has started.

10. **extends**: Allows extending and overriding configurations from another service or file.

11. **external_links**: Links containers from another service or project to the current service.

## 3.4 Managing multi-container applications with Docker Compose

Managing multi-container applications with Docker Compose is a powerful way to streamline the development, deployment, and scaling of complex applications. Docker Compose allows you to define and run multi-container Docker applications using a single YAML file, making it easy to orchestrate and manage your entire application stack.

Here's how you can manage multi-container applications with Docker Compose:

### 1\. Define Your Services:

Start by defining the services that make up your application in a `docker-compose.yml` file. Each service represents a containerized component of your application. Specify the Docker image, ports, volumes, environment variables, and any other configuration options needed for each service.

```yaml
version: "3"
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html
  app:
    image: myapp:latest
    ports:
      - "5000:5000"
    environment:
      - DEBUG=True
    depends_on:
      - db
  db:
    image: postgres:latest
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
```

### 2\. Start Your Application:

Use the `docker-compose up` command to start your multi-container application. Docker Compose will read the `docker-compose.yml` file, pull the necessary Docker images (if they don't exist locally), and start the containers for each service.

```bash
docker-compose up
```

- Running in background

```bash
docker-compose up -d
```

### 3\. Manage Your Application:

Docker Compose provides various commands for managing your multi-container application:

- `docker-compose up`: Start the application and all associated containers.
- `docker-compose down`: Stop the application and remove all associated containers, networks, and volumes.
- `docker-compose ps`: Check the status of running services.
- `docker-compose logs`: View the logs of all services.
- `docker-compose exec <service> <command>`: Run a command inside a running container.

### 4\. Update and Scale Your Application:

As your application evolves, you can update the configuration in the `docker-compose.yml` file and use the `docker-compose up --build` command to rebuild and restart your application with the new changes. Additionally, you can scale individual services using the `--scale` option:

```bash
docker-compose up --scale app=3
```

This command scales the `app` service to three replicas.

---
