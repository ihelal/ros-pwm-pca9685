# ROS driver for NXP Semiconductor PCA9685 I2C PWM chip

This is a ROS node for the PCA9685. The chip is notably used in the following products:

* [Adafruit 16-Channel 12-bit PWM/Servo Driver](https://www.adafruit.com/product/815)
* [Adafruit DC and Stepper Motor HAT for Raspberry Pi](https://www.adafruit.com/product/2348)
* [Waveshare Motor Driver HAT for Raspberry Pi](https://www.waveshare.com/motor-driver-hat.htm)
* [Waveshare Servo Driver HAT for Raspberry Pi](https://www.waveshare.com/servo-driver-hat.htm)

There should be no dependencies besides libi2c-dev.

## Parameters:

* **device** -- the path to the i2c device. Default is /dev/i2c-1. Use i2cdetect in the i2c-tools package to find out which bus your IMU is on.
* **address** -- the i2c address of the IMU. Default is 0x28.
* **frequency** -- PWM frequency in Hz. Default is 1600.

## Subscribers
* **command** -- a Int32MultiArray containing exactly 16 values corresponding to the 16 PWM channels. For each value, specify -1 to make no change to a channel. Specify a value between 0 and 65535 inclusive to update the channel's PWM value.

## Publishers
None.

## Services
None.

# Usage notes

## With the Adafruit Motor Driver HAT

The PCA9685 generates PWM signals which interface to two TB6612 motor drivers that handle 2 motors each.
Refer to the [Toshiba TB6612FNG documentation](https://www.sparkfun.com/datasheets/Robotics/TB6612FNG.pdf) for more info on the TB6612.

* PWM should be a PWM signal (0 to 65535).
* IN1 should be set to 0 OR 65535, nothing in-between.
* IN2 should be set to 0 OR 65535, nothing in-between.
* IN1 = 65535, IN2 = 65535: Brake
* IN1 = 65535, IN2 = 0: Forward
* IN1 = 0, IN2 = 65535: Reverse
* IN1 = 0, IN2 = 0: High impedance (coast)

### Motor channels

* Motor1: PWM = channel 8 (0 - 65535), IN1 = channel 9, IN2 = channel 10
* Motor2: PWM = channel 13, IN1 = channel 11, IN2 = channel 12
* Motor3: PWM = channel 2, IN1 = channel 3, IN2 = channel 4
* Motor4: PWM = channel 7, IN1 = channel 5, IN2 = channel 6