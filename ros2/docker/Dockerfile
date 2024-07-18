# Handle ros distro
ARG ROS_DISTRO=humble
ARG ROS_IMAGE=${ROS_DISTRO}-desktop-full-jammy

FROM osrf/ros:${ROS_IMAGE} as ros-ws

ARG ROS_DISTRO
ARG USER=root
ARG HOME=/home/${USER}

ENV DEBIAN_FRONTEND noninteractive
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES video,compute,utility

# create and configure a new user
ARG UID=1000
ARG GID=1000
RUN useradd -m ${USER} && echo "${USER}:${USER}passwd" | chpasswd && adduser ${USER} sudo
RUN usermod -a -G dialout ${USER}

WORKDIR ${HOME}
RUN chown -R ${USER}:${USER} ${HOME}

# Install catkin tools
# RUN apt update --fix-missing && apt upgrade -y && apt clean
# RUN apt install -y wget
# RUN sh -c \
#     'echo "deb http://packages.ros.org/ros/ubuntu `lsb_release -sc` main" \
#     > /etc/apt/sources.list.d/ros-latest.list'

# RUN wget http://packages.ros.org/ros.key -O - | apt-key add -
RUN apt update --fix-missing && apt upgrade -y && apt clean
RUN apt install -y \
    python3-colcon-common-extensions \
    python3-osrf-pycommon

# Install ubuntu libraries
RUN apt update --fix-missing && apt upgrade -y && apt clean
RUN apt install -y \
    git \
    python3 \
    ros-${ROS_DISTRO}-moveit \
    python3-pip

# Install urdf_to_dh parameters dependencies
RUN pip3 install --upgrade pip
RUN pip3 install \
    pandas \
    anytree \
    tabulate

WORKDIR ${HOME}/ros2_ws/src
RUN chown -R ${USER}:${USER} ${HOME}

RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc

CMD [ "bash" ]