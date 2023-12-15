FROM debian:stable-slim

ARG ZEPHYR_SDK_VERSION=0.16.4
ARG ZEPHYR_SDK_INSTALL_DIR=/opt/toolchains/zephyr-sdk-${ZEPHYR_SDK_VERSION}

# OS dependencies and packages

RUN \
  apt-get -y update \
  && apt-get -y install --no-install-recommends \
  ca-certificates \
  cmake \
  device-tree-compiler \
  git \
  ninja-build \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Zephyr SDK

RUN \
  export sdk_file_name="zephyr-sdk-${ZEPHYR_SDK_VERSION}_linux-$(uname -m)_minimal.tar.xz" \
  && apt-get -y update \
  && apt-get -y install --no-install-recommends \
  wget \
  xz-utils \
  && wget -q "https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v${ZEPHYR_SDK_VERSION}/${sdk_file_name}" \
  && mkdir -p ${ZEPHYR_SDK_INSTALL_DIR} \
  && tar -xvf ${sdk_file_name} -C ${ZEPHYR_SDK_INSTALL_DIR} --strip-components=1 \
  && ${ZEPHYR_SDK_INSTALL_DIR}/setup.sh -c \
  && rm ${sdk_file_name} \
  && apt-get remove -y --purge \
  wget \
  xz-utils \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Python

ENV VIRTUAL_ENV=/opt/venv
RUN \
  apt-get -y update \
  && apt-get -y install --no-install-recommends \
  python3 \
  python3-pip \
  python3-venv \
  && python3 -m venv $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

# West

RUN pip install --no-cache-dir wheel west