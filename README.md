# ORB-SLAM3 
install and run the ORBSLAM3 WITH ROS1 and REALSENSE D435i camera
Tested on Ubuntu 20.04
# Configuration Version info
-ubuntu 20.04  
-ROS1  
-Pangolin 0.6  
-Eigen 3  
-Opencv 4.2  
-C++14 Compiler  

# 1. Prerequisites

## OpenCV
Use this (https://github.com/doubleZ0108/OpenCV-4.2.0) to install opencv

## Pangolin
Before building Pangolin, ensure the necessary dependencies are installed:
```
sudo apt update
sudo apt install -y cmake g++ libglew-dev libboost-dev libboost-thread-dev \
libboost-filesystem-dev libboost-program-options-dev libjpeg-dev libpng-dev \
libtiff5-dev libegl1-mesa-dev
```
```
git clone https://github.com/stevenlovegrove/Pangolin.git
cd Pangolin
git checkout 86eb4975fc4fc8b5d92148c2e370045ae9bf9f5d
mkdir build
cd build
cmake ..
make -j$(nproc)
sudo make install
```
## Install the Eigen3 Library
```
sudo apt-get install libeigen3-dev

```
## Install the Boost library
There is no boost in the official website, but if boost is not installed, many errors about C++ will be reported and it cannot be located.
```
wget https://boostorg.jfrog.io/artifactory/main/release/1.77.0/source/boost_1_77_0.tar.gz
tar -xvf boost_1_77_0.tar.gz
cd boost_1_77_0
./bootstrap.sh
sudo ./b2 install
```
## Python
```
sudo apt install libpython2.7-dev
```
# 3. Building ORB-SLAM3 library and examples

Clone the repository:
```
git clone https://github.com/hussains72/SLAM3_Imp.git
```

```
cd SLAM3_Imp
chmod +x build.sh
./build.sh
```
```
cd SLAM3_Imp
chmod +x build_ros.sh
./build.sh
```
# 4. Add ROS environment
```
sudo gedit ~/.bashrc
export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:/home/sajid/SLAM3_Imp/Examples_old/ROS
source ~/.bashrc
```
# 5. install librealsense and the ROS wrapper for Ubuntu 20.04 (with ROS Noetic) from source

install dependencies
```
sudo apt update && sudo apt upgrade
sudo apt install git cmake build-essential libssl-dev libusb-1.0-0-dev pkg-config libgtk-3-dev libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev
sudo apt install ros-noetic-catkin python3-catkin-tools python3-pip
pip3 install -U setuptools
```
Install librealsense from Source
```
mkdir -p ~/realsense_ws/src
cd ~/realsense_ws/src
git clone https://github.com/IntelRealSense/librealsense.git
cd librealsense
git checkout v2.50.0  # Recommended version
mkdir build && cd build
cmake .. -DBUILD_EXAMPLES=true -DCMAKE_BUILD_TYPE=Release
make -j$(nproc)
sudo make install
```
Verify installation
```
realsense-viewer
```
Install ROS Wrapper for RealSense from Source
```
cd ~/catkin_ws/src
git clone https://github.com/IntelRealSense/realsense-ros.git
cd realsense-ros
git checkout 2.3.2  # Recommended version
cd ~/catkin_ws
catkin_make
source devel/setup.bash
```
Configure the ROS Wrapper
```
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
Test the ROS wrapper
```
roslaunch realsense2_camera rs_camera.launch
```

# 6. Running ORB-SLAM3 with realsense d435i camera
monocular node

```
rosrun ORB_SLAM3 Mono Vocabulary/ORBvoc.txt Examples/Monocular/EuRoC.yaml
```
RGBD node
```
rosrun ORB_SLAM3 RGBD Vocabulary/ORBvoc.txt Examples/RGB-D/TUM1.yaml
```

`
