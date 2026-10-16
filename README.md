## RoboSubLA_Simulation

# Simulation environment using ROS2 Humble and Gazebo Ignition for testing underwater autonomy, computer vision systems, motion controllers, and buoyancy models. 

## Setup 

Installation Guide

~Note: ROS2 Humble is made for Ubuntu 22.04, so this guide is for that. This guide should be helpful if you don't have it installed -> [ https://github.com/seed-labs/seed-labs/blob/master/lab-setup/apple-arm/seedvm-v2/SeedVM-Ubuntu_Installation.md#installserver ] You can get the iso from here -> [ https://cdimage.ubuntu.com/ubuntu/releases/22.04/release/ ]

Much of this guide is from the ROS2 Humble install guide, but I added Gazebo and included tools that I found helpful/necessary. 

1. In the terminal, check to make sure your locale supports UTF-8: 
```
locale
```
If it doesn't then run: 
```
$ sudo apt update && sudo apt install locales
$ sudo locale-gen en_US en_US.UTF-8
$ sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
$ export LANG=en_US.UTF-8
```
Run locale again to confirm.

2. Ensure the Ubuntu Universe repository is enabled: 
```
sudo apt install software-properties-common
sudo add-apt-repository universe
```
3. Install Curl (if needed) and the ros2-apt-source package. 
```
sudo apt update && sudo apt install curl -y
export ROS_APT_SOURCE_VERSION=$(curl -s https://api.github.com/repos/ros-infrastructure/ros-apt-source/releases/latest | grep -F "tag_name" | awk -F'"' '{print $4}')
curl -L -o /tmp/ros2-apt-source.deb "https://github.com/ros-infrastructure/ros-apt-source/releases/download/${ROS_APT_SOURCE_VERSION}/ros2-apt-source_${ROS_APT_SOURCE_VERSION}.$(. /etc/os-release && echo ${UBUNTU_CODENAME:-${VERSION_CODENAME}})_all.deb"
sudo dpkg -i /tmp/ros2-apt-source.deb
```
4. Update the apt repository and ensure everything is up to date. 
```
sudo apt update
sudo apt upgrade 
```
5. Install ROS2 desktop, libraries, CML tools, compilers, and other things that are probably important: 
```
sudo apt install ros-humble-desktop
sudo apt install ros-humble-ros-base
sudo apt install ros-dev-tools
```
6. Source this file to set up your environment: 
```
source /opt/ros/humble/setup.bash
```
You can also do this: 
```
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
```
Otherwise, you'll have to run 'source /opt/ros/humble/setup.bash' every time you open the terminal.

7. Install ros-humble-ros-gz (Gazebo Ignition): 
```
sudo apt update && sudo apt install ros-humble-ros-gz -y 
```
8. Run rosdep so you can install ROS dependencies automatically: 
```
sudo rosdep init 
rosdep update 
```
9. I'm pretty sure this step only matters if you are running Ubuntu on a virtual machine, but if you are not and the Gazebo test below crashes due to Ruby 3.0 (It crashes because Gazebo's visual window can't communicate with graphics drivers; I don't think there is any actual issue with Ruby 3.0), try this, I guess: 
```
export LIBGL_ALWAYS_SOFTWARE=1 && ign gazebo empty.sdf
```
Again, to avoid having to type this into every new terminal run:
```
echo "export LIBGL_ALWAYS_SOFTWARE=1" >> ~/.bashrc
```
10. Test that Gazebo works: 
```
ign gazebo empty.dsf
```
11. Make sure NumPy is installed: 
```
python3 -c "import numpy; print('Numpy is installed')"
```
If not, run: 
```
sudo apt update && sudo apt install python3-numpy -y
```

## Launching RoboSubLA Simulator

Cloning and building the workspace will come soon, I promise! 

## Troubleshooting

Will add things here later. 



 
