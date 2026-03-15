# syntax=docker/dockerfile:1.7
ARG ZEPHYR_SDK_VERSION=1.0.0
ARG ZEPHYR_SDK_INSTALL_DIR=/opt/toolchains/zephyr-sdk-${ZEPHYR_SDK_VERSION}
ARG ZEPHYR_SDK_TOOLCHAINS="-t arm-zephyr-eabi"
ARG BASE_IMAGE="zephyr:base-${ZEPHYR_SDK_VERSION}SDK"

FROM ${BASE_IMAGE}

# Target architecture SDK

ARG ZEPHYR_SDK_INSTALL_DIR
ARG ZEPHYR_SDK_TOOLCHAINS

RUN --mount=type=cache,target=/var/cache/apt,sharing=locked \
  --mount=type=cache,target=/var/lib/apt/lists,sharing=locked \
  apt-get -y update \
  && apt-get -y install --no-install-recommends \
  xz-utils \
  wget \
  && ${ZEPHYR_SDK_INSTALL_DIR}/setup.sh -c ${ZEPHYR_SDK_TOOLCHAINS} \
  && apt-get remove -y --purge \
  wget \
  xz-utils \
  && apt-get autoremove -y \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
