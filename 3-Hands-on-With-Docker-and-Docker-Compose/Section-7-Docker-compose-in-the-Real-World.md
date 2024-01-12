# Docker compose in the Real World
- Using `docker run` is tiresome
- Create only a single file `docker-compose.yml` and run a single command
- Docker compose is flexible, a valuable tool

## Adding docker compose to support the web app
```yaml
version: '3'

services:
  redis:
    image: 'redist:3.2-alpine'
    ports:
      - '6379:6379'
    volumes:
      - 'redis:/data'

  web:
    build: '.'
    depends_on:
      - 'redis'
    env_file:
      - '.env'
    # environment:
      # FLASK_DEBUG: 'true'
    # image: 'username/name:1.0'
    ports:
      - '5000:5000'
    volumes:
      - '.:/app'

volumes:
  redis: {}
```

## Managing our web app with docker compose
- `docker compose --help` - Opens the docker compose help
- `docker compose build` - Build images
- `docker compose pull` - Pull images from hub.docker.com
- `docker compose up` - Start the containers
- `docker compose stop` - Stop all containers
- `docker compose up --build -d` - Build and run in the background and run containers.
- `docker compose logs -f` - Tail the output
- `docker compose restart` - Restart all containers
- `docker compose restart name1` - Restart only `name1` container
- `docker compose exec name1` - Execute a command on `name1` container
- `docker compose run name1 [[command] args]` - Execute a command and exit once finished
- `docker compose up name1` - Starts only `name1` container, unless there is a `depends_on` option on docker-compose.yml
- `docker compose rm` - Remove stopped containers

## Docker compose API v1 / v2 / v3
- v1 is legacy
- v2 is relevant
- [Docker Compose File Versions Documentation](https://docs.docker.com/compose/compose-file/compose-versioning/)
