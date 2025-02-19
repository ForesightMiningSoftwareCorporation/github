FROM ubuntu:focal

WORKDIR /usr/src/
ARG RUST_VERSION=1.82
ARG OPENSSL_VERSION=1.1.1m

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
  apt-get install \
  -yq --no-install-recommends \
  build-essential \
  cmake \
  curl \
  gfortran \
  git \
  gnupg2 \
  gobject-introspection \
  libasound2-dev \
  libatk1.0-0 \
  libcairo-gobject2 \
  libexpat1-dev \
  libfontconfig-dev \
  libfreetype-dev \
  libgdk-pixbuf2.0-0 \
  libglib2.0-0 \
  libgtk-3-dev \
  libmkl-full-dev \
  libomp-8-dev \
  libpango-1.0-0 \
  libssl-dev \
  libudev-dev \
  libxcb-composite0-dev \
  lsb-release \
  musl-dev \
  musl-tools \
  openssh-client \
  pkg-config \
  software-properties-common \
  tzdata \
  wget

# Static linking for C++ code
RUN ln -s "/usr/bin/g++" "/usr/bin/musl-g++"

# install Rust
RUN curl https://sh.rustup.rs -sSf | \
  sh -s -- --default-toolchain $RUST_VERSION -y -t x86_64-unknown-linux-musl --profile minimal

ENV PATH=/root/.cargo/bin:$PATH
RUN rustup target add x86_64-unknown-linux-musl

# Install OpenSSl
COPY build_openssl_ubuntu.sh build_openssl_ubuntu.sh
RUN ./build_openssl_ubuntu.sh
