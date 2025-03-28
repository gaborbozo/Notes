# Dockerfile
A Dockerfile is a text file that contains a **set of instructions for building a Docker image**. It specifies the base image, sets up the environment, installs dependencies, and defines other configuration settings.
## Often used parameters
### FROM
Prerequisites for the application
```dockerfile
FROM node:18
``` 
### WORKDIR
Sets the current working directory for subsequent instructions in the Dockerfile.
```dockerfile
WORKDIR /app
```
### COPY
Copies files from a local source location to a destination in the Docker container
```dockerfile
COPY . .
```
### RUN
Execute any commands in a new layer on top of the current image and commit the results.
A Dockerfile can have many RUN steps that layer on top of one another to build the image.
### EXPOSE
informs Docker that the container listens on the specified network ports at runtime.
```dockerfile
EXPOSE 3000
```
If an app is exposed to run an image port switch need to be indicated `-p 10101:3000` --- application can be reached through 10101
### CMD
CMD is the command the container executes by default when you launch the built image.
### ENTRYPOINT
Similar to CMD and can modify the way a CMD is interpreted when container is started from an image
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjkxMzE4MTM5XX0=
-->