# Setup ROS 2 Environment

## 0. (Recommended) Pre-Requisites
- CPU: X86_64, ARM64
- Operating System: Ubuntu 24.04.

!!! note "Operating System (OS)"
    According to the [REP-2000](https://reps.openrobotics.org/rep-2000/#jazzy-jalisco-may-2024---may-2029) list, Ubuntu 24.04 and Windows 10 are both tier 1 supported OS by ROS 2 Jazzy, and MacOS is on the tier 3 list. 
    This means you can pretty much install ROS 2 on any OS.
    But installing Ubuntu on Raspberry Pi is way easier.
    Interested readers can follow the official guides to:
    - [install ROS 2 on Windows](https://docs.ros.org/en/jazzy/Installation/Windows-Install-Binary.html)
    - [build ROS 2 from source on MacOS](https://docs.ros.org/en/jazzy/Installation/Alternatives/macOS-Development-Setup.html)
    - or simply [run ROS 2 in dockers](https://docs.ros.org/en/jazzy/How-To-Guides/Run-2-nodes-in-single-or-separate-docker-containers.html)

## 1. Installation
We recommend you following the official [guide](https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html) to install ROS 2 with Ubuntu `deb` packages.

!!! danger "Version Binding"
    If this is your first time, please strictly bind the ROS 2 version: **Jazzy** with Ubuntu version: **24.04**.
