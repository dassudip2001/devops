# 4. Running & Managing Docker Containers

## 4.1. Running Docker Containers from Images: `docker run`

### Docker Run Command:

#### Syntax:

```dockerfile
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

#### Description:

- The `docker run` command creates and starts a new container based on the specified image.
- If the image is not available locally, Docker automatically pulls it from the configured registry.
- By default, `docker run` attaches the container's standard input, output, and error streams to the terminal where it's invoked.
- You can customize the container's behavior and runtime configuration using various options.

#### Example:

```dockerfile
docker run -d --name my-container -p 8080:80 my-image:latest
```

**This command:**

- Runs a container in detached mode (`-d`).
- Names the container as `my-container` (`--name`).
- The container's port 80 is mapped to the host's port 8080 (`-p`). So, if you access `http://localhost:8080` in your web browser, the requests will be directed to port 80 of the container, where your application is running.
- Uses the image `my-image` with the tag `latest`.

#### Options:

| Category                  | Option               | Description                                           |
| ------------------------- | -------------------- | ----------------------------------------------------- |
| **Container Lifecycle**   | `-d, --detach`       | Run the container in detached mode (background).      |
|                           | `--name`             | Assign a name to the container.                       |
|                           | `--rm`               | Automatically remove the container when it exits.     |
| **Resource Constraints**  | `--cpu-shares`       | CPU shares (relative weight).                         |
|                           | `--memory`, `-m`     | Memory limit.                                         |
|                           | `--cpus`             | CPU count.                                            |
| **Networking**            | `-p, --publish`      | Publish a container's port(s) to the host.            |
|                           | `--network`          | Connect the container to a network.                   |
| **Volume Mounting**       | `-v, --volume`       | Bind mount a volume.                                  |
|                           | `--mount`            | Attach a filesystem mount to the container.           |
| **Environment Variables** | `-e, --env`          | Set environment variables.                            |
|                           | `--env-file`         | Read environment variables from a file.               |
| **Execution**             | `-it, --interactive` | Allocate a pseudo-TTY and keep STDIN open.            |
|                           | `--entrypoint`       | Override the entry point specified in the Dockerfile. |
| **Others**                | `--workdir`, `-w`    | Working directory inside the container.               |
|                           | `--restart`          | Restart policy for the container.                     |

## 4.2. Managing Docker Containers: `docker ps`, `docker rm`, `docker logs`, `docker exec`, `docker start/stop/restart`

| Category                                     | Command                                                                              | Description                                                          |
| -------------------------------------------- | ------------------------------------------------------------------------------------ | -------------------------------------------------------------------- |
| **Listing Containers**                       | `docker ps`                                                                          | Lists running containers.                                            |
|                                              | `docker ps -a`                                                                       | Lists all containers (including stopped ones).                       |
| **Starting and Stopping Containers**         | `docker start [CONTAINER_ID/NAME]`                                                   | Starts a stopped container.                                          |
|                                              | `docker stop [CONTAINER_ID/NAME]`                                                    | Stops a running container.                                           |
|                                              | `docker restart [CONTAINER_ID/NAME]`                                                 | Restarts a running container.                                        |
| **Removing Containers**                      | `docker rm [CONTAINER_ID/NAME]`                                                      | Removes one or more containers.                                      |
|                                              | `docker rm $(docker ps -a -q)`                                                       | Removes all stopped containers.                                      |
| **Viewing Container Logs**                   | `docker logs [CONTAINER_ID/NAME]`                                                    | Retrieves the logs of a container.                                   |
|                                              | `docker logs -f [CONTAINER_ID/NAME]`                                                 | Follows the logs in real-time.                                       |
| **Executing Commands in Containers**         | `docker exec [OPTIONS] CONTAINER_ID COMMAND [ARG...]`                                | Runs a command in a running container.                               |
| **Inspecting Containers**                    | `docker inspect [CONTAINER_ID/NAME]`                                                 | Provides detailed information about a container.                     |
|                                              | `docker inspect --format='{{.State.Status}}' [CONTAINER_ID/NAME]`                    | Retrieves the status of a container.                                 |
| **Viewing Container Stats**                  | `docker stats [CONTAINER_ID/NAME]`                                                   | Displays resource usage statistics of running containers.            |
| **Pausing and Unpausing Containers**         | `docker pause [CONTAINER_ID/NAME]`                                                   | Pauses all processes within a running container.                     |
|                                              | `docker unpause [CONTAINER_ID/NAME]`                                                 | Resumes a paused container.                                          |
| **Copying Files Between Container and Host** | `docker cp [OPTIONS] CONTAINER_ID:/path/to/container/file /path/to/host/destination` | Copies files or folders between a container and the host filesystem. |
| **Managing Container Resources**             | `docker update [OPTIONS] CONTAINER_ID`                                               | Updates container resource limits and configurations.                |

## 4.3. Viewing Container Information: `docker inspect`, `docker stats`

| Category                          | Command                                                                                                  | Description                                                                                                                                        |
| --------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Inspecting Containers**         | `docker inspect [CONTAINER_ID/NAME]`                                                                     | Provides detailed information about a container, including its configuration, network settings, etc.                                               |
| **Displaying Container Logs**     | `docker logs [OPTIONS] [CONTAINER_ID/NAME]`                                                              | Retrieves the logs of a container. Options include following logs in real-time (`-f, --follow`) and tailing a specific number of lines (`--tail`). |
| **Listing Containers**            | `docker ps`                                                                                              | Lists running containers along with their status, uptime, and resource usage.                                                                      |
|                                   | `docker ps -a`                                                                                           | Lists all containers, including stopped ones, along with their status.                                                                             |
| **Displaying Container Stats**    | `docker stats [CONTAINER_ID/NAME]`                                                                       | Displays resource usage statistics of running containers, such as CPU and memory usage.                                                            |
| **Checking Container Status**     | `docker inspect --format='{{.State.Status}}' [CONTAINER_ID/NAME]`                                        | Retrieves the status of a container (running, stopped, paused, etc.).                                                                              |
| **Querying Container IP Address** | `docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' [CONTAINER_ID/NAME]` | Retrieves the IP address of a container.                                                                                                           |

---
