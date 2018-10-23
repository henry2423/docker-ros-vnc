# Docker container images with ROS, Gazebo, Xfce4 VNC Desktop and Tensorflow

This repository developed from ConSol/docker-headless-vnc-container, with provide the headless VNC environments for docker container

## Current Image Build:
* `henry2423/ros-vnc-ubuntu:kinetic` : __Ubuntu 16.04 with `ROS Kinetic + Gazebo 8`__

  [![](https://images.microbadger.com/badges/version/henry2423/ros-vnc-ubuntu:kinetic.svg)](https://hub.docker.com/r/henry2423/ros-vnc-ubuntu/) [![](https://images.microbadger.com/badges/image/henry2423/ros-vnc-ubuntu:kinetic.svg)](https://microbadger.com/images/henry2423/ros-vnc-ubuntu:kinetic)

* `henry2423/ros-vnc-ubuntu:lunar` : __Ubuntu 16.04 with `ROS Lunar + Gazebo 9`__

  [![](https://images.microbadger.com/badges/version/henry2423/ros-vnc-ubuntu:lunar.svg)](https://hub.docker.com/r/henry2423/ros-vnc-ubuntu/) [![](https://images.microbadger.com/badges/image/henry2423/ros-vnc-ubuntu:lunar.svg)](https://microbadger.com/images/henry2423/ros-vnc-ubuntu:lunar)

## Spec
This is a Docker environmentalist equipped with ROS, Gazebo, xfce-vnc, no-vnc(http vnc service) and TensorFlow-gpu.
The container is developed under xfce-docker-container source and add the ROS, TensorFlow GPU environment on top of it, to provide a essential kit for anyone who develop with robotic and deep learning.

## Usage
- Run command with mapping to local port `5901` (vnc protocol) and `6901` (vnc web access):

      docker run -d -p 5901:5901 -p 6901:6901 henry2423/ros-vnc-ubuntu:kinetic

- If you want to get into the container use interactive mode `-it` and `bash`
      
      docker run -it -p 5901:5901 -p 6901:6901 henry2423/ros-vnc-ubuntu:kinetic bash

- If you want to connect to tensorboard, run command with mapping to local port `6006`:
      
      docker run -it -p 5901:5901 -p 6901cu:6901 -p 6006:6006 henry2423/ros-vnc-ubuntu:kinetic

- Build an image from scratch:

      docker build -t henry2423/ros-vnc-ubuntu:kinetic .

## Connect & Control
If the container runs up, you can connect to the container throught the following 
* connect via __VNC viewer `localhost:5901`__, default password: `vncpassword`
* connect via __noVNC HTML5 full client__: [`http://localhost:6901/vnc.html`](http://localhost:6901/vnc.html), default password: `vncpassword` 
* connect via __noVNC HTML5 lite client__: [`http://localhost:6901/?password=vncpassword`](http://localhost:6901/?password=vncpassword) 
* connect to __Tensorboard__ if you do the tensorboard mapping above: [`http://localhost:6006`](http://localhost:6006)
* The default username and password in container is ros:ros

## Detail Environment setting

#### 1.1) Using root (user id `0`)
Add the `--user` flag to your docker run command:

    docker run -it --user root -p 6901:6901 henry2423/ros-vnc-ubuntu:kinetic

#### 1.2) Using user and group id of host system
Add the `--user` flag to your docker run command:

    docker run -it -p 6901:6901 --user $(id -u):$(id -g) henry2423/ros-vnc-ubuntu:kinetic

### 2) Override VNC and Container environment variables
The following VNC environment variables can be overwritten at the `docker run` phase to customize your desktop environment inside the container:
* `VNC_COL_DEPTH`, default: `24`
* `VNC_RESOLUTION`, default: `1920x1080`
* `VNC_PW`, default: `vncpassword`
* `USER`, default: `ros`
* `PASSWD`, default: `ros`

#### 2.1) Example: Override the VNC password
Simply overwrite the value of the environment variable `VNC_PW`. For example in
the docker run command:

    docker run -it -p 5901:5901 -p 6901:6901 -e VNC_PW=vncpassword henry2423/ros-vnc-ubuntu:kinetic

#### 2.2) Example: Override the VNC resolution
Simply overwrite the value of the environment variable `VNC_RESOLUTION`. For example in
the docker run command:

    docker run -it -p 5901:5901 -p 6901:6901 -e VNC_RESOLUTION=800x600 henry2423/ros-vnc-ubuntu:kinetic

## Contributors

* [ConSol](https://github.com/ConSol/docker-headless-vnc-container) - developed the ConSol/docker-headless-vnc-container
