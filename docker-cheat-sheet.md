# Docker Cheat Sheet

## Docker Basics

- **Images**: Read-only templates used to create containers. They contain everything needed to run a container, including the application code, runtime, libraries, and dependencies.
- **Containers**: Runnable instances of an image. Containers provide a lightweight, isolated environment for running applications.
- **Dockerfile**: A text file that contains instructions for building Docker images. It specifies the base image, commands to install dependencies, configure the environment, and run the application.
- **Docker Engine**: The client-server application responsible for managing Docker objects, such as images, containers, networks, and volumes.
  - **Docker Daemon (dockerd)**: The server component that listens for Docker API requests and manages Docker objects.
  - **Docker CLI (docker)**: The command-line interface used to interact with the Docker daemon.
- **Docker Hub**: A centralized repository for Docker images, where users can share, pull, and push images.

## Docker Commands

### Management Commands

- **Build an image**: `docker build -t <image_name> .`
  - Builds a Docker image using the Dockerfile in the current directory.
- **List images**: `docker images`
  - Displays a list of Docker images on the local system.
- **Run a container**: `docker run <image_name>`
  - Creates and starts a container based on the specified image.
- **List containers**: `docker ps` (active) or `docker ps -a` (all)
  - Lists active containers or all containers, including stopped ones.
- **Stop container**: `docker stop <container_id>`
  - Stops a running container.
- **Remove container**: `docker rm <container_id>`
  - Removes one or more containers.
- **Remove image**: `docker rmi <image_name>`
  - Removes one or more images.
- **View logs**: `docker logs <container_id>`
  - Displays the logs of a specific container.
- **Inspect container**: `docker inspect <container_id>`
  - Returns low-level information about a container.
- **Inspect image**: `docker image inspect <image_name>`
  - Returns low-level information about an image.
- **Pull image from Docker Hub**: `docker pull <image_name>`
  - Downloads an image from Docker Hub to the local system.
- **Push image to Docker Hub**: `docker push <image_name>`
  - Pushes an image from the local system to Docker Hub.
- **Tag image**: `docker tag <image_id> <new_image_name>`
  - Tags an existing image with a new name and optionally a new tag.
- **Save image to file**: `docker save -o <output_file_name> <image_name>`
  - Saves one or more images to a tar archive file.
- **Load image from file**: `docker load -i <input_file_name>`
  - Loads images from a tar archive file.
- **Prune unused resources**: `docker system prune`
  - Removes unused data, including stopped containers, dangling images, and more.

### Dockerfile Instructions

- **FROM**: Specifies the base image for subsequent instructions in the Dockerfile.
- **RUN**: Executes commands in a new layer on top of the current image and commits the result.
- **COPY / ADD**: Copies files or directories from the host machine to the container's filesystem.
- **WORKDIR**: Sets the working directory for the following instructions.
- **EXPOSE**: Informs Docker that the container listens on specific network ports at runtime.
- **CMD**: Specifies the default command to run when the container starts.
- **ENTRYPOINT**: Configures a container that will run as an executable.

## Docker Compose

- **Definition file**: `docker-compose.yml`
  - YAML file used to define multi-container Docker applications.
- **Build services**: `docker-compose build`
  - Builds Docker images for services defined in the Docker Compose file.
- **Run services**: `docker-compose up`
  - Creates and starts containers for all services defined in the Docker Compose file.
- **Run services in the background**: `docker-compose up -d`
  - Starts containers in detached mode (in the background).
- **Stop services**: `docker-compose down`
  - Stops and removes containers, networks, and volumes created by `docker-compose up`.
- **View logs**: `docker-compose logs`
  - Displays logs for services defined in the Docker Compose file.

## Docker Networking

- **Bridge Network**: Default network created when Docker is installed. Containers connected to the same bridge can communicate with each other.
- **Host Network**: Containers share the network namespace with the Docker host and can communicate directly.
- **Overlay Network**: Connects multiple Docker daemons across multiple hosts, enabling communication between containers running on different hosts.
- **Macvlan Network**: Assigns a MAC address to each container's virtual network interface, allowing containers to appear as physical devices on the network.

## Docker Volumes

- **Bind Mounts**: Links a directory on the host machine to a directory within a container, allowing data to persist beyond the container lifecycle.
- **Volumes**: Persistent storage managed by Docker, independent of the container's lifecycle. Volumes are preferred for persisting data in production environments.
- **Volume Drivers**: Plugins that enable the use of external storage systems (e.g., NFS, AWS EBS) as Docker volumes.

## Docker Security

- **User Namespaces**: Maps container users to host users, providing an additional layer of isolation and security.
- **AppArmor / SELinux**: Mandatory access control systems that enforce security policies and restrict container capabilities.
- **Docker Content Trust**: Enables digital signing and verification of images to ensure authenticity and integrity.
- **Secrets Management**: Safely stores sensitive data (e.g., passwords, API keys) and injects them into containers at runtime.

## Docker Swarm

- **Swarm Mode**: Built-in orchestration tool in Docker for managing a cluster of Docker hosts.
- **Manager Nodes**: Control the swarm and maintain cluster state.
- **Worker Nodes**: Execute tasks dispatched by manager nodes.
- **Services**: Define tasks to execute across the swarm, specifying desired state and constraints.
- **Stacks**: Group related services into a single unit for easier management and deployment.
- **Tokens**: Used for authentication and communication between nodes in the swarm.

## Docker Tips

- **Use Multi-Stage Builds**: Reduce final image size by separating build and runtime environments in Dockerfile.
- **Leverage Caching**: Utilize Docker's layer caching mechanism during builds to speed up subsequent builds.
- **Use .dockerignore**: Exclude unnecessary files and directories from being copied into the image during the build process.
- **Monitor Resource Usage**: Monitor CPU, memory, and disk usage of Docker containers to optimize resource allocation.
- **Regularly Update Images**: Keep Docker images and containers up-to-date with the latest security patches and software updates.
- **Backup Data Volumes**: Regularly back up critical data stored in Docker volumes to prevent data loss in case of container failure or data corruption.
