# Zephyr Container Images

Develop Zephyr applications using OCI-compatible Docker images.

Currently there are two types of images - a "base" image that contains the core dependencies to build a Zephyr application for a target SDK version and ones for a specific target architecture. Most users will generally interact with the architecture-specific images.

# Getting container images

## Build images locally

Building images locally ensures you can trust the source of the image, as well as allow you to modify the container image configuration.

### Building with Docker CLI

_Build the base image_

```
docker build --build-arg ZEPHYR_SDK_VERSION=0.16.4 -f "./zephyr-base/Dockerfile" -t zephyr:base-0.16.4SDK "./zephyr-base"

```

_To build an image for Arm Cortex-M targets:_


```
docker build --build-arg BASE_IMAGE="zephyr:base-0.16.4SDK" --build-arg ZEPHYR_SDK_TOOLCHAINS="-t arm-zephyr-eabi" -f "./zephyr/Dockerfile" -t zephyr:arm-0.16.4SDK "./zephyr"
```

_To build an image for multiple toolchains:_

```
docker build --build-arg BASE_IMAGE="zephyr:base-0.16.4SDK" --build-arg ZEPHYR_SDK_TOOLCHAINS="-t arm-zephyr-eabi -t x86_64-zephyr-elf" -f "./zephyr/Dockerfile" -t zephyr:arm_x86-0.16.4SDK "./zephyr"
```