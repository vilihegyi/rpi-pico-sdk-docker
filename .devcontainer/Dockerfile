FROM alpine:3.16.2

# Install required packages
RUN apk update && \
    apk upgrade && \
    apk add git \
            python3 \
            py3-pip \
            cmake \
            build-base \
            libusb-dev \
            bsd-compat-headers \
            newlib-arm-none-eabi \
            gcc-arm-none-eabi

# Raspberry Pi Pico C/C++ SDK --version 1.4.0
ARG SDK_PATH=/usr/share/pico_sdk
RUN git clone --depth 1 --branch 1.4.0 https://github.com/raspberrypi/pico-sdk $SDK_PATH && \
    cd $SDK_PATH && \
    git submodule update --init

# Set the Environment variable to the SDK_PATH
ENV PICO_SDK_PATH=$SDK_PATH

# Picotool installation
RUN git clone --depth 1 --branch 1.1.0 https://github.com/raspberrypi/picotool.git /home/picotool && \
    cd /home/picotool && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make -j$(nproc) && \
    cp /home/picotool/build/picotool /bin/picotool && \
    rm -rf /home/picotool
