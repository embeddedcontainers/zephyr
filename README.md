# Zephyr Container Images

Develop Zephyr applications using OCI-compatible Docker images.

Currently there are two types of images - a "base" image that contains the core dependencies to build a Zephyr application for a target SDK version and ones for a specific target architecture. Most users will generally interact with the architecture-specific images.

# Getting container images

## Prebuilt Images

The simplest way to start using these container images is with the prebuilt images provided by the project. Images are automatically generated using Github Actions and hosted on the Github Container Registry (GHCR.) GHCR is functionally equivalent to Dockerhub and can be used with standard tools like the Docker CLI.

The project follows an evergreen strategy, meaning only the latest SDK release is maintained. Older SDKs are still hosted but it is recommended to build images locally in order to guarantee the latest packages and security updates are included.

### Using prebuilt images

The full list of prebuilt images can be found [here](https://github.com/embeddedcontainers/zephyr/pkgs/container/zephyr/versions?filters%5Bversion_type%5D=tagged).

For example, the image for the `arm` toolchain can be found [here](https://github.com/embeddedcontainers/zephyr/pkgs/container/zephyr/292819795?tag=arm-0.17.0SDK).

To install via the Docker CLI:

```
$ docker pull ghcr.io/embeddedcontainers/zephyr:arm-0.17.0SDK
```

Use as base image in Dockerfile:

```
FROM ghcr.io/embeddedcontainers/zephyr:arm-0.17.0SDK
```

## Build images locally

Building images locally ensures you can trust the source of the image, as well as allow you to modify the container image configuration.

### Building with Docker CLI

_Build the base image_

```
docker build --build-arg ZEPHYR_SDK_VERSION=0.17.0 -f "./zephyr-base/Dockerfile" -t zephyr:base-0.17.0SDK "./zephyr-base"

```

_To build an image for Arm Cortex-M targets:_


```
docker build --build-arg BASE_IMAGE="zephyr:base-0.17.0SDK" --build-arg ZEPHYR_SDK_TOOLCHAINS="-t arm-zephyr-eabi" -f "./zephyr/Dockerfile" -t zephyr:arm-0.17.0SDK "./zephyr"
```

_To build an image for multiple toolchains:_

```
docker build --build-arg BASE_IMAGE="zephyr:base-0.17.0SDK" --build-arg ZEPHYR_SDK_TOOLCHAINS="-t arm-zephyr-eabi -t x86_64-zephyr-elf" -f "./zephyr/Dockerfile" -t zephyr:arm_x86-0.17.0SDK "./zephyr"
```

_There is a different Dockerfile for Posix target like `native_sim`. To build:_

```
docker build --build-arg BASE_IMAGE="zephyr:base-0.17.0SDK" -f "./zephyr-posix/Dockerfile" -t zephyr:posix-0.17.0SDK "./zephyr-posix"
```
