FROM nvidia/cuda:12.4.1-base-ubuntu22.04 AS builder

LABEL maintainer="Loïs Postula <lois.postula@foresightmining.com>"
LABEL description="Orica Blast Physics Builder Image"
LABEL version="1.0"

WORKDIR /usr/src/
ARG OPENSSL_VERSION=1.1.1m

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
  apt-get install \
  -yq --no-install-recommends \
  software-properties-common
RUN add-apt-repository ppa:graphics-drivers
RUN apt-get update && \
  apt-get install \
  -yq --no-install-recommends \
  lsb-release \
  libudev-dev \
  libasound2-dev \
  libxcb-composite0-dev \
  openssh-client \
  wget \
  curl \
  gnupg2 \
  tzdata \
  pkg-config \
  libssl-dev \
  musl-dev \
  musl-tools \
  nvidia-cuda-dev \
  libfontconfig-dev \
  build-essential \
  libfreetype-dev \
  libexpat1-dev \
  cmake \
  curl \
  gfortran \
  git \
  protobuf-compiler \
  libgtk-3-dev \
  nvidia-driver-550

# Static linking for C++ code
RUN ln -s "/usr/bin/g++" "/usr/bin/musl-g++"

# install Rust
RUN curl https://sh.rustup.rs -sSf | \
  sh -s -- --default-toolchain stable -y -t x86_64-unknown-linux-musl --profile minimal

ENV PATH=/root/.cargo/bin:$PATH

RUN rustup target add x86_64-unknown-linux-musl

# Install OpenSSl
COPY build_openssl_ubuntu.sh build_openssl_ubuntu.sh
RUN ./build_openssl_ubuntu.sh
