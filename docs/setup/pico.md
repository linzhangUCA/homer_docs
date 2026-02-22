# Setup Raspberry Pi Pico 2 (the Cerebellum)

## 0. Pre-Requisites
### 0.1 Hardware
- A Raspberry Pi Pico 2 development board (Pico).
- A Computer (Desktop/Laptop/RPi)
- A Micro-USB cable.
- (Optional) HomeR Thalamus


### 0.2 Software
- Install [Thonny](https://thonny.org/)
Open up a terminal and execute following command:

``` sh
bash <(wget -O - https://thonny.org/installer-for-linux)
```

!!! tip
    Go to [thonny.org](https://thonny.org/) for installation guides on other OS.

- Follow the official guide: [Getting started with Raspberry Pi Pico](https://projects.raspberrypi.org/en/projects/getting-started-with-the-pico/) to install MicroPython Firmware and get familiar with Python coding on the Pico.

- Download `homer_pico` repository.
```console
cd ~  # save to $HOME directory
git clone https://github.com/linzhangUCA/homer_pico.git
```

## 1. Test and Upload Motion Control Scripts
The HomeR's motion control is a modular design made up by the following scripts.
It is highly recommended to test functionality of each module by the order.

!!! danger "Lift Wheels"
    It is very important that the motorized wheels are not contacting anything during the tests.
    Lift up the robot by putting it on top of something (e.g. a box).
    Check the wires and cables so that they are free from getting tangled to the wheels.

### 1.1. [`base_motor.py`](https://github.com/linzhangUCA/homer_pico/blob/main/upython_scripts/base_motor.py)
This script contains the `BaseMotor` class.
It is featured methods/functions to invoke, stop and drive a brushed DC motor using a "Phase/Enable" type of motor driver chip ([DRV8874](https://www.ti.com/lit/gpn/drv8874)).
The usage examples and testing code is located under the line: `if __name__ == "__main__":`.
Run this script to ramp up and down the speed of a motor in both forward and backward directions.
### 1.2. [`encoded_motor.py`](https://github.com/linzhangUCA/homer_pico/blob/main/upython_scripts/encoded_motor.py)
This script extends the `BaseMotor` class by adding methods/functions to count the signals changes sensed by a quadrature encoder attached to the motor.
Run this script to read the encoder counts while the motor speed is ramping up and down.
### 1.3. [sentient_wheel.py](https://github.com/linzhangUCA/homer_pico/blob/main/upython_scripts/sentient_wheel.py)
### 1.4. [regulated_wheel.py](https://github.com/linzhangUCA/homer_pico/blob/main/upython_scripts/regulated_wheel.py)
### 1.5. [diff_drive_controller.py](https://github.com/linzhangUCA/homer_pico/blob/main/upython_scripts/diff_drive_controller.py)


