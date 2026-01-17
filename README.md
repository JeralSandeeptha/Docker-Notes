# Docker Notes

<br />

## Table of Contents
- [Introduction](./files/introduction.md)
- [Components](./files/components.md)
- [Container Lifecycle](./files/lifecycle.md)
- [Docker Images](./files/docker-images.md)
- [Docker Volumes](./files/volumes.md)
- [Resource Management](#resource-management)
- [Restart Policies](#restart-policies)
- [Docker Compose](#docker-compose)
- [Docker Network](#docker-network)
- [How to setup docker for Windows](#how-to-setup-docker-for-windows)

<br /><br />

## Resource Management
- Docker lets you limit and control the amount of system `resources` (`CPU`, `memory`, etc.) your containers use. This is helpful when running multiple containers or on shared infrastructure.
- We can identify 3 resources in docker container
 - `CPU`
 - `Memory`
 - `Network`

- If you want to get quick details
```cmd
docker stats
```

- Common Resource Constraints

| Resource       | Flag                                      | Example                          | Description                          |
| -------------- | ----------------------------------------- | -------------------------------- | ------------------------------------ |
| **Memory**     | `--memory` or `-m`                        | `-m 512m`                        | Limits memory to 512MB               |
| **CPU shares** | `--cpu-shares`                            | `--cpu-shares 512`               | Relative weight; default is 1024     |
| **CPU quota**  | `--cpu-quota`                             | `--cpu-quota=50000`              | Microseconds of CPU time allowed     |
| **CPU period** | `--cpu-period`                            | `--cpu-period=100000`            | Period for CPU quota (default 100ms) |
| **CPU limit**  | `--cpus`                                  | `--cpus="1.5"`                   | Set number of CPUs directly          |
| **PIDs limit** | `--pids-limit`                            | `--pids-limit=100`               | Limit number of processes            |
| **Disk I/O**   | `--device-read-bps`, `--device-write-bps` | `--device-read-bps=/dev/sda:1mb` | Limit disk I/O bandwidth             |

### CPU
-  This allows you to control how much CPU power your containers use, which is vital when running multiple containers or optimizing performance.

- Why Manage CPU in Docker?
 - Prevent one container from hogging all the CPU.
 - Ensure fair CPU usage across multiple containers.
 - Simulate CPU limits for testing or production constraints.

- `--cpus` – Limit CPU cores directly
```bash
// ✅ This means the container can use up to 1.5 CPU cores.
docker run --cpus="1.5" myapp
```

- `--cpu-shares` – Set relative CPU priority
```bash
docker run --cpu-shares=512 myapp

/*
Default is 1024.
It’s not a hard limit, but a weight.
If two containers are running:
 One has 1024, the other 512
 The first gets twice as much CPU time as the second.
✅ Useful when all containers compete for CPU.
*/
```

- `--cpu-quota` and `--cpu-period` – Fine-grained control
```bash
docker run --cpu-quota=50000 --cpu-period=100000 myapp

/*
This allows the container to use 50% of a single CPU.
Formula: quota / period = CPU usage
Default period is 100000 µs (100 ms)
✅ Useful when you want precise CPU limits, especially for high-density setups.
*/
```

- `--cpuset-cpus` – Pin container to specific CPU cores
```bash
docker run --cpuset-cpus="0,2" myapp

/*
✅ This forces the container to run only on CPU 0 and 2.

✅ Good for:
Performance isolation
Real-time or latency-sensitive apps
*/
```

### Memory
- An essential topic for running containers efficiently and avoiding crashes due to memory overuse.

- By default, Docker containers can use all available system memory, which can lead to:
 - Memory exhaustion on the host
 - One container killing others (via OOM – Out Of Memory)
 - Performance bottlenecks

- `--memory` or `-m` → Set max memory limit
```bash
docker run -m 512m nginx

/*
This limits the container to 512MB of RAM.

You can also use:
 k (kilobytes)
 m (megabytes)
 g (gigabytes)
*/
```

- `--memory-swap` → Set total memory + swap
```bash
docker run -m 512m --memory-swap 1g nginx

/*
This means:
512MB RAM

512MB swap (total: 1GB memory usage allowed)
🧠 Swap is slower than RAM and is used when memory runs out.
*/
```

- `--memory-reservation` → Soft limit (ideal usage)
```bash
docker run --memory-reservation=300m -m 512m nginx

/*
If under 300MB → container runs smoothly.
If memory pressure occurs → Docker tries to keep it under 300MB.
Hard limit remains 512MB.
*/
```

- `--oom-kill-disable` → Prevent auto-killing
```bash
docker run -m 512m --oom-kill-disable nginx

/*
Disables Docker's Out Of Memory killer, which normally kills containers that exceed memory.
⚠️ Use carefully — container may hang instead of being killed.
*/
```

- `--kernel-memory` (Deprecated in newer Docker versions) - (Deprecated)

### Network
- Docker uses network drivers to enable communication between containers, host, and the outside world
![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1751199734/6_bro6yv.png)

<br /><br />

## Restart Policies
- Restart policies help ensure your containers automatically restart under certain conditions (like after a crash or reboot)

### ✅ Common Restart Policies
| Policy                     | Behavior                                                                 |
| -------------------------- | ------------------------------------------------------------------------ |
| `no` (default)             | Do not restart                                                           |
| `always`                   | Always restart the container no matter what                              |
| `unless-stopped`           | Restart always except when explicitly stopped by user                    |
| `on-failure[:max-retries]` | Restart only if the container exits with a non-zero status (e.g., crash) |

```cmd
docker run --restart=unless-stopped myapp
```

<br /><br />

## Docker Compose
- `Docker Compose` lets you define and run multiple Docker containers using a single configuration file: docker-compose.yml.
- Instead of running multiple docker run commands, you can:
  - Define all services (e.g., app, database, frontend)
  - Set their configuration (ports, env, volumes, etc.)
  - Start everything with one command
    
- To run compose file
```bash
docker compose up
```
- To stop compose file
```bash
docker compose down
```

![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1751212793/7_asxq3z.png)
![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1751212814/8_mgtuiu.png)

### Docker Docker Compose Commands
docker-compose up: Start services defined in a docker-compose.yml file.
docker-compose down: Stop services defined in a docker-compose.yml file.
docker-compose build: Build or rebuild services.
docker-compose logs: View output from services.
docker-compose exec <service_name> <command>: Execute a command in a running container.

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
