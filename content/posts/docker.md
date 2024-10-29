+++
title = 'Docker (WIP)'
date = 2023-12-03T15:02:46+05:45
draft = false
+++

#### Docker

> A container platform that allows you to build, test & deploy applications quickly

#### Dockerfile

> A set of instructions for creating an image

#### Image

> A packaged application and its dependencies

#### Container

> A running instance of that image executing the application in an isolated environment

```bash
# Pull docker image from DockerHub
docker pull IMAGE_NAME:TAG

# List all the images
docker images

# Run docker image
docker run IMAGE_NAME:TAG
docker run ubuntu:latest

# Runs container in the background
docker run -d node:latest

# Run and interact with the container
docker run -it node

# Here,
# -d mean detached mode : run in the background
# -p 4000:3000 means map the port 4000 of your host machine
# to the port 3000 inside the container
docker run -d -p 4000:3000 --name acme-api acme-api:latest

sudo docker run -d -p 27017:27017 7ee26c8012da

# List all the running containers
docker ps

# List containers including the stopped ones
docker ps -a

# Remove docker container
sudo docker rm CONTAINER_NAME_or_ID

# Remove all the docker images
sudo docker rmi $(sudo docker images -q)
```

#### This is a simple example of Dockerfile for an express API

> Here, RUN is used to specify commands which runs while the docker image is being built
>
> While, CMD is used to specify commands which runs while the docker container is run

```dockerfile
FROM node:17-alpine

WORKDIR /app

COPY . .

RUN npm install

EXPOSE 3000

CMD ["node","app.js"]
```

```bash
# Build the docker image from docker file
# . specifies the relative path to the docker file form the terminal
docker build -t TAGNAME .

docker build -t myapp .

# Lists the built images
docker images

# Run the built image
docker run myapp

# Specify the name of the container

> Using this does not expose the port to the host machine
docker run --name myapp_c1 myapp

> Hence, we use 
> Here, -d which runs container in the background
> -p is used to map the port 4000 of your host machine
sudo docker run --name myapp_c1 -p 3000:3000 -d myapp

sudo docker run -d -p 27017:27017 7ee26c8012da
# Stop docker container
sudo docker stop CONTAINER_NAME_or_ID

# Stops all the containers
sudo docker stop $(sudo docker ps -q)

```