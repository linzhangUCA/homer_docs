# Set Up `homer_navigation` Package

!!! note
    It is recommended setting up this package on the server computer for a fluent experience of SLAM and navigation.
    Setting it up on the RPi may increase the burden, but should be OK to run.

## Create a Workspace (if not created one yet)

```bash
mkdir -p ~/homer_ws/src
```

## Install `homer_navigation` Package

```bash
cd ~/homer_ws/src
git clone https://github.com/linzhanguca/homer_navigation.git
cd ~/homer_ws
colcon build
source install/local_setup.bash
```

## Create a Map

1. Open a terminal on **RPi**, launch `homer_interface` and related resources

```bash
ros2 launch homer_bringup homer.launch.py
```

2. Open a terminal on the **server**, launch `slam_toolbox` and related resources.
```bash
ros2 launch homer_navigation create_map.launch.py
```

3. (Optional) Open a terminal either on the server or RPi, start `teleop_twist_keyboard` to drive the robot around and create the map.

```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```


## Save the Map
> Using slam_toolbox plugin


## Navigation
1. Open a terminal on **RPi**, launch `homer_interface` and related resources

```bash
ros2 launch homer_bringup homer.launch.py
```

2. Open a terminal on the **server**, launch `slam_toolbox` and related resources.
```bash
ros2 launch homer_navigation navigation.launch.py
```

3. In Rviz, use "2D Goal Pose" button to set desired ending pose.

