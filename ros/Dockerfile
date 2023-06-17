FROM balenalib/amd64-ubuntu:jammy
ARG DEBIAN_FRONTEND=noninteractive

# Update Packages
RUN apt-get update
RUN apt-get install -y apt-utils
RUN apt-get install locales && locale-gen en_US en_US.UTF-8 && update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 && export LANG=en_US.UTF-8

# Install ROS Package Keys
RUN apt-get install -y curl gnupg2 apt-transport-https gnupg ca-certificates lsb-release
RUN curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key  -o /usr/share/keyrings/ros-archive-keyring.gpg
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

# Update package repo for ROS
RUN apt-get update

# Install ROS
RUN apt-get update && apt-get install -y ros-humble-desktop-full ros-humble-demo-nodes-cpp ros-humble-gazebo-ros2-control-demos xfce4 xinit xserver-xorg xserver-xorg-video-fbdev xinit pciutils xfonts-100dpi xfonts-75dpi xfonts-scalable 
RUN apt-get install -y python3-argcomplete wget unzip nano build-essential xterm gedit firefox ros-humble-turtlebot3 ros-humble-turtlebot3-gazebo ros-humble-turtlebot3-msgs ros-humble-dynamixel-sdk ros-humble-turtlebot3

# Configure Enviroment for ROS
RUN echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
COPY start.sh /start.sh
CMD ["/bin/sh", "start.sh"]

# Add tortoisebot repository
RUN mkdir -p ros2_ws/src
RUN cd ros2_ws/src
RUN git clone -b humble-devel https://github.com/AtharvaBhorpe/tortoisebot.git
RUN cd ..
RUN sudo apt install ros-humble-joint-state-publisher ros-humble-robot-state-publisher ros-humble-cartographer ros-humble-cartographer-ros  ros-humble-gazebo-plugins ros-humble-teleop-twist-keyboard  ros-humble-teleop-twist-joy ros-humble-xacro ros-humble-nav2* ros-humble-urdf ros-humble-rviz2 -y
RUN colcon build --symlink-install
RUN echo "source ~/ros2_ws/install/local_setup.bash" >> ~/.bashrc
