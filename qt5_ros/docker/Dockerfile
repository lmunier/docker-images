# Handle ros distro
ARG ROS_DISTRO=noetic
ARG ROS_IMAGE=${ROS_DISTRO}-desktop-full

FROM osrf/ros:${ROS_IMAGE} as ros-ws

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

# Installation of Qt5.12
RUN apt update --fix-missing && apt upgrade -y && apt clean
RUN apt -y install \
    build-essential \
    qt5-default \
    python3 \
    python3-pip \
    qtcreator

RUN python3 -m pip install --upgrade pip
RUN python3 -m pip install \
    pyside2==5.15.2

USER ${USER}
CMD [ "bash" ]
