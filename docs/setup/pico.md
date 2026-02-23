# Setup Raspberry Pi Pico 2 (MicroPython)

## Hardware List

- A Raspberry Pi Pico 2 development board (Pico).
- A Computer (Desktop/Laptop/RPi)
- A Micro-USB cable.

## Install MicroPython Firmware

Raspberry Pi Foundation has a very detailed and easy-to-follow guide allowing people to [get started using Pico](https://projects.raspberrypi.org/en/projects/getting-started-with-the-pico).

1. Install [Thonny](https://thonny.org/) on the computer.
    Open up a terminal and execute following command:

    ``` sh
    bash <(wget -O - https://thonny.org/installer-for-linux)
    ```

    !!! tip
        Go to [thonny.org](https://thonny.org/) for installation guides on other OS.

1. Install `rshell` if you prefer CLI for managing MicroPython scripts.

    ```console
    sudo apt install python3-pip
    pip install rshell --break-system-packages
    ```

1. (First time) Install MicroPython firmware from Thonny
    1. Click the bottom right corner of Thonny (where shows "Local Python 3"), then select "Install MicroPython"
    2. In the pop-out window, make sure the "Target volume" is automatically recognized and the "Target model" is set to "Raspberry Pi RP2350" or similar.
    3. Select "RP2" as the "MicroPython family", "Raspberry Pi Pico 2" as the "variant", "1.27.0" as the "version".

    Click "Install" button to add MicroPython firmware to your Pico board.

## Nuke Pico ("Factory Reset")

In case of the Pico gets frozen or is doing anything unexpected.
You may want to nuke the Pico board (clear the Flash memory).

1. Download the [`flash_nuke.uf2`](https://datasheets.raspberrypi.com/soft/flash_nuke.uf2) file (If downloaded a `.zip` file, unzip to extract the `.uf2` file.).
2. Hold the white button on the Pico board while plug the Pico into the computer until the Pico is recognized as a external storage device.
3. Drag and drop (copy and paste) the `flash_nuke.uf2` file to the external storage device.
