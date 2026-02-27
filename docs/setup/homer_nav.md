# Install and use `homer_navigation` package (On Server)

!!! note
    Setting up this package on the server computer is highly recommended for a fluent experience of SLAM and navigation.
    Setting it up on the RPi should be OK, but the Pi will be struggling.

## Install `homer_navigation` Package

```console
mkdir -p ~/homer_ws/src  # create a workspace
cd ~/homer_ws/src  # navigate into src/ under the workspace
git clone https://github.com/linzhanguca/homer_navigation.git  # download package
cd ~/homer_ws  # navigate to workspace root
colcon build  # build all packages in workspace
echo "source ~/homer_ws/install/local_setup.bash" >> ~/.bashrc  # register package related resources
source ~/.bashrc
```

## Create a Map


1. Set HomeR at a good starting location on the ground.

2. Open a terminal on **RPi**, launch `homer_interface` and related resources
```bash
ros2 launch homer_bringup homer.launch.py
```

3. Open a terminal on **Server**, launch `slam_toolbox` under the "mapping" mode.
```bash
ros2 launch homer_navigation create_map.launch.py
```
> A Rviz window will be popped out.

4. Open a terminal either on Server or RPi, start `teleop_twist_keyboard` to drive the robot around and create the map simultaneously.
```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

<video autoplay loop muted playsinline width="100%">
  <source src="../assets/videos/homer_nav/mapping.webm" type="video/webm">
</video>


## Save the Map
1. In Rviz, go to "SlamToolboxPlugin" panel, and locate the "Serialize Map" button.
2. Type the **absolute path** for the map which is intended to be saved in the box next to the "Serialize Map" button.

    !!! info
        Use **absolute path**.
        For example, `/tmp/test_map`.
        The shortcut, `~/`, for the home directory will not work.
        You will need to explicitly express the home directory, for example: `/home/<username>/<follow_up_paths>`.

3. Click "Serialize Map" button, then verify if map files are saved successfully.

    !!! success
        Two files will be saved at the location specified in the "SlamToolboxPlugin".
        One is `<map_name>.data`, and the other one is `<map_name>.posegraph`

<video autoplay loop muted playsinline width="100%">
  <source src="../assets/videos/homer_nav/save_map.webm" type="video/webm">
</video>


## Navigation
1. Open localization configuration file `$HOME/homer_ws/src/homer_navigation/configs/localization_params.yaml`, and edit `map_file_name` around line 18. 
Use the map name you've saved in the previous steps, for example:
```yaml
  map_file_name: /tmp/test_map
```
Rebuild the navigation package with the specified map files.
```console
cd ~/homer_ws/
colcon build
source install/local_setup.bash
```

2. On **RPi**, launch `homer_interface` and `rplidar_composition`
  ```console
  ros2 launch homer_bringup homer.launch.py
  ```

3. On **Server**, launch `slam_toolbox` under the "localization" mode and a collection of `nav2` nodes.
```console
ros2 launch homer_navigation navigation.launch.py
```

3. (Optional) If the lidar scan and the map are misaligned, use "2D Pose Estimate" button on the top of the Rviz to set initial pose for HomeR.  

4. In Rviz, use "2D Goal Pose" button to set desired ending pose for HomeR.

<video autoplay loop muted playsinline width="100%">
  <source src="../assets/videos/homer_nav/navigation.webm" type="video/webm">
</video>

