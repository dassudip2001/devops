# 3. Writing and Building Docker Images with Dockerfiles

## 3.1 What & Why is a Dockerfile?

### What is a Dockerfile?

- A Dockerfile is a text file; which has many commands or instructions.
- These instructions are executed from top to bottom, creating a new image.

### Why or Purpose of Dockerfiles.?

- The purpose of Dockerfiles is to automate the process of creating Docker images in a consistent manner.

### How is Docker image build with Dockerfile?

- Docker builds images by starting with a **base image**, which serves as the foundation.
- Each instruction results in a new layer being added to the image.
- After all the layes are added base image, resulting in a new image.

## 3.2. Explanation of key directives such as `FROM`, `RUN`, `COPY`, `ADD`, `CMD`, `ENTRYPOINT`, `ENV` and `WORKDIR`.

**Key directives used in Dockerfiles:**

1.  **`FROM`**:

    - Specifies the **base image** for the Docker image being built.
    - It defines the starting point for the image build process. Example:

      ```dockerfile
      FROM ubuntu:latest
      ```

2.  **`RUN`**:

    - Executes commands within the container during the image build process.
    - It is used to install dependencies, configure settings, and perform other tasks. Example:

      ```dockerfile
      RUN apt-get update && apt-get install -y <package_name>
      ```

3.  **`COPY`**:

    - Copies files from the host machine into the container's filesystem.
    - It is often used to add application code or configuration files to the image. Example:

      ```dockerfile
      COPY ./app /app
      ```

4.  **`ADD`**:

    - **Similar to COPY**, but with additional features such as extracting archives and downloading files from URLs.
    - It's versatile but COPY is preferred for simple file copying. Example:

      ```dockerfile
      ADD ./archive.tar.gz /path/to/destination
      ```

5.  **`CMD`**:

    - Provides default arguments for the entrypoint command or specifies a different command to run when the container starts.
    - It can be **overridden** at runtime. Example:

      ```dockerfile
      CMD ["node", "server.js"]
      ```

6.  **`ENTRYPOINT` (optional)**:

    - **Similar as CMD**, Specifies the main command to be executed when the container starts.
    - It can also accept arguments passed at runtime. Example:

      ```dockerfile
      ENTRYPOINT ["node"]

      CMD ["server.js"]
      ```

    - **Why use `ENTRYPOINT`?**
      - Let's say during runtime i changed some setting and now for starting the app the main file is **`script.js`**, i can pass it as an argument,
      - While using **`CMD`** i have to pass node **`script.js`**, or
      - with **`ENTRYPOINT`** & **`CMD`** i just need to pass **`script.js`**, because node is already set as defaul entrypoint.

7.  **`WORKDIR`**:

    - Sets the working directory, means that all commands executed in the Dockerfile after the `WORKDIR` instruction will be relative to this directory unless explicitly specified otherwise.
    - It is used to ensure consistency in file paths and directory structures. Example:

    ```dockerfile
    WORKDIR /path/to/working/directory
    ```

8.  **ENV (Environment)**:

    - The `ENV` instruction is used to set environment variables in the Docker image.
    - It takes precedence over any environment variables **with the same name that are set inside the application code**, thus **overwriting the environment** variables inside the application code.

    ```dockerfile
    # Set environment variables
    ENV NODE_ENV=production \
        PORT=8080 \
        DB_HOST=localhost \
        DB_USER=admin
    ```

## 3.3. Basic syntax and structure of Dockerfiles

```dockerfile
FROM node:14

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy application files
COPY . .

# Expose port
EXPOSE 3000

# Define default command to start the application
CMD ["npm", "start"]
```

## 3.4. Building Docker images using Dockerfiles

### Docker Build Command:

#### Syntax:

```dockerfile
docker build [OPTIONS] PATH | URL | -
```

#### Build Process:

- Docker reads the Dockerfile line by line and executes each instruction in order.
- Each instruction creates a new layer in the image, allowing for efficient caching and reusability.
- The build context(location of Dockerfile) (specified by PATH, URL, or `-`) is sent to the Docker daemon, which includes all files needed for the build process.
- Docker caches intermediate build stages, allowing subsequent builds to be faster if the Dockerfile and build context haven't changed.

#### Example:

```dockerfile
docker build -t my-image:latest .
```

This command builds an image named `my-image` with the tag `latest` using the Dockerfile located in the current directory (`.`).

- For example, you can use a GitHub repository URL as the build context in the `docker build` command:

  ```dockerfile
  docker build -t my-image:latest https://github.com/username/repository.git
  ```

### Docker Build Options

| Option        | Description                                                                              |
| ------------- | ---------------------------------------------------------------------------------------- |
| `-t, --tag`   | Tags the built image with a name and optional tag(s).                                    |
| `--file, -f`  | Specifies the path to the Dockerfile to use for building the image.                      |
| `--build-arg` | Sets build-time variables that can be used in the Dockerfile with the `ARG` instruction. |
| `--no-cache`  | Forces Docker to build the image without using the cache.                                |
| `--pull`      | Forces Docker to pull the latest version of the base image before building.              |
| `--squash`    | Squashes all image layers into a single layer, reducing the final image size.            |
| `--network`   | Sets the networking mode for the build process.                                          |
| `--progress`  | Sets the type of progress output during the build.                                       |

## 3.5. Managing Docker Images

