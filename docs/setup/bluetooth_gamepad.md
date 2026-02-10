# Set Up Bluetooth Gamepad

If you have a bluetooth gamepad as shown in the picture below, you can connect it either by a graphical interface or command line interface.

## (Graphical) Connection via System Settings

1. Press `Super`/`WIN`/`Cmd` key or left click the top-right corner of the Ubuntu desktop to bring out the system search bar.
Search "bluetooth" then left-click to enter the `Bluetooth` page in the `Settings` interface.

2. On gamepad, press and **hold** down the `HOME` and the `SHARE` button together, until the gamepads's LED starting to make **double blinks** pattern.
The double blinking pattern indicates the gamepad has entered the pairing mode.
The connectable gamepad will be appearing in the `Devices` list, named as "Wireless Controller".

!!! warning
    If the user release the `SHARE` button too quick or only pressed down the `HOME` button, the LED will make single blinks and the user will not be able to view/connect the gamepad.
    Wait for the single blinking to be stopped by itself, then try again by pressing and **holding** down the `HOME` and the `SHARE` button together.

3. Left-click the "Wireless Controller" and wait the device's status turned into "Connected".
The LED on the gamepad will be then stabled on.

## (CLI) Connection via Command Line

## Add `input` Group to User Account
```sh
sudo usermod -aG input $USER
```
