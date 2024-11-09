# 使用 Ubuntu 20.04 作为基础镜像
FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

ENV LANG=zh_CN.UTF-8
ENV LC_ALL=zh_CN.UTF-8
ENV LANGUAGE=zh_CN.UTF-8

WORKDIR /tmp

RUN sed -i "s@http://deb.debian.org@http://mirrors.aliyun.com@g" /etc/apt/sources.list && \
    apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y --no-install-recommends vim git zip unzip tar xz-utils \
    cmake make git openjdk-11-jdk ssh clang-format-12 gcc g++ gdb \
    curl wget ncftp net-tools build-essential doxygen autoconf libtool linux-tools-common linux-tools-generic \
    x11-apps tree python python3 python3-pip iputils-ping libglew-dev libgtk-3-dev \
    automake tk less language-pack-zh-hans libeigen3-dev libceres-dev libpcl-dev \
    x11-common x11-session-utils x11-utils x11-xfs-utils x11-xkb-utils x11-xserver-utils fonts-wqy-zenhei && \
    apt-get install -y gnupg && \
    apt-get install -y libopencv-dev &&\
    apt-get update &&\
    rm -rf /tmp/*  /var/lib/apt/lists/*

# 设置工作目录
WORKDIR /workspace

# 设置默认启动命令（可选）
CMD ["/bin/bash"]