| Category                   | Command                                            | Description                                                                                                  |
| -------------------------- | -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **Pulling Images**         | `docker pull IMAGE[:TAG]`                          | Downloads a Docker image from a registry. If the tag is omitted, it defaults to `latest`.                    |
| **Listing Images**         | `docker images [OPTIONS] [REPOSITORY[:TAG]]`       | Lists locally available Docker images. Options include `-a, --all` to show all images.                       |
| **Building Images**        | `docker build [OPTIONS] PATH`                      | URL                                                                                                          |
| **Tagging Images**         | `docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]` | Assigns a new tag to an existing image.                                                                      |
| **Pushing Images**         | `docker push IMAGE[:TAG]`                          | Pushes a Docker image or a repository to a registry.                                                         |
| **Removing Images**        | `docker rmi IMAGE[:TAG]`                           | Removes one or more Docker images. Options include `docker image prune [OPTIONS]` to remove dangling images. |
| **Inspecting Images**      | `docker inspect IMAGE[:TAG]`                       | Displays detailed information about a Docker image, including its layers, labels, and configuration.         |
| **Cleaning Up Disk Space** | `docker system prune [OPTIONS]`                    | Removes all unused data, including stopped containers, dangling images, and cache.                           |
| **Exporting Images**       | `docker save IMAGE[:TAG] > image.tar`              | Saves a Docker image to a tar archive file.                                                                  |
| **Importing Images**       | `docker load < image.tar`                          | Loads a Docker image from a tar archive file.                                                                |
| **History of an Image**    | `docker history IMAGE[:TAG]`                       | Displays the history of an image, showing how it was built layer by layer.                                   |

## 3.6. Few more directives: `ARG`, `EXPOSE`, `VOLUME`, `EXPOSE`, `LABEL`, `ONBUILD`, `HEALTHCHECK`, `SHELL`, `USER`

1.  **ARG (Argument)**:

    - `ARG` is used to define variables that can be passed to the Dockerfile **at build time** using the `--build-arg` flag.
    - These arguments can be used to customize the build process, such as specifying version numbers or default settings.

    - Example:

    ```dockerfile
    # Define an argument with a default value
    ARG VERSION=1.0

    # Use the argument in a RUN instruction
    RUN echo "Building version $VERSION"
    ```

    - When building the Docker image, you can override the default value of the `VERSION` argument by passing it as a build argument using the `--build-arg` flag.
    - For example, `docker build --build-arg VERSION=2.0 -t myimage .` will use `2.0` as the value for `VERSION` instead of the default `1.0`.

2.  **USER**:

    - The `USER` directive sets the user or UID that the container process runs as when the container starts.

    - Example:

    ```dockerfile
    USER appuser
    ```

    - During the build, commands run as "appuser", ensuring file operations use "appuser" permissions.
    - At runtime, the container process runs as "appuser", so it will have only that permission that the "appuser" has, thuse enhance security.

3.  **VOLUME**:

    - `VOLUME` is used to create a mount point within the container for storing persistent data.
    - It allows data to be shared between the host machine and the container or between multiple containers.

    ```dockerfile
    VOLUME /app/data
    ```

4.  **EXPOSE**:

    - `EXPOSE` is used to specify which ports should be exposed by the container at runtime.
    - It does not actually publish the port, but it serves as documentation for users of the image.

    ```dockerfile
    EXPOSE 8080
    ```

5.  **LABEL**:

    - `LABEL` used to add metadata to the Docker image in the form of key-value pairs.
    - It provides a way to document and annotate the image for users and administrators.

    ```dockerfile
    LABEL version="1.0" \
        description="This is a custom Docker image" \
        maintainer="John Doe <john@example.com>"
    ```

6.  **HEALTHCHECK**:

    - `HEALTHCHECK` is used to define a command to check the health of the container.
    - It allows Docker to monitor the container's health and take action based on the results.

    ```dockerfile
    HEALTHCHECK --interval=5s --timeout=3s CMD curl -f http://localhost/ || exit 1
    ```

    - It checks the health of the container by running a `curl` command every 5 seconds with a timeout of 3 seconds (means, if the command doesn't complete within 3 seconds, it will be considered a failure).
    - If the `curl` command fails to reach the specified URL, and exits with a non-zero status code the health check will fail, indicating that the container is unhealthy.

7.  **ONBUILD**:

    - The `ONBUILD` directive adds triggers to the image to execute commands when the image is used as the base for another image.
    - Say you have many teams ann they have different build's requirements, you create a base image of your WebApp so that any team can use your created base image, as there base image and build over that image to create there own build.
    - **`base-nodejs.Dockerfile`**

      ```dockerfile
      FROM node:14

      WORKDIR /app

      COPY package*.json ./

      RUN npm install

      # ONBUILD triggers
      ONBUILD RUN npm run build
      ONBUILD CMD ["npm", "start"]
      ```

    - The ONBUILD triggers in the base-nodejs image ensure that specific actions, such as running `npm run build` and setting `npm start` as the default command, are automatically performed when another image is built using this base image.

    - **`MyWebApp.Dockerfile`**

      ```dockerfile
      # Dockerfile for MyWebApp, based on the base-nodejs image
      FROM base-nodejs:latest

      # Copy application files
      COPY . .

      # Override the default CMD instruction (defined by ONBUILD)
      CMD ["node", "app.js"]
      ```

8.  **SHELL**:

    - The `SHELL` directive allows you to override the default shell used by Docker to execute commands in the Dockerfile.
    - It is used to specify a different shell interpreter, such as `bash`, `sh`, or `powershell`, depending on the platform and requirements of the Dockerfile.

      ```dockerfile
      SHELL ["/bin/bash", "-c"]
      ```

---
