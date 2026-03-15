# syntax=docker/dockerfile:1.7
ARG ZEPHYR_SDK_VERSION=1.0.0
ARG ZEPHYR_SDK_INSTALL_DIR=/opt/toolchains/zephyr-sdk-${ZEPHYR_SDK_VERSION}
ARG BASE_IMAGE="zephyr:base-${ZEPHYR_SDK_VERSION}SDK"

FROM ${BASE_IMAGE}

# OS dependencies and Zephyr SDK posix setup

ARG ZEPHYR_SDK_VERSION=1.0.0
ARG ZEPHYR_SDK_INSTALL_DIR=/opt/toolchains/zephyr-sdk-${ZEPHYR_SDK_VERSION}

RUN --mount=type=cache,target=/var/cache/apt,sharing=locked \
  --mount=type=cache,target=/var/lib/apt/lists,sharing=locked \
  apt-get -y update \
  && apt-get -y install --no-install-recommends \
  gcc-multilib \
  make \
  wget \
  && ${ZEPHYR_SDK_INSTALL_DIR}/setup.sh -c \
  && apt-get remove -y --purge \
  wget \
  && apt-get autoremove -y