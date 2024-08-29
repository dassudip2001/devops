# 2. Docker Networking - I

## 2.1. Introduction to Docker Networking

Docker networking enables communication between containers, as well as between containers and the host system or external networks.

### **Importance of Docker Networking:**

1.  **Isolation**: Ensures communication between containers without compromising isolation.
2.  **Microservices**: Facilitates communication in microservices architecture.
3.  **Scalability**: Simplifies scaling by dynamically discovering services.
4.  **Security**: Helps control traffic flow and implement access controls.

## 2.2. Default Networking in Docker

- Docker provides **three default networking modes**: **bridge**, **host**, and **none**.
- These modes offer different ways for containers to communicate with each other and with the host system.

### **Bridge Networking Mode:**

- Creates a virtual bridge network for containers.
- Enables communication within the same network.
- Allows access to host and external networks via NAT.
- **Pros:** Isolation, built-in port forwarding.
- **Cons:** Limited direct communication between different bridge networks.

### **Host Networking Mode:**

- Bypasses Docker's virtual network, using host's network stack.
- Offers high performance with minimal overhead.
- **Pros:** High performance, direct port accessibility.
- **Cons:** Reduced isolation, potential port conflicts.

### **None Networking Mode:**

- Disables networking for containers.
- Provides maximum isolation.
- **Pros:** Maximum isolation, useful for specialized configurations.
- **Cons:** No communication without additional configurations, limited usability.

## 2.3 Docker Bridge Networking

### 2.3.1. Container-to-Container Communication

- In Docker bridge networking, containers within the same bridge network can communicate with each other using their container names or IP addresses.

- Docker assigns a **unique IP address** to each container within the bridge network, facilitating direct communication without the need for port mapping.

### 2.3.2. Configuring and Managing Bridge Networks

Docker provides commands and tools for configuring and managing bridge networks to suit specific application requirements.

#### **Creating a Bridge Network:**

```bash
docker network create my_bridge_network
```

#### **Attaching Containers to Bridge Networks:**

```bash
docker run --name container1 --network my_bridge_network -d ubuntu
docker run --name container2 --network my_bridge_network -d ubuntu
```

#### **Inspecting Bridge Networks:**

```bash
docker network inspect my_bridge_network
```

#### **Removing Bridge Networks:**

```bash
docker network rm my_bridge_network
```

### 2.3.3. Customizing Bridge Network Configuration

Docker allows customization of bridge network configurations to accommodate different networking needs and optimize performance.

#### **Configuring Subnet and Gateway:**

```bash
docker network create --subnet=172.18.0.0/16 --gateway=172.18.0.1 my_custom_network
```

#### **Setting Bridge Network Driver Options:**

```bash
docker network create --driver=bridge --opt com.docker.network.bridge.enable_icc=false my_custom_network
```

#### **Using Docker Compose for Network Configuration:**

```yaml
version: "3"
services:
  service1:
    image: nginx
    networks:
      - my_network

networks:
  my_network:
    driver: bridge
```

## 2.4. Exposing Ports and Port Mapping

- Exposing ports and port mapping in Docker allows containers to make their services accessible to other containers or external systems.

- It allows communication between containers and the host system, as well as facilitating access to containerized services from external networks.

### 2.4.1. Port Exposure in Docker Containers

By default, Docker containers run in isolated environments, and their ports are not accessible from outside the container. To make container services accessible, ports must be explicitly exposed.

#### **Exposing Ports in Dockerfile:**

```Dockerfile
# Expose port 80 for HTTP traffic
EXPOSE 80
```

#### **Exposing Ports in Docker Run Command:**

```bash
docker run -d -p 8080:80 my_container_image
```

### 2.4.2. Port Mapping

Port mapping allows Docker containers to bind container ports to host ports, making container services accessible from the host system or external networks.

**Syntax:**

```bash
docker run -d -p <host_port>:<container_port> my_container_image
```

### 2.4.3. Managing Exposed Ports

Docker provides commands and tools for managing exposed ports and port mapping configurations.

#### **Listing Exposed Ports:**

```bash
docker port my_container
```

#### **Inspecting Container Port Configuration:**

```bash
docker inspect --format='{{range $p, $conf := .NetworkSettings.Ports}}{{$p}} -> {{(index $conf 0).HostPort}}{{end}}' my_container
```

### 2.4.4. Using Docker Compose for Port Mapping

Docker Compose simplifies port mapping configurations for multi-container applications by allowing specification of port mappings in the `docker-compose.yml` file.

**Example:**

```yaml
version: "3"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
```

---
