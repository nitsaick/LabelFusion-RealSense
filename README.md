# LabelFusion-RealSense
This repository is guide to install and run LabelFusion with RealSense

## Install or Build [librealsense](https://github.com/IntelRealSense/librealsense)

- [Install](https://github.com/IntelRealSense/librealsense/blob/master/doc/distribution_linux.md)
- [Build](https://github.com/IntelRealSense/librealsense/blob/master/doc/installation.md)

## Install ROS
- Install ROS [Kinetic](http://wiki.ros.org/kinetic/Installation/Ubuntu) on Ubuntu 16.04
- Install ROS [Melodic](http://wiki.ros.org/melodic/Installation/Ubuntu) on Ubuntu 18.04


## Build LCM
```bash
sudo apt install build-essential libglib2.0-dev default-jdk python-dev
cd ./3rd-party/lcm
mkdir build && cd build
cmake ..
make
sudo make install
cd ../..
```

## Build PCL
```bash
cd ./3rd-party/pcl
mkdir build && cd build
cmake ..
make
sudo make install
cd ../..
```

## Configure ROS Package
- [realsense-ros](https://github.com/IntelRealSense/realsense-ros)
- [ddynamic_reconfigure](https://github.com/pal-robotics/ddynamic_reconfigure/tree/kinetic-devel)
- [rgbd_ros_to_lcm](https://github.com/MobileManipulation/rgbd_ros_to_lcm)
- [rgbd_launch](https://github.com/ros-drivers/rgbd_launch)

```bash
cd ./catkin_ws/src/rgbd_ros_to_lcm/include
lcm-gen -x ../lcmtypes/*.lcm
cd ../../../..
```

## Make & Install ROS Package
```bash
cd ./catkin_ws/src/
catkin_init_workspace
cd ..
catkin_make clean
catkin_make -DCATKIN_ENABLE_TESTING=False -DCMAKE_BUILD_TYPE=Release
catkin_make install
echo "source `pwd`/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
cd ..
```

## Install docker
[Install](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

## Install nvidia-docker 1.0.1
```bash
wget -P /tmp https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.1/nvidia-docker_1.0.1-1_amd64.deb
sudo dpkg -i /tmp/nvidia-docker*.deb && rm /tmp/nvidia-docker*.deb
```


## Collect raw data from Realsense
```bash
roscore
```

```bash
roslaunch realsense2_camera rs_rgbd.launch
```

```bash
roslaunch rgbd_ros_to_lcm lcm_republisher.launch
```

```bash
lcm-logger
```
# Not done yet, coming soon