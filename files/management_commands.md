# Docker Management Commands

## Docker Basic Commands
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

## Docker Swarm Commands
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
