+++
title = 'Docker (WIP)'
date = 2023-12-03T15:02:46+05:45
draft = false
+++

### Docker

> A container platform that allows you to build, test & deploy applications quickly

### Dockerfile

> A set of instructions for creating an image

### Image

> A packaged application and its dependencies

### Container

> A running instance of that image executing the application in an isolated environment

```bash
# Pull docker image from DockerHub
docker pull IMAGE_NAME:TAG

# Run docker image
docker run IMAGE_NAME:TAG
docker run ubuntu:latest

# Runs container in the background
docker run -d node:latest

# List all the images
docker images

# List all the running containers
docker ps

# List containers including the stopped ones
docker ps -a

# Run and interact with the container
docker run -it node

# Build the docker image from docker file
# . specifies the relative path to the docker file form the terminal
docker build -t TAGNAME .
docker build -t myapp .

# Here,
# -d mean detached mode : run in the background
# -p 4000:3000 means map the port 4000 of your host machine
# to the port 3000 inside the container
docker run -d -p 4000:3000 --name acme-api acme-api:latest

sudo docker run -d -p 27017:27017 7ee26c8012da

# Stop docker container
sudo docker stop CONTAINER_NAME_or_ID

# Stops all the containers
sudo docker stop $(sudo docker ps -q)

# Remove docker container
sudo docker rm CONTAINER_NAME_or_ID
```
