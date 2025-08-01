FROM ubuntu:24.04

# configure timezone
ENV TZ=Asia/Taipei
RUN apt-get update \
    && apt-get install --no-install-recommends tzdata \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone \
    && dpkg-reconfigure -f noninteractive tzdata

# basic setup
ARG BASIC="wget libfontconfig"
RUN sed -i "s/archive.ubuntu.com/mirror.twds.com.tw/g" /etc/apt/sources.list.d/ubuntu.sources \
    && apt-get update && apt-get upgrade -y \
    && apt-get install -y ${BASIC} \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# install Quarto binary
RUN wget https://github.com/quarto-dev/quarto-cli/releases/download/v1.7.32/quarto-1.7.32-linux-amd64.deb \
    && yes | dpkg -i quarto-1.7.32-linux-amd64.deb \
    && rm quarto-1.7.32-linux-amd64.deb \
    && yes | quarto install tinytex
