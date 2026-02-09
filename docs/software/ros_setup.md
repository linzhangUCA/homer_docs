# Setup ROS 2 Environment

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
sudo apt install software-properties-common
sudo add-apt-repository universe

sudo apt update && sudo apt install curl -y
export ROS_APT_SOURCE_VERSION=$(curl -s https://api.github.com/repos/ros-infrastructure/ros-apt-source/releases/latest | grep -F "tag_name" | awk -F\" '{print $4}')
curl -L -o /tmp/ros2-apt-source.deb "https://github.com/ros-infrastructure/ros-apt-source/releases/download/${ROS_APT_SOURCE_VERSION}/ros2-apt-source_${ROS_APT_SOURCE_VERSION}.$(. /etc/os-release && echo ${UBUNTU_CODENAME:-${VERSION_CODENAME}})_all.deb"
sudo dpkg -i /tmp/ros2-apt-source.debl

# Install development tools
sudo apt update && sudo apt install ros-dev-tools

# Install ROS 2
sudo apt install ros-jazzy-desktop
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

## 3. System Environment Setup

Install tools:

An example `~/.bashrc` file is as the below.

``` sh
source /opt/ros/jazzy/setup.bash  # activate ros2
source $HOME/homer_ws/install/local_setup.bash  # register HomeR's packages
export ROS_DOMAIN_ID=123  # same on all devices, 0~232
export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp  # use cyclonedds
source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash  # autocomplete colcon commands
```

???ip "User Configuration Script"
    In Ubuntu (and many Linux distros), a bash shell configuration file is saved at `$HOME/.bashrc`.
    The scripts stored in this file will be executed every time the user started a terminal session.

Interested readers can follow the contents below to take a peek at the detailed explanation of the executions above.

### 3.2. Activate ROS 2 automatically

Append `source /opt/ros/jazzy/setup.bash` to (the end of) `$HOME/.bashrc` file will automatically activate `ros2` command.
Or, we need to manually activate it every time a new terminal started, which is very inconvenient.

### 3.3. Enable message paths among machines

To ensure nodes running on different devices can communicate with each other, we need to designate a domain ID to these devices.
Append `export ROS_DOMAIN_ID=<domain_number>` to (the end of) `$HOME/.bashrc`, where `<domain_number>` should be within the range between 0 to 232.
For more details, please read the official guide [about domain ID](https://docs.ros.org/en/jazzy/Concepts/Intermediate/About-Domain-ID.html).

### 3.4. Use a dedicated workspace

When you have multiple projects to manage, keep HomeR distinctive and organized is important.
Create a dedicated ROS 2 workspace for it and reserve the `src` directory for the packages with the command:
`mkdir -p <workspace_path>/src`

### 3.5. Switch to a navigation friendly data distribution system (DDS)

ROS 2 is using Data Distribution System (DDS) for communication management.
The default Fast DDS is OK, but not the ideal one for working with the navigation.
We found Eclipse Cyclone DDS is a good alternative, so you can install it by:
`sudo apt install ros-jazzy-rmw-cyclonedds-cpp`

### 3.6. Automatic complete `colcon` command

`source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash`
