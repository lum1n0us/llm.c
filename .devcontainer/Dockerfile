FROM mcr.microsoft.com/devcontainers/base:jammy

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
   && apt upgrade -y

RUN apt install -y --no-install-recommends bat build-essential file software-properties-common tree wget

####################
# Install wasi-sdk
####################
ARG WASI_SDK_VER=wasi-sdk-22
WORKDIR /opt
RUN wget https://github.com/WebAssembly/wasi-sdk/releases/download/${WASI_SDK_VER}/${WASI_SDK_VER}.0-linux.tar.gz
RUN tar xf ${WASI_SDK_VER}.0-linux.tar.gz && rm ${WASI_SDK_VER}.0-linux.tar.gz

####################
# Re-Install cmake > 3.23
####################
ARG CMAKE_VER=3.29.2
RUN apt purge --auto-remove -y cmake
WORKDIR /tmp
RUN wget https://github.com/Kitware/CMake/releases/download/v${CMAKE_VER}/cmake-${CMAKE_VER}-linux-x86_64.sh
RUN chmod +x cmake-${CMAKE_VER}-linux-x86_64.sh \
  && ./cmake-${CMAKE_VER}-linux-x86_64.sh --skip-license --prefix=/usr/local \
  && rm cmake-${CMAKE_VER}-linux-x86_64.sh

####################
# Install pip
####################
RUN apt install -y python3-pip \
  && pip3 install --upgrade pip

####################
# Install wamr
####################
ARG WAMR_VER=2.0.0
WORKDIR /opt
RUN mkdir wamr-${WAMR_VER} \
  && cd wamr-${WAMR_VER} \
  && wget https://github.com/bytecodealliance/wasm-micro-runtime/releases/download/WAMR-${WAMR_VER}/wamrc-${WAMR_VER}-x86_64-ubuntu-22.04.tar.gz \
  && wget https://github.com/bytecodealliance/wasm-micro-runtime/releases/download/WAMR-${WAMR_VER}/iwasm-${WAMR_VER}-x86_64-ubuntu-22.04.tar.gz \
  && tar xfv wamrc-${WAMR_VER}-x86_64-ubuntu-22.04.tar.gz \
  && tar xfv iwasm-${WAMR_VER}-x86_64-ubuntu-22.04.tar.gz \
  && rm wamrc-${WAMR_VER}-x86_64-ubuntu-22.04.tar.gz \
  && rm iwasm-${WAMR_VER}-x86_64-ubuntu-22.04.tar.gz
