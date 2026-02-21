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

- Download `homer_pico` repository
Open a terminal and enter following commands
```console
cd ~  # save to $HOME directory
git clone https://github.com/linzhangUCA/homer_pico.git
```

## 1. Test and Upload Motion Control Scripts
The HomeR's motion control is a modular design.

### 1.1. [BaseMotor]()
### 1.2. [EncodedMotor]()
### 1.3. [SentientWheel]()
### 1.2. [RegulatedWheel]()
### 1.2. [DiffDriveController]()


