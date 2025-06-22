FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Install basic packages
RUN apt update && apt install -y \
    curl \
    gnupg2 \
    lsb-release \
    software-properties-common \
    locales \
    sudo \
    git \
    && locale-gen en_US en_US.UTF-8 \
    && update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 \
    && rm -rf /var/lib/apt/lists/*

# Add vscode user with sudo permissions (needed by GitHub Codespaces)
ARG USERNAME=vscode
RUN useradd -m -s /bin/bash $USERNAME && \
    echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/$USERNAME


RUN apt update && apt install -y curl gnupg2 lsb-release software-properties-common && \
    curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key | apt-key add - && \
    sh -c 'echo "deb http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2-latest.list' && \
    apt update && \
    apt install -y ros-humble-ros-base && \
    echo "source /opt/ros/humble/setup.bash" >> /home/vscode/.bashrc
