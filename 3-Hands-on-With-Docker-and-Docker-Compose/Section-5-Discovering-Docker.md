# Discovering Docker

## Hello World with Docker
- `docker run hello-world`
- If the image does not exist, it will download the container automatically from the Docker Hub.
- The Docker daemon created a new container from that image which runs the executable that produces the output you are currently reading.
- The Docker daemon streamed that output to the Docker client, which sent it to your terminal.

## Docker Image and Container
- Images and containers are two different things.
- A docker image is a combination of file system and parameters, a single package that rolls up everything you need to run an application.
- A docker image doesn't have any state attached to it and once built it never changes.
- A docker image is you can download, build and run.
- The act of running an image is a container. e.g Image -> class, while Container -> instance
- A docker image as a result of running a series of steps, called build process. The steps are define on a `Dockerfile`.
- One image, many containers.
- Containers are immutable, meaning any changes that you make while running will be lost forever when stopped.

## Docker Build Process
- 2 ways to build a docker image
    - (Rarely used) Run a docker container, make changes with `docker commit`
    - (Mostly used) A `Dockerfile` - is a file where all the step by step process of the build are written, more like a recipe book on how to create the docker image
- Builds only what changed