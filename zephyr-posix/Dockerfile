ARG ZEPHYR_SDK_VERSION=0.17.0
ARG ZEPHYR_SDK_INSTALL_DIR=/opt/toolchains/zephyr-sdk-${ZEPHYR_SDK_VERSION}
ARG BASE_IMAGE="zephyr:base-${ZEPHYR_SDK_VERSION}SDK"

FROM ${BASE_IMAGE}

# OS dependencies and packages

RUN \
  apt-get -y update \
  && apt-get -y install --no-install-recommends \
  gcc-multilib \
  make \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Zephyr SDK

ARG ZEPHYR_SDK_INSTALL_DIR

RUN \
  apt-get -y update \
  && apt-get -y install --no-install-recommends \
  wget \
  && ${ZEPHYR_SDK_INSTALL_DIR}/setup.sh -c \
  && apt-get remove -y --purge \
  wget \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*