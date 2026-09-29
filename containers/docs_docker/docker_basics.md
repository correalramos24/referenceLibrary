# Docker

- [Docker](#docker)
  - [Introduction](#introduction)
  - [Docker installation](#docker-installation)
  - [Images and containers basics](#images-and-containers-basics)
    - [Images useful commands](#images-useful-commands)
    - [Containers useful commands](#containers-useful-commands)
  - [More on running containers](#more-on-running-containers)
    - [docker run options](#docker-run-options)
    - [Container volumes](#container-volumes)
  - [Container networking](#container-networking)
  - [Multi-containers architecture](#multi-containers-architecture)


## Introduction
* Docker allows to use always the same environment (sandbox)
* Different from a VM, all the containers have the same OS at the end.
  * A container with a Linux app, can only run with a linux kernel
* Docker runs an application image within a container in the host.
* A docker container needs to be *removable*, in other words the important data needs to be saved outside (with a volume).
* At execution time, you can ask with tab key for auto-complete the commands (or display the possible commands)

## Docker installation

Follow the steps from the official webpage.

For user containers, is required super-user powers; to avoid this, use:
```bash
sudo groupadd docker
sudo usermod -aG docker $USER
#logout and login
```

## Images and containers basics

Docker runs a container using an image, that can be obtained in two ways:
1. From a *Dockerfile*: A text file where you can custom your image with `docker build`.
2. From an image registry ([dockerhub](https://hub.docker.com)): Other user generates an image that we can download with `docker pull <img>` (this command is inside docker run also).

> Some insights of the images:
> * All the images have a tag, for different target host, versions, etc ...
> * An image is a set of layers into the top of another image, called base image.

For running an image in a container, use `docker run <img:tag>`. If Docker doesn't find the image locally, it will pull the image from the registry. 

>Some insights of the containers:
>* All the containers have an unique container id  (hash value) and a unique name. You can execute commands either using the id or the unique name.
>* The stdout is converted automatically by Docker into the container log.

| Command                      | Explanation                                                  |
| ---------------------------- | ------------------------------------------------------------ |
| `docker build`               | Create a image from the *Dockerfile* at PWD, with `-f` can use another file |
| `docker run <img:tag>`       | Runs a new container with the image *img* and the specified *tag* |
| `docker run -it <img:tag>`   | Runs a new container interactive                             |
| `docker exec <id> <cmd>`     | Execute a command in a running container                     |
| `docker exec -it <id> <cmd>` | Execute the command interactive & with a pseudo-tty (open a shell) |

### Images useful commands

The images can be build and managed (removed, tagged, etc) via different commands. The useful commands are:

| Command                                  | Explanation                                                  |
| ---------------------------------------- | ------------------------------------------------------------ |
| `docker images`                          | List all the downloaded images on your system (short for `docker image ls`) |
| `docker pull <img:tag>`                  | Download the image specified                                 |
| `docker push <img:tag>`                  | Upload an image to a registry.                               |
| `docker tag sourceImg:tag targetImg:tag` | Create a tag image from a source image. Basically renames an image |
| `docker save`                            | Save an image via STDOUT                                     |
| `docker prune`                           | Remove unused images                                         |
| `docker rmi <img:tag> [img:tag]`         | Remove one or more images (can't be used by a container). Alias for `docker image rm` |

Commands for one specific image are within `docker image ...` and the commands for all the images on the host is `docker images ...`.

### Containers useful commands

All the container-related command can be access using `docker container <cmd>`command line. There are some alias also for skip write container. The most useful:

| Command                        | Explanation                                                  |
| ------------------------------ | ------------------------------------------------------------ |
| `docker ps`                    | List all the running containers (with -a lists all)          |
| `docker container ls`          | Same as `docker ps`                                          |
| `docker stop <id> [<id> ...]`  | Stop one or more containers (Sends *SIGTERM*)                |
| `docker start <id> [<id> ...]` | Re-start one or more container                               |
| `docker pause <id> [<id> ...]` | Pause one or more containers (Sends *SIGSTOP*)               |
| `docker unpause <id> [<id>..]` | (Sends *SINGCONT*)                                           |
| `docker kill <id> [<id> ...]`  | Kill one or more containers (Sends *SIGKILL*)                |
| `docker logs <id>`             | See the logs from a container. With -f the output is appended |
| `docker container prune`       | Remove all stopped container                                 |
| `docker rm <id> [<id> ...]`    | Remove one or more containers                                |
| `docker stats [<id> <id> ...]` | See stats of the container, in running state by default      |
| `docker top <id>`              | See top process of a container.                              |

> All the containers id can be either container id or the container name.

## More on running containers

So far, we can run containers and manage with the commands above but there are more things about running the containers.

### docker run options
!TODO

### Container volumes

![image](https://github.com/correalramos24/Docker/assets/17430554/a177dd33-3e67-44fb-9ee4-9e198ddde578)

This is the unique way to share files between the container & the host and to add data persistence to a container (remember, the containers can be discarded). You can also copy data from/back a container but is considered a bad practice (again because the container can be discarded at any moment).

To use volumes in a container, is required to specify the volume on the container creation (`docker exec`), using either `-v` or `--volume` with the following syntax:
````bash
-v, --volume=[absolute-host-src/volume_name:]container-dest[:<options>]
````
> You can directly mount a directory, using an absolute path
> The options define the permission (rw,ro).
> With `docker volume create <vol_name>` the docker engine creates an empty volume
> If a volume name isn't defined, the docker engine generates a new volume
> The volumes are stored at `/var/lib/docker/volumes/` on Linux.

## Container networking



## Multi-containers architecture
