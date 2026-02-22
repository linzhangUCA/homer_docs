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
The HomeR's motion control is a modular design featured with following Classes.

### 1.1. [BaseMotor](https://github.com/linzhangUCA/homer_pico/blob/main/upython_scripts/base_motor.py)
Contains functions to invoke, stop and drive a brushed DC motor using a "Phase/Enable" type of motor driver chip.
The code below `if __name__ == "__main__"` showcases an usage of the class to ramp up and ramp down the speed of a motor in both forward and backward directions.
### 1.2. [EncodedMotor](https://github.com/linzhangUCA/homer_pico/blob/main/upython_scripts/encoded_motor.py)
Adds functions to `BaseMotor` class to count the quadrature encoder's signal changes caused by the motor's rotation.
### 1.3. [SentientWheel](https://github.com/linzhangUCA/homer_pico/blob/main/upython_scripts/sentient_wheel.py)
### 1.2. [RegulatedWheel]()
### 1.2. [DiffDriveController]()


