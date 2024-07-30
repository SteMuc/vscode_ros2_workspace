FROM osrf/ros:humble-desktop-full

# Set environment variables
ENV color_prompt=yes
ENV QT_X11_NO_MITSHM=1
ENV DRI_NAME=card1
ENV NVIDIA_VISIBLE_DEVICES=all
ENV NVIDIA_DRIVER_CAPABILITIES=all
ENV __NV_PRIME_RENDER_OFFLOAD=1
ENV __GLX_VENDOR_LIBRARY_NAME=nvidia

# Set up display
ENV DISPLAY=$DISPLAY
ENV TERM=$TERM

ARG USERNAME=ros
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    #
    # [Optional] Add sudo support. Omit if you don't need to install software after connecting.
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y python3-pip
ENV SHELL /bin/bash

# Install ROS dependencies
RUN apt-get update \
	&& DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
	ros-dev-tools \
	stm32flash \
	libeigen3-dev \
    libignition-gazebo6-dev \
    libpoco-dev \
    ros-$ROS_DISTRO-ackermann-msgs \
    ros-$ROS_DISTRO-ament-cmake \
    ros-$ROS_DISTRO-ament-cmake-clang-format \
    ros-$ROS_DISTRO-ament-cmake-clang-tidy \
    ros-$ROS_DISTRO-control-msgs \
    ros-$ROS_DISTRO-control-toolbox \
    ros-$ROS_DISTRO-controller-interface \
    ros-$ROS_DISTRO-controller-manager \
    ros-$ROS_DISTRO-gazebo-ros \
	ros-$ROS_DISTRO-gazebo-ros-pkgs \
    ros-$ROS_DISTRO-generate-parameter-library \
    ros-$ROS_DISTRO-geometry-msgs \
    ros-$ROS_DISTRO-hardware-interface \
    ros-$ROS_DISTRO-hardware-interface-testing \
    ros-$ROS_DISTRO-joint-state-broadcaster \
    ros-$ROS_DISTRO-joint-state-publisher-gui \
    ros-$ROS_DISTRO-launch-testing \
    ros-$ROS_DISTRO-moveit \
    ros-$ROS_DISTRO-realtime-tools \
    ros-$ROS_DISTRO-ros2-control \
    ros-$ROS_DISTRO-ros2-control-test-assets \
    ros-$ROS_DISTRO-ros2-controllers \
    ros-$ROS_DISTRO-sensor-msgs \
    ros-$ROS_DISTRO-xacro \
    ros-$ROS_DISTRO-ros-gz \
	ros-$ROS_DISTRO-navigation2 \
	ros-$ROS_DISTRO-slam-toolbox \
	ros-$ROS_DISTRO-nav2-bringup \
	ros-$ROS_DISTRO-ign-ros2-control \
	ros-$ROS_DISTRO-robot-localization \
	ros-${ROS_DISTRO}-ros-ign-bridge \
	ros-${ROS_DISTRO}-rmw-cyclonedds-cpp\
	&& apt-get clean -q -y \
	&& apt-get autoremove -q -y \
	&& rm -rf /var/lib/apt/lists/*

RUN echo "export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp" >> /home/ros/.bashrc \
    && echo "source /opt/ros/humble/setup.bash" >> /home/ros/.bashrc 

USER $USERNAME
CMD ["/bin/bash"]


