title: ZOE (Zigbee + PoE for RPi)

# Overview

**(Preliminary instructions. Detailed write-up, design files and purchase information up soon -- 17/12/19)**

![ZOE, Revision B](/_assets/zoe.jpg)

ZOE is a 802.15.4/Zigbee(tm) development board designed to be used alongside a Raspberry Pi. It follows the Raspberry Pi HAT Mechanical specification but it does not have the ID EEPROM therefore it is not really a HAT.

The Zigbee radio used is the TI CC2530 along with CC2592 Range Extender (PA+LNA). This is a fairly common and mature chip combo, famously used by zigbee2mqtt and other open-source Zigbee systems.

Intended to be used as a Zigbee coordinator, ZOE also has RTC for time keeping and can (optionally) power both itself and the Raspberry Pi through passive 48V or IEEE 802.3af Power-over-Ethernet (PoE).

While a TagConnect to CC-Debugger footprint is included, no external programmer is required for flashing the Zigbee module thanks to flash-cc2531, a bitbanged implementation of the Chipcon programming protocol. **Make sure you set the dip switch to programming mode** and follow the instruction below to flash your board.


## Purchase 

Both kits and assembled versions of ZOE will be made available on Tindie in early 2020. 

[Click here](https://mailchi.mp/1746be86dd81/electrolama) to subscribe to the Electrolama mailing list to be notified of project updates and when kits/assembles units go on sale.


# User Manual

## Initial Setup

### Reclaim UART

In order to get serial communication between the Pi and Zigbee module working, the console UART needs to be disabled. `TXD0`/`RXD0` pins are used. Edit `/boot/cmdline.txt` and remove `console=serial0,115200` to claim the UART back. Also disable the hciuart service by running: `sudo systemctl disable hciuart`

`/dev/ttyAMA0` can now be used for communicating with the module after a reboot.

### Disable WiFi and Bluetooth

To prevent radio interference, Bluetooth and WiFi should be disabled. Edit `/boot/config.txt` and append the following to the end of the file:

```
dtoverlay=disable-bt
dtoverlay=disable-wifi
```

Reboot the Pi and verify that both WiFi and Bluetooth interfaces are disabled.

### Enable I2C

If you'd like to use the RTC, run `sudo raspi-config` and enable I2C under "Interfacing Options". After a reboot, install the i2c-tools package and scan the bus:

```
sudo apt-get install i2c-tools
sudo i2cdetect -y 1
```

If you have the RTC chip populated, it should report back on address `0x68`:

```
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


## Programming the radio (bit-banged, flash-cc2531)

**Make sure the programming jumpers are in the "ON" position before programming the module** (FIXME: add photo)

Install wiringpi dep:

`sudo apt install wiringpi`

Grab the latest flash-cc2531 and unzip:

`wget -O flash-cc2531.zip https://codeload.github.com/jmichault/flash_cc2531/zip/master && unzip flash-cc2531.zip`

You will need a suitable firmware for this board, if you want to experiment with zigbee2mqtt the [Z-Stack-firmware](https://github.com/Koenkk/Z-Stack-firmware/tree/master/coordinator) by Koenkk is a good starting point, it's important that any firmware used should be comiled for both the CC2530 with the CC2592 range extender:

``

Identify chip:
```
~/flash_cc2531 $ ./cc_chipid
  ID = a524.
```

Erase chip:
```
~/flash_cc2531 $ ./cc_erase
  ID = a524.
  erase result = 00a2.
```

Program chip:
```
~/flash_cc2531 $ ./flash_cc2531/cc_write ./CC2530ZNP-Prod.hex
  ID = a524.
  reading line 15490.
  file loaded (15497 lines read).
writing page 128/128.
verifying page 128/128.
 flash OK.
```

Return the programming jumpers back to the "OFF" position after programming the module.

To reset the module, either power cycle the Pi (off and the on again) or use the following little program to toggle the GPIO that the reset pin is connected to:

``` c
#include <stdio.h>
#include <wiringPi.h>

int pinRST=24;

int main()
{
    if(wiringPiSetup() == -1){
        printf("no wiring pi detected\n");
        return 0;
    }

    pinMode(pinRST, OUTPUT);
    digitalWrite(pinRST, HIGH);

    printf("ok\n");

}
```

Compile with `gcc -Wall -o modreset modreset.c -lwiringPi` and run to reset the module.


## Using the RTC

As root, set RTC up:

`# echo ds1307 0x68 > /sys/class/i2c-adapter/i2c-1/new_device`

Update the system time:

`$ sudo apt install ntpdate && sudo ntpdate -s 0.pool.ntp.org`

Write system time to RTC:

`$ sudo hwclock -w`

Read date/time back from RTC:

`$ sudo hwclock -r`


# Downloads

(will be added soon)


# Changelog

(will be added soon)

# Contact 

Ping <a href="https://twitter.com/omerk">@OmerK</a>
