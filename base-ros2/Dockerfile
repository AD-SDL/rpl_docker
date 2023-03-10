FROM waggle/plugin-base:1.1.1-base
LABEL description="Waggle base image containing ROS2 foxy."
LABEL maintainer="Sage Waggle Team <sage-waggle@sagecontinuum.org>"
LABEL url="https://github.com/waggle-sensor/plugin-base-images/tree/master/base-ros2"

ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8
ENV ROS_DISTRO=foxy
ENV ROS_ROOT=/opt/ros/${ROS_DISTRO}
ENV ROS_PYTHON_VERSION=3
ENV ROS_WS=/root/overlay_ws

# install system packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    gnupg2 \
    lsb-release \
    net-tools \
    iputils-ping \
    && rm -rf /var/lib/apt/lists/*

# install ros2 foxy-base and build packages
RUN curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add - \
    && sh -c 'echo "deb [arch=$(dpkg --print-architecture)] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2-latest.list' \
    && apt-get update \
    && apt-get install -y ros-foxy-ros-base \
    && apt-get install -y --no-install-recommends \
        python3-colcon-common-extensions \
        build-essential \
        python3-vcstool \
    && rm -rf /var/lib/apt/lists/*

# sourcing underlay in .bashrc
RUN echo "source $ROS_ROOT/setup.bash" >> ~/.bashrc

# creating and sourcing an empty overlay where other ros2 packages will be added
RUN mkdir -p $ROS_WS/src/
WORKDIR $ROS_WS
RUN colcon build --symlink-install \
    && sh -c 'echo "source $ROS_WS/install/setup.bash" >> ~/.bashrc'