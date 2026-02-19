# Setup ROS 2

We will install and set up system environment of ROS 2 on both Raspberry Pi and a host computer.

???+ info "Operating System (OS)"
    According to the [REP-2000](https://reps.openrobotics.org/rep-2000/#jazzy-jalisco-may-2024---may-2029) list, Ubuntu 24.04 and Windows 10 are both tier 1 supported OS by ROS 2 Jazzy, and MacOS is on the tier 3 list.
    This means you can pretty much install ROS 2 on any OS.
    But installing Ubuntu on Raspberry Pi is way easier.
    Interested readers can follow the official guides to:
    - [install ROS 2 on Windows](https://docs.ros.org/en/jazzy/Installation/Windows-Install-Binary.html)
    - [build ROS 2 from source on MacOS](https://docs.ros.org/en/jazzy/Installation/Alternatives/macOS-Development-Setup.html)
    - or simply [run ROS 2 in dockers](https://docs.ros.org/en/jazzy/How-To-Guides/Run-2-nodes-in-single-or-separate-docker-containers.html).

## 1. Installation

Please refer to the official guide to [install ROS 2 with Ubuntu `deb` packages](https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html).

!!! danger "Version Binding"
    If this is your first time, please strictly bind the ROS 2 version: **Jazzy** with Ubuntu version: **24.04**.

We have summarized all the shell commands from the official guide as below.
Copy and paste them to your terminal window to install ROS 2

``` sh
# Set locale
sudo apt update && sudo apt upgrade -y
sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

# Enable required repositories
sudo apt install software-properties-common -y
sudo add-apt-repository universe

sudo apt update && sudo apt install curl -y
export ROS_APT_SOURCE_VERSION=$(curl -s https://api.github.com/repos/ros-infrastructure/ros-apt-source/releases/latest | grep -F "tag_name" | awk -F\" '{print $4}')
curl -L -o /tmp/ros2-apt-source.deb "https://github.com/ros-infrastructure/ros-apt-source/releases/download/${ROS_APT_SOURCE_VERSION}/ros2-apt-source_${ROS_APT_SOURCE_VERSION}.$(. /etc/os-release && echo ${UBUNTU_CODENAME:-${VERSION_CODENAME}})_all.deb"
sudo dpkg -i /tmp/ros2-apt-source.deb

# Install development tools
sudo apt update && sudo apt install ros-dev-tools -y

# Install ROS 2
sudo apt install ros-jazzy-desktop -y
```

## 2. Verify ROS 2 Installation

This step verifies if ROS 2's communication, C++ and Python API are working correctly.
???+ tip
    This is exactly the same as the [Try some examples](https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html#try-some-examples) section in the official installation guide.

In one terminal, source the setup file and then run a C++ `talker`:

```sh
source /opt/ros/jazzy/setup.bash
ros2 run demo_nodes_cpp talker
```

In another terminal source the setup file and then run a Python `listener`:

```bash
source /opt/ros/jazzy/setup.bash
ros2 run demo_nodes_py listener
```

???+ tip
    Hold `Ctrl` then press `c` on the keyboard will terminate the executing program.

## 3. ROS 2 Environment Setup

- Install CycloneDDS (from terminal).

```sh
sudo apt install ros-jazzy-rmw-cyclonedds-cpp
```

Edit `$HOME/bashrc` file and add following to (the bottom of) the file.

``` sh
source /opt/ros/jazzy/setup.bash  # activate ros2
export ROS_DOMAIN_ID=123  # same on all devices, 0~232
export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp  # use cyclonedds
source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash  # autocomplete colcon commands
export _colcon_cd_root=/opt/ros/jazzy/  # specify ros2 root dir
```

!!! note
    `ROS_DOMAIN_ID` can be set to any number between 0 and 232.
    See the following section for more details.

???+ tip "User Configuration Script"
    In Ubuntu (and many Linux distros), a shell configuration file is saved at `$HOME/.bashrc`.
    The commands stored in this file will be executed every time the user started a terminal session.

### Quick Explanation

1. Add `source /opt/ros/jazzy/setup.bash` to `$HOME/.bashrc` file will automatically activate `ros2` command.
Or, we need to manually activate it every time a new terminal started, which is very inconvenient.

2. To ensure nodes running on different devices can communicate with each other, we need to designate a domain ID to these devices.
Append `export ROS_DOMAIN_ID=<id_number>` to `$HOME/.bashrc` file, where `<id_number>` should be within the range between 0 to 232.
For more details, please read the official guide [about domain ID](https://docs.ros.org/en/jazzy/Concepts/Intermediate/About-Domain-ID.html).

3. ROS 2 is using Data Distribution System (DDS) for communication management.
The default FastDDS is OK, but not the ideal one for working with the navigation.
We found Eclipse CycloneDDS is a good alternative, so we install it by:
`sudo apt install ros-jazzy-rmw-cyclonedds-cpp`.
Then enable it by appending `export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp` to the `$HOME/.bashrc` file.

4. [`colcon`](http://colcon.readthedocs.io/) is a command line tool to improve the workflow of building, testing and using multiple software packages.
Add `source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash` to `$HOME/.bashrc` file will enable autocompletion function of `colcon`.

5. We can quickly navigate around ROS 2 packages using the `colcon_cd` command.
Set the system environment variable: `export _colcon_cd_root=/opt/ros/jazzy/` in `$HOME/.bashrc` will designate root directory of all ROS 2 packages.
