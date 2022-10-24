# Docker commands

See docker version

```bash
docker --version
```

View docker status

```bash
docker info
```

Run a container

```bash
docker run <image name>
```

See the containers running

    $ docker ps

See all containers

    $ docker ps -all

    $ docker ps -a

Get information from a container

    $ docker inspect <container id>

    $ docker inspect <container name>

Name a container

    $ docker run --name <container name> <image name>

Rename a container

    $ docker rename <current name> <new name>

Remove a container

    $ docker rm <container id>

    $ docker rm <container name>

Remove a running container

    $ docker rm -f <container id>

    $ docker rm -f <container name>    

Run a container in interactive mode

    $ docker run -it <image name>

Run a container in the background

    $ docker run --detach <image name>

    $ docker run -d <image name>

Run a container with a custom command

    $ docker run -d <image name> <custom command>

Connect to a running container

    $ docker exec -it <container id> <custom command>

    $ docker exec -it <container name> <custom command>

Stop a container

    $ docker stop <container id>

    $ docker stop <container name>

Expose a container

    $ docker run -p <machine port>:<container port> <image name>

View container logs

    $ docker logs <container id>

    $ docker logs <container name>

View the logs of a container indefinitely

    $ docker logs -f <container id>

    $ docker logs -f <container name>

View the last n lines of logs

    $ docker logs --tail=10 -f <container id>

    $ docker logs --tail=10 -f <container name>

See the logs of the last minute

    $ docker logs --since=1m -f <container id>

    $ docker logs --since=1m -f <container name>

Docker bind mounts

    $ docker run -v <machine directory>:<container directory> <image name>

List existing volumes

    $ docker volume ls

Create a new volume

    $ docker volume create <volume name>

Mount a volume to a container

    $ docker run --mount src=<volume name>,dst=<container directory> <image name>

Delete volumes that are not being used

    $ docker volume prune

Copy files from machine to container

    $ docker cp <file path> <container id>:<path into container>

    $ docker cp <file path> <container name>:<path into container>

Copy files from container to machine

    $ docker cp <container id>:<path into container> <file path>

    $ docker cp <container name>:<path into container> <file path> 

View the images that are in the local environment

    $ docker image ls

    $ docker images

Bring an image from a repository to the local environment

    $ docker pull <image name>:<version>

Publish an image to the repository

    $ docker push <repository name>/<software name>:<software version>

Build an image

    $ docker build -t <repository name>/<software name>:<software version> .

Change the tag of an image

    $ docker tag <current tag> <new tag>

Build history of an image

    $ docker history <image name>

Show network interfaces

    $ docker network ls

Create a network interface

    $ docker network create --attachable <network name>

Delete a network interface

    $ docker network rm <network id>

    $ docker network rm <network name>

Inspect a network interface

    $ docker inspect <network id>

    $ docker inspect <network name>

Connect a container to a network interface

    $ docker network connect <network id> <container id>

    $ docker network connect <network name> <container name>

Pass environment variables

    $ docker run --env <variable name>=<variable value> <container id>

    $ docker run --env <variable name>=<variable value> <container name>

## Docker compose

Example of a compose file "docker-compose.yml"

```yml
version: "3.8"

services:

  app:
    image: rgalicia0729/test
    environment:
      MONGO_URL: 'mongodb://db:27017/test'
    volumes:
      -.:/usr/app
      -/usr/app/node_modules
    depends_on:
      - db
    ports:
      - "3000:3000"

  db:
    image: mongo
```

Docker compose build

    $ docker-compose build

Run docker compose services

    $ docker-compose up -d

View docker compose services

    $ docker-compose ps

View docker compose services logs

    $ docker-compose logs

View the logs of a specific service

    $ docker-compose logs <service name>

Run a command on a compose service

    $ docker-compose exec <service name> <custom command>

Destroy compose services

    $ docker-compose down

Compose override "docker-compose.override.yml"

```yml
version: "3.8"

services:

  app:
    build: .
    command: npx nodemon index.js
```

Delete containers

    $ docker container prune

Delete images

    $ docker image prune

Remove networks

    $ docker network prune

Delete volumes

    $ docker volume prune

Delete containers, images, volumes and networks

    $ docker system prune

Delete all containers

    $ docker rm -f $(docker ps -aq)

Delete all images

    $ docker rmi -f $(docker image ls -q)

See the resources of the running containers

    $ docker stats

Assign a memory limit to a container

    $ docker run --memory <1g | 4m> <image name>

Kill a docker container

    $ docker kill <container name>