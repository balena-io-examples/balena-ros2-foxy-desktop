# balena ROS2 Foxy Desktop container

[![balena deploy button](https://www.balena.io/deploy.png)](https://dashboard.balena-cloud.com/deploy?repoUrl=https://github.com/balena-io-examples/balena-ros2-foxy-desktop/)

## Special Note:
This GitHub repository is based on the foundational work of Keenan Johnson's repo, located here: https://github.com/keenanjohnson/balena-ros/. Be sure to give Keenan a Star and a Follow!


## About
This repo installs ROS2 into a 64-bit Ubuntu Arm container, ready to be run on a Raspberry Pi 4 or an NVIDIA Jetson Nano running balenaOS.  Other 64-bit Arm platforms might also work, but have not been tested.  The Dockerfile adds the basic requirements, adds the ROS key and APT sources, then installs the ROS binaries.  This repo sets up the ROS2 Foxy "Desktop" install, which is a fully featured installation including a desktop GUI, Rviz for robot visualization, and Gazebo for simulation.  If you only need the minimal ROS installation, there is also a "Base" repo available here: https://github.com/balena-io-examples/balena-ros2-foxy-base, which makes for a slimmer container.

## Usage
To get started, you can simply click the "Deploy with balena" button above, or use the traditional workflow and do a `git clone` of this repo, and then a `balena push YourAppNameHere` to deploy the container to your device.  You can read about how to create a balena application, setup your device, and install the balena CLI here:  https://www.balena.io/docs/learn/getting-started/raspberrypi4-64/python/

Once your device is provisioned and online, and the containers have been built and downloaded, you are ready.  This repo will build a full desktop environment, so you'll want to attach a monitor, keyboard, and mouse to your device.  Upon starting up, you will be brought directly to the desktop.  We have included the TurtleBot3 sample application, so that you can get started and see how Rviz and Gazebo work.  From the Start menu, open up a Terminal, and enter the following commands to launch TurtleBot:

```
export TURTLEBOT3_MODEL=burger
ros2 launch turtlebot3_gazebo turtlebot3_house.launch.py
```

It will take a moment, but you will see Gazebo launch and a 3D-rendered house get built.  A robot is created and placed on the ground out front, as well.  To drive TurtleBot, you need to launch another Terminal, and enter the following commands:

```
export TURTLEBOT3_MODEL=burger
ros2 run turtlebot3_teleop teleop_keyboard
```

This will allow you to move the robot around, using the keys as shown in the CLI: w,a,s,d,x for forward, left, stop, right, and back respectively.

You can also have a look at TurtleBot's view of the world by launching Rviz.  This is useful to get the Lidar perspective, and how it maps it's surroundings.  Open yet another terminal, and enter the following:

```
export TURTLEBOT3_MODEL=burger
ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True
```

You can find more documentation on how to make use of TurtleBot here:  https://emanual.robotis.com/docs/en/platform/turtlebot3/



![Alt text](/img/screenshot1.png?raw=true)

![Alt text](/img/screenshot2.png?raw=true)
