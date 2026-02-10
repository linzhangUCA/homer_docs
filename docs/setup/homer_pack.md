# Set up HomeR Packages

When you have multiple projects to manage, keep HomeR distinctive and organized is important.
This involves:

1. Create a dedicated ROS 2 workspace for HomeR and reserve the `src` directory right under it.
2. Clone/Download two ROS 2 packages for HomeR.
3. Build the workspace and register HomeR packages.

```sh
mkdir -p ~/homer_ws/src  # create workspace and src dir
cd ~/homer_ws/src  # navigate into the src dir
git clone https://github.com/linzhangUCA/homer_bringup  # clone hardware interface, required by RPi
git clone https://github.com/linzhangUCA/homer_navigation  # clone navigation pack, optional on RPi
cd ~/homer_ws  # navigate to workspace
colcon build  # build workspace (all packages in it)
source ~/homer_ws/install/local_setup.bash  # register homer packages
```

If you want to set `homer_ws` as your default ROS 2 workspace, then add the registration command: `source $HOME/homer_ws/install/local_setup.bash` in the `$HOME/bashrc` file.

An example of a fully loaded system configuration file for ROS 2 and HomeR is shown as below.

``` sh hl_lines="6"
source /opt/ros/jazzy/setup.bash  # activate ros2
export ROS_DOMAIN_ID=123  # same on all devices, 0~232
export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp  # use cyclonedds
source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash  # autocomplete colcon commands
export _colcon_cd_root=/opt/ros/jazzy/  # specify ros2 root dir
source $HOME/homer_ws/install/local_setup.bash  # register HomeR's packages
```
