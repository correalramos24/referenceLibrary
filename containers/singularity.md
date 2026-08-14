# Singularity

Containaritzation to build an entire software stack into one file, making the portability between machines trivial. 

The Singularity allows:
* BYOE (Bring Your Own environment)
* Reproducibility
* Portability between machines

Singularity is based in images (.sif files). Behind the scenes, Docker is used to build the images and containers.

Singularity (v3 & above) is written in Go.

## Create images
Images can be assemble from existig containers (online or local), from a Docker image or from singularity definition files. The container is a singularity image file (SIF)

### Build command


### Sandboxes
In this case, a special chroot directory is generated, whit writting rights. You can commit the changes and generate the sif file.

### Singularity definition files


## Execute containers

### Environment
