# If needed to run docker without using sudo :
# https://stackoverflow.com/questions/72846258/docker-deamon-dont-work-without-sudo-with-sudo-all-services-is-working
# unset DOCKER_HOST
# docker context use default

# To build this image : sudo docker build --build-arg DOCKER_USER=$USER NB_CPU_CORES=nproc -t docker_qt .

FROM ubuntu:22.04

ARG USER=root
ARG HOME=/home/${USER}

ENV DEBIAN_FRONTEND noninteractive
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES video,compute,utility

# create and configure a new user
ARG UID=1000
ARG GID=1000
RUN addgroup --gid ${GID} ${USER}
RUN adduser --uid ${UID} --gid ${GID} ${USER} && yes | passwd ${USER}
RUN usermod -a -G dialout ${USER}

WORKDIR ${HOME}
RUN chown -R ${USER}:${USER} ${HOME}

# Installation of Qt
RUN apt update --fix-missing && apt upgrade -y && apt clean
RUN apt -y install \
    build-essential \
    qt6-base-dev \
    qt6-base-dev-tools \
    qt6-base-private-dev \
    qmake6 \
    qt6-image-formats-plugins \
    linguist-qt6 \
    qt6-tools-dev \
    qt6-l10n-tools \
    qt6-tools-dev-tools \
    libopengl-dev \
    libegl1-mesa-dev \
    libegl1-mesa \
    libegl-mesa0

RUN apt -y install \
    git \
    python3 \
    python3-pip \
    qtcreator

USER ${USER}
CMD [ "bash" ]
