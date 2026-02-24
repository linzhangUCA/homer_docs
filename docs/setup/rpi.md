# Hardware Interface on Raspberry Pi

## Install ROS Package for HomeR

```console
cd ~/homer_ws/src
git clone https://github.com/linzhanguca/homer_bringup.git
cd ~/homer_ws
colcon build
```

## Usage

```console
ros2 run homer_bringup homer_interface
```

```console
ros2 launch homer_bringup homer.launch.py
```
