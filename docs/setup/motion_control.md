# Motion Controller

The HomeR's motion control is relying on a series of MicroPython scripts running on the Pico board.
Please follow the steps below to get the Pico ready for driving HomeR and sensing its motion status.

!!! note
    If you haven't, please [set up the Pico](pico.md) before move on.

## Hardware List

- A Raspberry Pi Pico 2 development board (Pico).
- A Computer (Desktop/Laptop/RPi)
- A Micro-USB cable.
- (Optional) The relay PCB: [HomeR Thalamus](https://github.com/linzhangUCA/homer_ee)

## 1. Set Up [`homer_pico`](https://github.com/linzhangUCA/homer_pico) on Pico

1. Download and navigate to the repository.

    ```console
    cd ~  # use $HOME as an example
    git clone https://github.com/linzhanguca/homer_pico.git
    cd homer_pico
    ```

2. Upload differential drive controller

    ```console
    rshell -p /dev/ttyACM0 --buffer-size 512 cp -r upython_scripts/drivetrain /pyboard/
    ```

3. Set up automatic communication using [`pico_messenger.py`](./upython_scripts/pico_messenger.py).

    ```console
    rshell -p /dev/ttyACM0 --buffer-size 512 cp upython_scripts/pico_messenger.py /pyboard/main.py
    ```

    !!! note
        A hard reset (unplug Pico then plug it back) is required to activate `main.py`.

4. Verify communication
    ```console
    python3 tests/computer_messenger.py
    ```
    Both wheels will start to ramp the speed up and down then repeat with opposite direction.
    !!! bug "Communication Failure"
        In case the computer failed to spin the wheels, you may want to unplug the Pico and plug it back in.

## 2. Motion Control Scripts

The HomeR's motion control is a modular design made up by the following scripts.
It is highly recommended to test functionality of each module by the order.

!!! danger "Lift Wheels"
    It is very important that the motorized wheels are not contacting anything during the tests.
    Lift up the robot by putting it on top of something (e.g. a box).
    Check the wires and cables so that they are free from getting tangled.

### 2.1. [`base_motor.py`](https://github.com/linzhangUCA/homer_pico/blob/main/upython_scripts/drivetrain/base_motor.py)

This script contains the `BaseMotor` class.
It is featured methods/functions to invoke, stop and drive a brushed DC motor using a "Phase/Enable" type of motor driver chip ([DRV8874](https://www.ti.com/lit/gpn/drv8874)).
The usage examples and testing code is located under the line: `if __name__ == "__main__":`.
Run this script to ramp up and down the speed of a motor in both forward and backward directions.

### 2.2. [`encoded_motor.py`](https://github.com/linzhangUCA/homer_pico/blob/main/upython_scripts/drivetrain/encoded_motor.py)

This script extends the `BaseMotor` as the `EncodedMotor` class.
It adds methods/functions to count the signal changes sensed by a quadrature encoder attached to the motor.
Run this script to read the encoder counts while the motor speed is ramping up and down.

### 2.3. [sentient_wheel.py](https://github.com/linzhangUCA/homer_pico/blob/main/upython_scripts/drivetrain/sentient_wheel.py)

This script extends the `EncodedMotor` as the `SentientWheel` class.
It takes the characteristics of the wheel attached to the motor into account.
Run this script to read the wheel's linear and angular velocity as it is  ramping up and down.

### 2.4. [regulated_wheel.py](https://github.com/linzhangUCA/homer_pico/blob/main/upython_scripts/drivetrain/regulated_wheel.py)

This script extends the `SentientWheel` as the `RegulatedWheel` class.
It adds a PID controller to regulate the motor's velocity.
Run this script to set a target linear velocity for the wheel.
The PID controller will assess the gap between the measured velocity and target velocity to adjust control signals.

### 2.5. [diff_drive_controller.py](https://github.com/linzhangUCA/homer_pico/blob/main/upython_scripts/drivetrain/diff_drive_controller.py)

This scripts instantiates two `RegulatedWheel`s to construct the `DiffDriveController` class.
It regulates individual wheel's velocity based on
