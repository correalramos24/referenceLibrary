# Docker
- [Docker](#docker)
  - [Introduction](#introduction)
  - [Docker installation](#docker-installation)
  - [Images and containers](#images-and-containers)
  - [Dockerfiles](#dockerfiles)
- [docker-compose](#docker-compose)
  - [Secret files](#secret-files)


## Introduction
* Docker allows to use always the same environment (sandbox)
* Different from a VM, all the containers have the same OS at the end.
  * A container with a Linux app, can only run with a linux kernel
* Docker runs an application image within a container in the host.
* A docker container needs to be *removable*, in other words the important data needs to be saved outside (with a volume).

## Docker installation

Follow the steps from the official webpage.

For user containers, is required super-user powers; to avoid this, use:
```bash
sudo groupadd docker
sudo usermod -aG docker $USER
#logout and login
```

## Images and containers

Docker runs a container using an image, that can be obtained in two ways:
1. From a *Dockerfile*: A text file where you can custom your image with `docker build`.
2. From an image registry ([dockerhub](https://hub.docker.com)): Other user generates an image that we can download with `docker pull <img>` (this command is inside docker run also).

> Some insights of the images:
> * All the images have a tag, for different target host, versions, etc ...
> * An image is a set of layers into the top of another image, called base image.

For running an image in a container, use `docker run <img:tag>`. If Docker doesn't find the image locally, it will pull the image from the registry. 

>Some insights of the containers
>* All the containers have an unique container id and a unique name.
>* The stdout is converted automatically by Docker into the container log.

Here there all the useful commands related with images and containers:

| Command                        | Explanation                                                  |
| ------------------------------ | ------------------------------------------------------------ |
| `docker run <img:tag>`         | Runs a container with the image *img* and the specified *tag* |
| `docker pull <img:tag>`        | Download the image specified.                                |
| `docker images`                | List all the downloaded images on your system                |
| `docker ps`                    | List all the running containers (with -a lists all)          |
| `docker start <id> [<id> ...]` | Start one or more stopped containers (detached by default, -a for attach) |
| `docker stop <id> [<id> ...]`  | Stops one or more containers.                                |
| `docker logs <id>`             | See the logs from a container. With -f the output is appended |
| `docker exec <id> <cmd>`       | Execute a command in a running container                     |
| `docker exec -it <id> <cmd>    | Execute the command interactive & with a pseudo-tty (open a shell) |

> All the id can be either container id or the container name.

## Dockerfiles
Used to generate docker images, by default the name of the file must be Dockerfile (with capital D).


# docker-compose

## Secret files
Avoid to have a docker-compose file with tokens, keys and other critical information. You just define your secrets 
that point towards a plain text file in the directory of your `docker-compose.yaml`.

