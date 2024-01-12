# Docker in the Real World

## Creating a Dockerfile
- Some notes: On creating a Dockerfile, install the dependencies first instead of copying the files
- Do this
```diff
+ FROM python
+
+ RUN mkdir /app
+ WORKDIR /app
+
+ COPY requirements.txt requirements.txt
+ RUN pip install -r requirements.txt
+
+ COPY . .
```
- Not this
```diff
- FROM python
-
- RUN mkdir /app
- WORKDIR /app
-
- COPY . .
-
- RUN pip install -r requirements.txt
```
- `Dockerfile`
```dockerfile
FROM python

RUN mkdir /app
WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY . .

LABEL maintainer="Some maintainer address" \
      version="1.0"

CMD flask run --host=0.0.0.0 --port=5000
```

## Running Docker Containers
- Building the docker image by `docker build -t <name> .`
- Listing all images `docker image ls`
- Listing all running containers `docker container ls`, append `-a` to show stopped containers
- Show container logs `docker container logs <name>`, tailing it by passing `-f` argument
- Show container stats `docker container stats`
- Stop a container `docker container stop <name>`
- Delete image `docker image rmi <name>`
- Running the docker container `docker run <name>`
- Other arguments
    - `-it` - Enable docker to handle linux signals, terminal colors and realtime inputs.
    - `-d` - Run in detached mode
    - `-p` - Ports, provide two ports `x:y` where `x` is host machine port to be bind to, and `y` is the docker image port to be bind to. If only one port is provided, then docker will assign a random host port.
    - `-e` - Environment variables to be passed on. Can be used multiple times.
    - `--rm` - Automatically remove container when exiting
    - `--name` - Give the container a name instead of a random one
    - `--restart <opts>` - Restarts a container depending on the option supplied. (Conflicts with `--rm` argument)
    - `<name>` - The docker image to run
- Do `service docker restart` as root when the docker daemon dies out

## Live Code Reloading with Volumes
- Run the docker image `docker run -it -p 5000:5000 -e FLASK_APP=app.py --rm --name web1 web1`
- Adding `-e FLASK_DEBUG=1` environment variable will make flask in debug mode
- Mounting a volume with `-v src:dst` where `src` is the host machine's directory to be mounted to docker, and `dst` is where to mount the `src` folder inside docker.

## Debugging Tips and Tricks
- Entering to the container `docker exec -it <name> bash`. Supplying `--user` flag will run as user mode, useful when mounting volumes to prevent `root` from owning the file, adding `--user "$(id -u):$(id -g)"` will use the host's system user ID and group ID to be passed in the docker file.

## Linking Containers with Docker Networks
- `docker network ls` - List all docker network adapters
- `docker network inspect <adapter>` - Inspects the specified adapter
- `docker network create --driver bridge firstnetwork` - Creates a new docker network named `firstnetwork` as bridged network
- `--net <network_name>` - Sets the container's network to the specified network on `docker run`
- About network drivers, `bridged` can only connect to containers on the same docker host, and on multiple hosts, you can look into `overlay` network driver

## Persisting data to Your Docker Host (Data Volumes)
- Using named volumes, e.g `web2_redis:/data`, `x:y` where `x` is the volume name, and `y` is the mount point inside the docker container
- `docker volume create web2_redis` - Creates a volume named `web2_redis`
- `docker volume ls` - Lists all volumes
- `docker volume inspect web2_redis` - Inspects the volume `web2_redis`
- Add `-v x:y` to use the volume and mount it inside the docker container

## Sharing data between containers
- On Dockerfile, `VOLUME ["/app/public"]` - it means that docker to expose this directory as a volume when the container runs. This volume will become accessible by other containers as long as they reference it.
- Second option: `-v /app/public`, an option without inside the Dockerfile
- Run first the flask image and then the redis image
- `docker run --rm -itd -p 5000:5000 -e FLASK_APP=app.py -e FLASK_DEBUG=1 --name web2 -v $PWD:/app --net firstnetwork web2`
- `docker run --rm -itd -p 6379:6379 --name redis --net firstnetwork -v web2_redis:/data --volumes-from web2 redis:3.2-alpine`

## Optimizing your docker images
- Using `.dockerignore` - acts like `.gitignore` but for docker especially in docker version control
- Pros
    - Substantially smaller
    - Package dependencies don't change often
- Cons
    - Adding more dependencies, the run command will be executed again
    - Complicates `Dockerfile`

## Running scripts when a container starts
- Dockerfile instruction `ENTRYPOINT`, allows to execute a script after the docker container starts
- Best used when passing an environment variable by passing `-e`
- `docker run --rm -it -p 5000:5000 -e FLASK_APP=app.py -e FLASK_DEBUG=1 --name webentrypoint -v $PWD:/app --net firstnetwork webentrypoint`
- `docker run --rm -it -p 5000:5000 -e FLASK_APP=app.py -e FLASK_DEBUG=1 -e WEB2_COUNTER_MSG="Docker fans have visited this page" --name webentrypoint --net firstnetwork webentrypoint`

## Cleaning up
- `docker container ls` - List all containers, append `-a` to show stopped containers
- `docker system df` - Show disk space is being used by docker, append `-v` is verbose
- `docker image ls` - Shows all docker images, any image that has the `<none>` tag are dangling/unused images
- `docker system info` - Display information about docker installation
- `docker system prune` - Prunes all safe to delete images and containers, append `-f` to delete automatically, `-a` is a dangerous argument
- `docker stop name1 name2 name3` - Stops containers `name1`, `name2` and `name3`
- `docker stop $(docker container ls -a -q)` - Stops multiple containers especially on running more than 10 or more docker containers