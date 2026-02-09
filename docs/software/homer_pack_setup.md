# Set up HomeR Packages

Install tools:

```sh
mkdir -p ~/homer_ws/src
cd ~/homer_ws/src
git clone https://github.com/linzhangUCA/homer_bringup
git clone https://github.com/linzhangUCA/homer_navigation
cd ~/homer_ws
colcon build
source ~/homer_ws/install/local_setup.bash
```

An example `~/.bashrc` file is as the below.

``` sh
...
source /opt/ros/jazzy/setup.bash  # activate ros2
source $HOME/homer_ws/install/local_setup.bash  # register HomeR's packages
export ROS_DOMAIN_ID=123  # same on all devices, 0~232
export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp  # use cyclonedds
source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash  # autocomplete colcon commands
export _colcon_cd_root=/opt/ros/jazzy/  # specify ros2 root dir
```
