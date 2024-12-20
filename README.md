# ROS 2 Tier 3 Packages

This repository contains ROS 2 Debian packages that need to be built on Tier 3 platforms, which are platforms that do not have official binary package support. The purpose of this repository is to simplify the process by providing pre-built packages, so users can avoid the complexities of building from source and instead use them like any other standard ROS 2 package available in the ROS ecosystem.

Currently, the following packages are available:


| ROS 2 Distro | OS | OS Code Name | CPU Architectures | Packages |
|:----------:|:----------:|:----------:|:----------:|:----------:|
| [Jazzy Jalisco](https://docs.ros.org/en/jazzy/Releases/Release-Jazzy-Jalisco.html) | Ubuntu 22.04 | jammy (Jammy Jellyfish) | AMD64 , ARM64 | [AMD64](debian_packages/dists/jammy/main/binary-amd64/Packages) , [ARM64](debian_packages/dists/jammy/main/binary-arm64/Packages) |

## Installation:

For detailed installation instructions, please refer to the [Install Guide](docs/INSTALL_GUIDE.md).
