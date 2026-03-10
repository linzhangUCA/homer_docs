# Set Up Raspberry Pi

## 1. Flash Ubuntu
>
> Coming soon.

## 2. Install and Setup ROS 2 Development Environment

Please refer to the [ROS Setup Guide](./ros.md).

### (Optional) Install [`slam_toolbox`](https://github.com/SteveMacenski/slam_toolbox) and [`Nav2`](https://docs.nav2.org/)

```console
sudo apt install ros-$ROS_DISTRO-slam-toolbox ros-$ROS_DISTRO-navigation2 ros-$ROS_DISTRO-nav2-bringup
```

## 3. Set up Raspberry Pi Camera

### 3.1. Install dependencies

```console
sudo apt install -y python3-pip git python3-jinja2
sudo apt install -y libepoxy-dev libjpeg-dev libtiff5-dev libpng-dev libopencv-dev
sudo apt install -y libboost-dev
sudo apt install -y libgnutls28-dev openssl libtiff5-dev pybind11-dev
sudo apt install -y qt6-base-dev libqt6core6t64 libqt6gui6t64 libqt6widgets6t64
sudo apt install -y meson cmake
sudo apt install -y python3-yaml python3-ply
sudo apt install -y libglib2.0-dev libgstreamer-plugins-base1.0-dev
sudo apt install -y python3-colcon-meson
```

### 3.2. Install ROS packages

!!! tip
    It is handy to have `rosdep` set up before we install the ROS packages.

```console
sudo rosdep init
rosdep update
```

Then, build the `camera_ros` package and `libcamera` driver inside a ROS workspace.

```console
mkdir -p ~/camera_infra/src  # create a dedicated ros workspace for camera
cd ~/camera_infra/src
git clone https://github.com/raspberrypi/libcamera.git
git clone https://github.com/christianrauch/camera_ros.git
source /opt/ros/$ROS_DISTRO/setup.bash
cd ~/camera_infra/
rosdep install -y --from-paths src --ignore-src --rosdistro $ROS_DISTRO --skip-keys=libcamera
colcon build
source ~/camera_infra/install/local_setup.bash
echo "source ~/camera_infra/install/local_setup.bash" >> ~/.bashrc
```

### Verify `camera_node`

1. Start the `camera_node`

```console
ros2 run camera_ros camera_node
```

1. Start `rviz2` in another terminal, then click "Add" -> "By Topic" -> "/camera/image_raw/Image".

## 4. Set synchronized time

Please refer to the article: [How to sync time between Robot and Host machine for ROS2](https://robofoundry.medium.com/how-to-sync-time-between-robot-and-host-machine-for-ros2-ecbcff8aadc4)

### Install [chrony](https://chrony-project.org/)

```bash
sudo apt install -y chrony
```

### Edit chrony configuration file

Open `/etc/chrony/chrony.conf` file with your favorite text editor (`nano`, `VSCode`, `vim`, etc.).
You'll need superuser privilege to edit this file, for example open it using

```bash
sudo nano /etc/chrony/chrony.conf
```

Add `server <server_ip_address> iburst` to the end of the configuration file.

### Restart chrony daemon

```bash
systemctl restart chronyd
```
