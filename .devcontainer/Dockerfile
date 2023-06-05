FROM ubuntu:22.04

ARG USERNAME=pi
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME

# Setup prerequisites
RUN apt-get update && apt-get install -y --no-install-recommends \
        ca-certificates \
        git \
        python3 \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/*

# https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf
    # P.7
RUN cd /home/pi/ \
    && mkdir pico \
    && cd pico \
    \
    && git clone https://github.com/raspberrypi/pico-sdk.git --branch master --single-branch --depth=1 \
    && cd pico-sdk \
    && git submodule update --init --recommend-shallow --depth=1 \
    && cd .. \
    && git clone https://github.com/raspberrypi/pico-examples.git --branch master --single-branch --depth=1 \
    \
    # P.8
    && apt-get update \
    && apt-get install -y --no-install-recommends cmake gcc-arm-none-eabi libnewlib-arm-none-eabi build-essential libstdc++-arm-none-eabi-newlib \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/* \
    \
    # P.18
    && apt-get update \
    && apt-get install -y --no-install-recommends minicom \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/* \
    \
    # P.23
    && cd /home/pi/ \
    && apt-get install -y --no-install-recommends automake autoconf build-essential texinfo libtool libftdi-dev libusb-1.0.0-dev \
    && git clone https://github.com/raspberrypi/openocd.git --branch rp2040 --recursive --depth=1 \
    && cd openocd \
    && ./bootstrap \
    && ./configure --enable-ftdi --enable-sysfsgpio --enable-bcm2835gpio \
    && make -j4 \
    && make install

USER $USERNAME
ENV PICO_SDK_PATH="/home/pi/pico/pico-sdk"