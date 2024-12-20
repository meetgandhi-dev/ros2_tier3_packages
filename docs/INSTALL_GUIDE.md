# Installation Guide

## ROS 2 Jazzy Jalisco on Ubuntu 22.04 Jammy Jellyfish

This guide is based on standard [ROS 2 installation guide](https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html). It covers the steps to install ROS 2 Jazzy Jalisco on Ubuntu 22.04 Jammy Jellyfish.

### Set locale

Ensure that your system is configured with the correct locale settings.

```bash
locale  # check for UTF-8

sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

locale  # verify settings
```

### Enable Ubuntu Universe repository

Install software-properties-common and enable the Universe repository:

```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
```

### Setting up the repository

#### Retrieve the GPG Key

```bash
sudo wget -O /etc/apt/keyrings/ros2-tier3-pkgs-pub.gpg.key https://raw.githubusercontent.com/meetgandhi-dev/ros2_tier3_packages/main/ros2-tier3-pkgs-pub.gpg.key
```

#### Add the repository to your sources list

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/ros2-tier3-pkgs-pub.gpg.key] https://raw.githubusercontent.com/meetgandhi-dev/ros2_tier3_packages/main/debian_packages $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2-tier3-pkgs.list > /dev/null
```

#### Update Package Lists

```bash
sudo apt update
sudo apt upgrade
```

### Install ROS 2

You can check the available variants [here](https://ros.org/reps/rep-2001.html#jazzy-jalisco-may-2024-may-2029). At present, this repository supports the following variants:

#### ROS Core

```bash
sudo apt install ros-jazzy-ros-core
```

#### ROS Base

```bash
sudo apt install ros-jazzy-ros-base
```


#### Desktop

```bash
sudo apt install ros-jazzy-desktop
```

### Additional Information

#### Required RMW Installation Options

You need to install the RMW (ROS Middleware) you plan to use. The available options are:

1. ros-jazzy-rmw-fastrtps-cpp
2. ros-jazzy-rmw-cyclonedds-cpp
3. ros-jazzy-rmw-connextdds


**Note:**  _For more information on DDS, please refer to [DDS implementations](https://docs.ros.org/en/jazzy/Installation/DDS-Implementations.html#dds-implementations)._

#### Installing rosdep definitions for Available Packages

To get the list of available packages, execute the following commands:

```bash
sudo apt install ros-jazzy-rosdep-jammy
sudo rosdep init
rosdep update
```
**Note:**  _It is safe to ignore the error of `sudo rosdep init` command._

### Verify the Installation

To verify the installation, let's use the demo_nodes_cpp package. You can install it using the following command:

```bash
sudo apt install ros-jazzy-demo-nodes-cpp
```
**Note:**  _If you've installed the Desktop version, this step is not necessary. For other variants, this will install some additional packages._

#### Run the talker node with the following command:

```bash
source /opt/ros/jazzy/setup.bash
ros2 run demo_nodes_cpp talker
```

You should see output similar to:

```text
[INFO] [1733938316.291208014] [talker]: Publishing: 'Hello World: 1'
[INFO] [1733938317.290885520] [talker]: Publishing: 'Hello World: 2'
[INFO] [1733938318.290906103] [talker]: Publishing: 'Hello World: 3'
[INFO] [1733938319.291135480] [talker]: Publishing: 'Hello World: 4'
[INFO] [1733938320.290920276] [talker]: Publishing: 'Hello World: 5'
```

#### Open a new terminal and run the listener node:

```bash
source /opt/ros/jazzy/setup.bash
ros2 run demo_nodes_cpp listener
```

You should see the below output:

```text
[INFO] [1733938418.466201807] [listener]: I heard: [Hello World: 12]
[INFO] [1733938419.466237522] [listener]: I heard: [Hello World: 13]
[INFO] [1733938420.466240579] [listener]: I heard: [Hello World: 14]
```

