# Container Lifecycle

![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1750912804/1_os9aug.png)

## Docker Container Commands
- `docker ps`: List running containers.
- `docker ps -a`: List all containers (including stopped ones).
- `docker ps --filter name=<container_name>`: Filtering options
- `docker create <image_name>`: Create a new container from an image.
- `docker start <container_id>`: Start a stopped container.
- `docker stop <container_id>`: Stop a running container.
- `docker restart <container_id>`: Restart a container.
- `docker rm <container_id>`: Remove a container.
- `docker pause <container_id>`: Pause a running container.
- `docker unpause <container_id>`: Unpause a paused container.
- `docker exec -it <container_id> <command>`: Run a command in a running container.(docker exec -it nginx sh)
- `docker attach <container_id>`: Attach local standard input, output, and error streams to a running container.
