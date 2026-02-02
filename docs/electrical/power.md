# Power Management

- All the components of HomeR are powered by 2x 18650 Lithium-ion batteries (7.4V nominal).
- The battery feeds 2x [DRV8874 carrier boards](https://www.pololu.com/product/4035) to drive 2x brushed [DC motors](https://www.pololu.com/product/4805).
- A [Power Expansion Board](https://category.yahboom.net/products/power-board-pi5) (PEB) is responsible for converting the coarse battery power (could be 6V to 8.4V) to stabilized 5V, then providing it to the main computing device: [Raspberry Pi 5](https://www.raspberrypi.com/products/raspberry-pi-5/) (RPi5).
- RPi5 powers up the micro-controller: [Raspberry Pi Pico 2](https://www.raspberrypi.com/products/raspberry-pi-pico-2/) and the [LiDAR](https://www.slamtec.com/en/Lidar/A1) through the USB ports.
- Pico 2 eventually serves regulated 5V to power up the [ultrasonic sensor](https://www.sparkfun.com/ultrasonic-distance-sensor-hc-sr04.html) and the [motor encoders](https://www.pololu.com/product/4805) via the `VBUS` pin.
- The Pico 2 also powers up an [Inertial Measurement Unit](https://invensense.tdk.com/products/motion-tracking/6-axis/mpu-6050/) (IMU) module: GY-521 with 3.3V via `3V3(OUT)` pin.


See diagram below to grab a intuitive idea of HomeR's power management.

![power_wiring](assets/images/power_wiring.png)

!!! note "Replay"
    - A relay board (HomeR Thalamus) is used for power and signal distribution but not illustrated in the diagram.
      The design is hosted in the [homer_ee](https://github.com/linzhangUCA/homer_ee) repository.

