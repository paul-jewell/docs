title: RPi Setup for zoe/zoe2

# Initial Setup for Raspberry Pi

<ins>**Please note that these instructions only apply to zoe and zoe2, for any other board you do not need to perform these setup steps.**</ins>

There are a few steps to prepare your Pi for zoe or zoe2. A fresh install of Raspbian Lite is highly recommended before you get started.


## Reclaim UART

In order to get serial communication between the Pi and E18 module working, the console UART needs to be disabled (`TXD0` and `RXD0` pins are used).

To disable the console UART, edit `/boot/cmdline.txt` as root and remove `console=serial0,115200`. Save and exit.

You should also disable the hciuart service by running: `sudo systemctl disable hciuart`

`/dev/ttyAMA0` can now be used for communicating with the E18 module after a reboot.


## Disable WiFi and Bluetooth

To prevent radio interference with Zigbee, the built-in Bluetooth and WiFi radios should be disabled. **A wired Ethernet connection is strongly recommended as you will, without a shadow of doubt, have better Zigbee performance with other radios disabled**.

Edit `/boot/config.txt` as root and append the following to the end of the file:

``` bash
dtoverlay=disable-bt
dtoverlay=disable-wifi
```

Reboot the Pi and verify that both WiFi and Bluetooth interfaces are disabled by observing the outputs of `ifconfig` and `hciconfig`.


## Enable I2C (zoe only)

If you'd like to use the RTC, run `sudo raspi-config` and enable I2C under "Interfacing Options". After a reboot, install the `i2c-tools` package and scan the bus:

``` bash
sudo apt update && sudo apt install i2c-tools
sudo i2cdetect -y 1
```

If you have the RTC chip populated, it should report back on address `0x68`:

``` bash
$ sudo i2cdetect -y 1
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- 68 -- -- -- -- -- -- --
70: -- -- -- -- -- -- -- --
```