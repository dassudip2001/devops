# 2. Installing Docker

In this section, we will guide you through the process of installing Docker.

To get started with Docker, follow these steps:

1. Visit the [official Docker website](https://www.docker.com/) and download the appropriate version for your operating system.
2. Install Docker following the provided instructions.
3. Verify the installation using the `docker --version` command.

## 2.1 Installing Docker

Docker can be installed on various operating systems, including Linux, macOS, and Windows. Here's a brief overview of the installation process for each:

1.  **Linux**:

    - On most Linux distributions, you can install Docker using the package manager. For example, on Ubuntu, you would use the following commands:

      ```bash
      sudo apt-get update
      sudo apt-get install docker.io
      ```

    - Verify Docker

      ```bash
      docker --version
      ```

    - After installationg, it creates a **docker** group.
    - Add your USER to this group, to avoid using `sudo` everytime.

      ```bash
      sudo usermod -aG docker <your user name>
      ```
      or

      - Giving permission to the user for Docker daemon socket: `sudo chown $USER /var/run/docker.sock`


    - Now you need to start the Docker service and enable it to start on boot:

      ```bash
      sudo systemctl start docker
      sudo systemctl enable docker
      ```

2.  **macOS**:

    - Docker Desktop provides an easy-to-use installer for macOS. You can download it from the official Docker website and follow the installation instructions provided.
    - Once installed, Docker Desktop will be available in your Applications folder. Launch it and follow any additional setup steps.

3.  **Windows**:

    - Docker Desktop is also available for Windows. You can download the installer from the Docker website and run it.
    - During installation, Docker Desktop may require enabling Hyper-V and other features. Follow the on-screen instructions to complete the setup.

### Configuration of Docker

After installing Docker, you may need to configure it based on your requirements. Some common configuration tasks include:

1.  **Network Configuration**: Docker provides default network configurations, but you may need to customize them for your environment. You can configure Docker networking using command-line tools or Docker Desktop's graphical interface.
2.  **Resource Allocation**: Docker allows you to control resource allocation for containers, such as CPU and memory limits. You can configure these settings globally or on a per-container basis.
3.  **Registry Authentication**: If you plan to pull Docker images from private registries, you may need to configure Docker to authenticate with those registries. This typically involves providing credentials or authentication tokens.

---
