# Docker Notes

<br />

## Table of Contents
- [Introduction](./files/introduction.md)
- [Components](./files/components.md)
- [Container Lifecycle](./files/lifecycle.md)
- [Docker Images](./files/docker-images.md)
- [Docker Volumes](./files/volumes.md)
- [Resource Management](./files/resource-management.md)
- [Restart Policies](./files/restart_policies.md)
- [Docker Compose](./files/compose.md)
- [Docker Network](#docker-network)
- [How to setup docker for Windows](#how-to-setup-docker-for-windows)

<br /><br />

## Docker Network
- Docker networks allow containers to communicate with each other, the Docker host, and the internet in a secure and flexible way

- Types of Networks

| Network Type | Description                                                 |
| ------------ | ----------------------------------------------------------- |
| `bridge`     | Default network for containers. Ideal for standalone apps.  |
| `host`       | Shares the host’s network stack. Fastest, but no isolation. |
| `none`       | No network. Container is completely isolated.               |
| `overlay`    | Used in Swarm mode for multi-host communication.            |
| `macvlan`    | Assigns MAC address to containers (advanced).               |
 
- Inspect Docker Networks
```cmd
docker network ls         # List networks
docker network inspect bridge  # Inspect details
```  

- Connecting Containers
```cmd
docker network create my-net
docker run -d --name app1 --network my-net myimage
docker run -d --name app2 --network my-net anotherimage
```

### Docker Network Commands
`docker network ls`: List all networks.
`docker network inspect <network_id>`: Display detailed information on one or more networks.
`docker network create <network_name>`: Create a new network.
`docker network connect <network_id> <container_id>`: Connect a container to a network.
`docker network disconnect <network_id> <container_id>`: Disconnect a container from a network.

<br /><br />

## How to setup Docker for Windows  
 
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

<br /><br />

## Docker Management Commands
docker version: Show the Docker version information.
docker info: Display system-wide information about Docker.
docker stats: Display all about the usages of the current run time.
docker system df: Show Docker disk usage.
docker system prune: Remove unused data (containers, networks, images, volumes).
docker system prune -a: Remove all unused images not just dangling ones.
docker system prune --volumes: Remove all unused volumes.
docker system events: Get real-time events from the server.
docker system logs: Fetch the logs of a container.

<br /><br />

### Docker Swarm Commands
docker swarm init: Initialize a swarm.
docker swarm join: Join a swarm as a node.
docker swarm leave: Leave the swarm.
docker node ls: List nodes in the swarm.
docker service ls: List services in the swarm.
docker service create: Create a new service.

<br /><br />

## Docker Miscellaneous Commands
docker login: Log in to a Docker registry.
docker logout: Log out from a Docker registry.
docker search <image_name>: Search for an image on Docker Hub.
docker cp <file_path> <container_id>:<path_in_container>: Copy files or folders between a container and the local filesystem.
docker wait <container_id>: Block until a container stops, then print its exit code.
