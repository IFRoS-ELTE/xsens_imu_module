# Use the ROS Noetic base image on Ubuntu Focal
FROM ros:noetic-ros-base-focal

# Set the ROS distribution environment variable
ENV ROS_DISTRO=noetic

# Set the ROS root directory
ENV ROS_ROOT=/opt/ros/${ROS_DISTRO}

# Set DEBIAN_FRONTEND to noninteractive to avoid interactive prompts during installation
ENV DEBIAN_FRONTEND=noninteractive

# Install essential tools, libraries, and ROS dependencies
RUN apt-get update && apt-get install --no-install-recommends -y \
        build-essential \
        git \
        python3-catkin-tools \
        python3-pip \
        nano \
        curl \
        wget \
        libgl1-mesa-dev \
        libglu1-mesa-dev \
        x11-apps \
        ros-noetic-rviz \
        ros-noetic-rqt \
        ros-noetic-rqt-common-plugins \
        sharutils \
        ros-noetic-diagnostic-updater \
    && apt-get clean \ 
    && rm -rf /var/lib/apt/lists/*

# Download and install the Xsens MT Software Suite
# IMPORTANT: This downloads the MT Software Suite for Linux x86. If you want to deploy this on the Pomona robot, you will need the ARM. -> research how you can get it or use the driver on the host if it is already installed!
RUN wget https://www.xsens.com/hubfs/Downloads/Software/MTSS/Releases/2022.0.0/MT_Software_Suite_linux-x86_2022.0_b7085_r119802.tar.gz \
    && tar -xzvf MT_Software_Suite_linux-x86_2022.0_b7085_r119802.tar.gz \
    && ./MT_Software_Suite_linux-x86_2022.0/mtsdk_linux-x86_2022.0.sh

# Add the source setup.bash command to the user's bashrc
RUN echo "source /opt/ros/noetic/setup.bash" >> /root/.bashrc

# Copy the ros_entrypoint.sh script from ros:ros-base
COPY ros_entrypoint.sh /
RUN chmod +x /ros_entrypoint.sh

# Set the ros_entrypoint.sh script as the entry point for the container
ENTRYPOINT ["/ros_entrypoint.sh"]

# Create a new workspace folder for ROS2
RUN mkdir -p /root/ros_ws/src

# Set the new workspace folder as the working directory
WORKDIR /root/ros_ws
