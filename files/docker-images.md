# Docker Images
- A Docker image is a lightweight, standalone, and executable package that contains everything needed to run a piece of software
- A Docker image is a blueprint or template for creating Docker containers.
- It includes,
 - The application code
 - Runtime environment (e.g., Node.js, Python, Java)
 - System tools and libraries
 - Configuration files

![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1750979806/2_rm0wlu.png)

- To create a `Docker Image` we need to create a `Dockerfile` first. `Dockerfile` includes all the steps and other instructions to create the `Docker Image`
- Executes top to bottom

![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1751125839/3_pgt6xv.png)

## Docker Layered Architecture
- We can see the layeres of a docker image. It shows all the layers and their sizes.
```docker
docker history <container_name>
```
- There are images called `Distroless Images`. It means they are minimal docker images that contain necessary runtime dependencies of apps.
![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1751151171/4_b6zdrs.png)
- These `Ditroless Images` doesn't allows us to install unsusal things like dependencies because they are minimal images. In that case we have to use `Multi Stage Builds`
- We can not access shells in `Ditroless Images`

## Docker Image Commands
docker images: List all images.
docker image ls: List all images.
docker image build -t <image_name> .: Build an image from a Dockerfile.
docker image pull <image_name>:<tag>: Pull an image from a registry.
docker image push <image_name>:<tag>: Push an image to a registry.
docker image rm <image_id>: Remove an image.
docker image inspect <image_name>: Display detailed information on one or more images.
