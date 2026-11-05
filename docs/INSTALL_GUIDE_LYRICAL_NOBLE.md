# Installation Guide

## ROS 2 Lyrical on Ubuntu 24.04 Noble

This guide covers installing ROS 2 Lyrical on Ubuntu 24.04 Noble using the ROS 2 Tier 3 APT repository.

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

Install `software-properties-common` and enable the Universe repository:

```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
```

### Setting up the ROS 2 Tier 3 repository

#### Retrieve the GPG key

```bash
sudo mkdir -p /etc/apt/keyrings
sudo wget -O /etc/apt/keyrings/ros2-tier3-pkgs-pub.gpg.key \\
  https://raw.githubusercontent.com/meetgandhi-dev/ros2_tier3_packages/main/ros2-tier3-pkgs-pub.gpg.key
```

#### Add the repository to your sources list

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/ros2-tier3-pkgs-pub.gpg.key] https://raw.githubusercontent.com/meetgandhi-dev/ros2_tier3_packages/main/debian_packages noble main" \\
  | sudo tee /etc/apt/sources.list.d/ros2-tier3-pkgs.list > /dev/null
```

#### Update package lists

```bash
sudo apt update
sudo apt upgrade
```

### Install ROS 2

The repository currently supports the following ROS 2 variants:

#### ROS Core

```bash
sudo apt install ros-lyrical-ros-core
```

#### ROS Base

```bash
sudo apt install ros-lyrical-ros-base
```

#### Desktop

```bash
sudo apt install ros-lyrical-desktop
```

### Configure rosdep definitions for Tier 3 packages

Initialize rosdep if it has not already been initialized:

```bash
sudo rosdep init
```

If `rosdep init` reports that the sources list already exists, you can ignore that message.

The Tier 3 rosdep definitions are provided through two YAML files: the main rosdep list and the manual rosdep list. You only need to download the `.list` file below; it contains the GitHub links to both YAML files.

```bash
sudo wget -O /etc/ros/rosdep/sources.list.d/rosdep-list-lyrical-noble.list \\
  https://raw.githubusercontent.com/meetgandhi-dev/ros2_tier3_packages/main/rosdep/noble/rosdep-list-lyrical-noble.list
```

Update rosdep to download the definitions:

```bash
rosdep update
```

### Verify the installation

To verify the installation, use the `demo_nodes_cpp` package. Install it with:

```bash
sudo apt install ros-lyrical-demo-nodes-cpp
```

**Note:** If you installed the Desktop variant, this package is already included.

#### Run the talker node

```bash
source /opt/ros/lyrical/setup.bash
ros2 run demo_nodes_cpp talker
```

You should see output similar to:

```text
[INFO] [1733938316.291208014] [talker]: Publishing: 'Hello World: 1'
[INFO] [1733938317.290885520] [talker]: Publishing: 'Hello World: 2'
[INFO] [1733938318.290906103] [talker]: Publishing: 'Hello World: 3'
```

#### Run the listener node in a new terminal

```bash
source /opt/ros/lyrical/setup.bash
ros2 run demo_nodes_cpp listener
```

You should see output similar to:

```text
[INFO] [1733938418.466201807] [listener]: I heard: [Hello World: 12]
[INFO] [1733938419.466237522] [listener]: I heard: [Hello World: 13]
[INFO] [1733938420.466237522] [listener]: I heard: [Hello World: 14]
```
