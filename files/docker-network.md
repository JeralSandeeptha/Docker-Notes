# Docker Network
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

## Docker Network Commands
`docker network ls`: List all networks.
`docker network inspect <network_id>`: Display detailed information on one or more networks.
`docker network create <network_name>`: Create a new network.
`docker network connect <network_id> <container_id>`: Connect a container to a network.
`docker network disconnect <network_id> <container_id>`: Disconnect a container from a network.
