# Docker Compose
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

## Docker Docker Compose Commands
docker-compose up: Start services defined in a docker-compose.yml file.
docker-compose down: Stop services defined in a docker-compose.yml file.
docker-compose build: Build or rebuild services.
docker-compose logs: View output from services.
docker-compose exec <service_name> <command>: Execute a command in a running container.
