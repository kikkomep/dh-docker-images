# docker-libs

Docker images to develop and run software based on the [EDDL](https://github.com/deephealthproject/eddl) and [ECVL](https://github.com/deephealthproject/ecvl) libraries and their Python wrappers ([PyEDDL](https://github.com/deephealthproject/pyeddl) and [PyECVL](https://github.com/deephealthproject/pycvl)).

## Description

The `docker-libs` repository allows users to build and publish on a registry (e.g., DockerHub) Docker images containing the [EDDL](https://github.com/deephealthproject/eddl) and [ECVL](https://github.com/deephealthproject/ecvl) libraries and their Python wrappers, [PyEDDL](https://github.com/deephealthproject/pyeddl) and [PyECVL](https://github.com/deephealthproject/pycvl). All the images are based on the [NVIDIA Container Toolkit](https://github.com/NVIDIA/nvidia-docker) and the EDDL and ECVL libraries are configured to leverage NVIDIA GPUs.

Precompiled images are published on [DockerHub](https://hub.docker.com/u/dhealth).

The available images are:

* **[`dhealth/libs`](https://hub.docker.com/r/dhealth/libs)** contains an installation of the EDDL and ECVL libraries
* **[`dhealth/libs-toolkit`](https://hub.docker.com/r/dhealth/libs-toolkit)** contains an installation of the EDDL and ECVL libraries, the source code of two libraries and all the development tools (compilers, libraries, etc.) you need to compile them

* **[`dhealth/pylibs`](https://hub.docker.com/r/dhealth/pylibs)** extends the `libs` image with the PyEDDL and PyECVL libraries
* **[`dhealth/pylibs-toolkit`](https://hub.docker.com/r/dhealth/pylibs-toolkit)** extends the `libs-toolkit` image with the PyEDDL and PyECVL libraries

## Example usage

Open a shell in a container with access to the DeepHealth libraries:

```bash
docker run -it --rm dhealth/libs /bin/bash
```

Open a shell to compile your local project:

```bash
docker run -it -u $(id -u) -v $(pwd):/tests --rm dhealth/libs-toolkit:0.1.1 /bin/bash
```



## How to build

A `Makefile` allows to easily compile and publish the Docker images. Type `make help` to see the available `Makefile` targets, i.e.:

```bash
help                           Show help
build                          Build and tag all Docker images
build_libs                     Build and tag 'libs' image
build_libs_toolkit             Build and tag 'libs-toolkit' image
build_pylibs                   Build and tag 'pylibs' image
build_pylibs_toolkit           Build and tag 'pylibs-toolkit' image
push                           Push all built images
push_libs                      Push 'libs' images
push_libs_toolkit              Push 'libs-toolkit' images
push_pylibs                    Push 'pylibs' images
push_pylibs_toolkit            Push 'pylibs-toolkit' images
publish                        Publish all built images to a Docker Registry (e.g., DockerHub)
publish_libs                   Publish 'libs' images
publish_libs_toolkit           Publish 'libs-toolkit' images
publish_pylibs                 Publish 'pylibs' images
publish_pylibs_toolkit         Publish 'pylibs-toolkit' images
repo-login                     Login to the Docker Registry
version                        Output the current version of this Makefile
```

Edit the file `settings.sh` to customize your images (name, software revision, Docker registry, etc.)
