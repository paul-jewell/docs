title: zoe (Zigbee, RTC and PoE for RPi)

*Last updated: 22/03/2020, tidied up documentation*

# Overview

![zoe, Revision C](/_assets/zoe-RevC.jpg)

zoe is a 802.15.4/Zigbee(tm) development board designed to be used alongside a Raspberry Pi. It follows the Raspberry Pi HAT Mechanical specification but it does not have the ID EEPROM therefore it is not technically a HAT.

The [E18-MS1PA](http://www.ebyte.com/en/product-view-news.aspx?id=121) Zigbee module used incorporates the [CC2530](http://www.ti.com/product/CC2530) wireless microcontroller with the [CC2592](http://www.ti.com/product/CC2592) Range Extender (PA+LNA). This is a fairly common and mature chip combo, famously used by [zigbee2mqtt](https://www.zigbee2mqtt.io/) and other open-source Zigbee systems.

Intended to be used as a Zigbee coordinator, zoe also has a very accurate [DS3231](https://www.maximintegrated.com/en/products/analog/real-time-clocks/DS3231.html) RTC for time keeping and can (optionally) power both itself and the Raspberry Pi through passive 48V or IEEE 802.3af Power-over-Ethernet (PoE).

While a [TagConnect](https://www.tag-connect.com/product/tc2050-idc-nl-10-pin-no-legs-cable-with-ribbon-connector) to [CC-Debugger](http://www.ti.com/tool/CC-DEBUGGER) footprint is included, no external programmer is required for flashing the Zigbee module thanks to [flash-cc2531](https://github.com/jmichault/flash_cc2531), a bitbanged implementation of the Chipcon programming protocol. 

## Purchase 

zoe comes in three flavours, in partial kit format where all SMD components are pre-soldered and connectors are not.

Available models and a comparison table:

|          | Radio | RTC | PoE |
|:--------:|:-----:|:---:|:---:|
| zoe-lite |   ✔️   |  ❌  |  ❌  |
|  zoe-RTC |   ✔️   |  ✔️  |  ❌  |
|  zoe-PoE |   ✔️   |  ✔️  |  ✔️  |

![zoe Lite Kit](/_assets/zoe-kit-lite.jpg)

![zoe RTC Kit](/_assets/zoe-kit-rtc.jpg)

![zoe PoE Kit](/_assets/zoe-kit-poe.jpg)

A limited of number of kits will be for sale on Tindie very soon.

**Please keep in mind that zoe is a general purpose development board and as such, it is shipped "blank" with no code on the wireless microcontroller. You will need to program it before it does anything meaningful.** Instructions are provided below.

[Click here](https://mailchi.mp/1746be86dd81/electrolama) to subscribe to the Electrolama mailing list to be notified of project updates and when kits go on sale.


# User Manual



## Unpacking and Soldering



## Initial Setup on the Raspberry Pi

Here are a few steps to prepare your Pi for zoe. A fresh install of Raspbian Lite is highly recommended before you get started.

### Reclaim UART

In order to get serial communication between the Pi and Zigbee module working, the console UART needs to be disabled. TXD0 and RXD0 pins are used to communicate with the CC2530 radio. 

To disable the console UART, edit `/boot/cmdline.txt` as root and remove `console=serial0,115200`. Save and exit.

You should also disable the hciuart service by running: `sudo systemctl disable hciuart`

`/dev/ttyAMA0` can now be used for communicating with the Zigbee module after a reboot.

### Disable WiFi and Bluetooth

To prevent radio interference with Zigbee, Bluetooth and WiFi should be disabled. You don't need to do this but a wired Ethernet connection is strongly recommended as you will, without a shadow of doubt, have better Zigbee performance with other radios disabled.

Edit `/boot/config.txt` as root and append the following to the end of the file:

```
dtoverlay=disable-bt
dtoverlay=disable-wifi
```

Reboot the Pi and verify that both WiFi and Bluetooth interfaces are disabled by observing the outputs of `ifconfig` and `hciconfig`.

### Enable I2C

If you'd like to use the RTC, run `sudo raspi-config` and enable I2C under "Interfacing Options". After a reboot, install the `i2c-tools` package and scan the bus:

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

Thanks to the flash-cc2531 tool, you can program the CC2530 radio without needing external programming adapters (typically a CC-DEBUGGER is used to program these parts). Please keep in mind that zoe is a general purpose development board and as such, it is shipped "blank" with no code on the wireless microcontroller. You will need to program it before it does anything meaningful.

**Make sure the programming switches are in the "ON" position before programming the module** 

(FIXME: add photo)

You might notice a piece of yellow/orange tape on top of the switch, peel this off before use.

Before we can use the flash-cc2531 tool, we need to install the wiringpi library dependency:

`sudo apt install wiringpi`

Grab the latest version of the flash-cc2531 tool and unzip:

`wget -O flash-cc2531.zip https://codeload.github.com/jmichault/flash_cc2531/zip/master && unzip flash-cc2531.zip`

You will need a suitable firmware for this board, if you want to experiment with [zigbee2mqtt](https://www.zigbee2mqtt.io/) the [Z-Stack-firmware](https://github.com/Koenkk/Z-Stack-firmware/tree/master/coordinator) by Koenkk is a good starting point, it's important that any firmware used should be compiled for both the CC2530 with the CC2592 range extender:

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

## Programming the radio (using CC-DEBUGGER)



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

  - EAGLE source files in [electrolama/zoe](https://github.com/electrolama/zoe)
  - [Schematic (pdf), Revision C](/_assets/zoe-revC-schematic.pdf)
  - [Local copy of the E18 Zigbee Module](/assets/E18-MS1PA1-PCB_Usermanual_EN_v1.1.pdf) (If you're looking for details of how CC2530 and CC2592 are connected inside the module)


# Changelog

In the repo, [click here](https://github.com/electrolama/zoe/blob/master/CHANGELOG.md).

# License

zoe is designed by Electrolama / Omer Kilic and licensed under the [Solderpad Hardware License 2.0](https://solderpad.org/licenses/SHL-2.0/). 

# Contact 

Ping <a href="https://twitter.com/omerk">@OmerK</a>
