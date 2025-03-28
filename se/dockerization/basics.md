# Docker
### Virtualization
A host machine with CPU, memory, and I/O resources allocates a portion of these resources to a virtual machine, which runs a complete operating system. A hypervisor, such as VMware or VirtualBox, manages these virtual machines, handling tasks like creation, deletion, memory allocation, and other resource management functions.
### Containerization
It's a lightweight environment where processes run on the host machine but are isolated within a confined space, unable to interact with resources outside their designated boundaries. Techniques like `chroot` (which redefines the root directory for a process) and `rlimit` (which limits memory usage) play a key role in achieving this isolation.

* Isolated containers
* Portability & sharing - Built one time, run forever
* Fast starting & running
* Light & easy
* Multiple containers can be runned at one time
## Docker hub
Used for storing and sharing Docker images.
```bash
docker run node:18
```
Runs node 18. version, **if it is not installed locally then it will pull from docker hub.**
Most of the times this process pulls multiple images which often called **overlapping layers**. This is necessary because to run a node we need an operating system, a runtime js, etc. which are separate images.

Our **applications always runs as a container** which is built by the image.
## Image
It's is a lightweight, standalone, and **executable package that includes everything needed to run a piece of software**, including the code, runtime, libraries, and system tools. Act as a **set of instructions** to build a Docker container.
Docker images also act as the **starting point** when using Docker.

`docker build` produces a static snapshot of the application and its environment based on the Dockerfile.
> An image is comparable to a snapshot in virtual machine environments.
* `docker images`
* `docker rmi <image_id>` removes an image.
* `docker image prune` removes unused images.
* `docker pull <image_name>:<tag>` pulls an image from a registry.
* `docker build -t <image_name>:<tag> <path_to_Dockerfile>` builds an image from a Dockerfile.
* `docker push <image_name>:<tag>`: pushes an image to a registry.

- `docker inspect <image_name>` shows detailed information.
## Container
A Docker container is a **runnable instance of a Docker image**. It encapsulates an application and its dependencies, isolated from the host system and other containers.

Containers created from the same image share the same application environment, ensuring consistency across different stages of the development lifecycle and across different deployment environments; development, testing and production .
* `docker ps`
* `docker start <container_id>`
* `docker stop <container_id>`
* `docker restart <container_id>`
* `docker pause <container_id>`
* `docker unpause <container_id>`
* `docker rm <container_id>` removes a stopped container.
* `docker kill <container_id>` sends a signal to stop a container.

- `docker logs <container_id>` views container logs.
- `docker stats <container_id>` displays real-time container resource usage.
- `docker inspect <container_id>` shows detailed information
- `docker exec -it <container_name_or_id> <command>` executes a command in a running container.
> `docker exec -it <container_id> /bin/bash`
# Connection between Dockerfile, Image and Container
Dockerfile defines the build instructions for a Docker image, and Docker containers are instances of Docker images that run applications in an isolated and reproducible environment.
1. The Dockerfile as a blueprint.
2. Create image by running `docker build` 
3. Instantiate container from images using the `docker run` command.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg5OTUwMjAyOF19
-->