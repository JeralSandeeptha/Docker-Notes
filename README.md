# Docker-Practice 

# How to setup Docker for Windows

(01.) First we need to setup the windows before installation.
  *   Go to Windows Features
  *   Then tick WSL(Windows Sub System for Linux) and Virtual Machine Platform

(02.) Then we need to restart the machine.

(03.) Then we need to check whether WSL and VMP is correctly enabled or not. 
      For that,
  *   Go to powershell
  *   To check WSL version ----> wsl --version
  *   To check WSL         ----> wsl --install
  *   To update WSL        ----> wsl --update
  *   WSL config           ----> wsl --set-default-version 2
  *   To windows version   ----> winver

(04.) Donwload and install docker desktop.

(05.) Open Docker Desktop.

(06.) Sign in to Docker Hub using docker desktop.

(07.) We should start the docker desktop service in background services.

(08.) Docker Setup successful.


# Docker Management Commands

docker version: Show the Docker version information.

docker info: Display system-wide information about Docker.

docker system df: Show Docker disk usage.

docker system prune: Remove unused data (containers, networks, images, volumes).

docker system prune -a: Remove all unused images not just dangling ones.

docker system prune --volumes: Remove all unused volumes.

docker system events: Get real-time events from the server.

docker system logs: Fetch the logs of a container.

# Docker Image Commands

docker images: List all images.

docker image ls: List all images.

docker image build -t <image_name> .: Build an image from a Dockerfile.

docker image pull <image_name>:<tag>: Pull an image from a registry.

docker image push <image_name>:<tag>: Push an image to a registry.

docker image rm <image_id>: Remove an image.

docker image inspect <image_name>: Display detailed information on one or more images.

# Docker Container Commands

docker ps: List running containers.

docker ps -a: List all containers (including stopped ones).

docker create <image_name>: Create a new container from an image.

docker start <container_id>: Start a stopped container.

docker stop <container_id>: Stop a running container.

docker restart <container_id>: Restart a container.

docker pause <container_id>: Pause a running container.

docker unpause <container_id>: Unpause a paused container.

docker exec -it <container_id> <command>: Run a command in a running container.

docker attach <container_id>: Attach local standard input, output, and error streams to a running container.

# Docker Network Commands

docker network ls: List all networks.

docker network inspect <network_id>: Display detailed information on one or more networks.

docker network create <network_name>: Create a new network.

docker network connect <network_id> <container_id>: Connect a container to a network.

docker network disconnect <network_id> <container_id>: Disconnect a container from a network.

# Docker Volume Commands

docker volume ls: List all volumes.

docker volume create <volume_name>: Create a new volume.

docker volume inspect <volume_name>: Display detailed information on one or more volumes.

docker volume rm <volume_name>: Remove a volume.

# Docker Docker Compose Commands

docker-compose up: Start services defined in a docker-compose.yml file.

docker-compose down: Stop services defined in a docker-compose.yml file.

docker-compose build: Build or rebuild services.

docker-compose logs: View output from services.

docker-compose exec <service_name> <command>: Execute a command in a running container.

# Docker Swarm Commands

docker swarm init: Initialize a swarm.

docker swarm join: Join a swarm as a node.

docker swarm leave: Leave the swarm.

docker node ls: List nodes in the swarm.

docker service ls: List services in the swarm.

docker service create: Create a new service.

# Docker Miscellaneous Commands

docker login: Log in to a Docker registry.

docker logout: Log out from a Docker registry.

docker search <image_name>: Search for an image on Docker Hub.

docker cp <file_path> <container_id>:<path_in_container>: Copy files or folders between a container and the local filesystem.

docker wait <container_id>: Block until a container stops, then print its exit code.
