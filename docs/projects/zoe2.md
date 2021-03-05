title: zoe2 (Zigbee, RTC and PoE for RPi)

# zoe2

## Overview

zoe2 is the newer version of [zoe](/projects/zoe), a multi-protocol/frequency development board designed to be used alongside a Raspberry Pi. It follows the [Raspberry Pi HAT Mechanical specification](https://github.com/raspberrypi/hats) but it does not have the ID EEPROM therefore it is not technically a HAT.

It builds on top of [zoe](/projects/zoe2/), with an upgraded radio that supports both 2.4GHz and 433MHz operation (with a potential 800MHz option as well). While there isn’t much in terms of software support for sub-GHz operation yet, this is an area of interest as it will (potentially) allow you to have a single board solution for multi-frequency operation, all deployed with a single PoE powered ethernet cable!

## Features

  - [CC1352P](https://www.ti.com/product/CC1352P) radio from Texas Instruments, using the [E79-400DM2005S](https://www.ebyte.com/en/product-view-news.aspx?id=766) module:
    - Dual-band sub-1GHz and 2.4GHz RF transceivers compatible with Bluetooth and IEEE 802.15.4 PHY and MAC standards
    - Max. RF Power: 20dBm at sub-GHz / 5dBm at 2.4GHz
    - Built-in ROM serial bootloader - no external programmer/debugger needed
  - Optional external SMA antenna for sub-GHz radio, PCB trace antenna for 2.4GHz
  - IEEE 802.3af or passive 48V PoE support for single cable deployment
  - RTC with backup battery for offline timekeeping 
  - Hacker friendly features:
    - QWIIC/Stemma QT compatible I2C expansion header
    - Solder jumpers to connect JTAG/BSL pins to RPi GPIO for OpenOCD and auto-BSL (not fully tested!)
    - "ID EEEPROM" and support circuitry, not populated (you will need to solder it yourself)
  - Supported by [Koenkk's Z-Stack-firmware repository](https://github.com/Koenkk/Z-Stack-firmware) for use with the Open Source Home Automation software

![zoe2, Revision C1](/_assets/zoe2-pi.jpg)

## PoE Testing

Work in progress, a detailed lab note will be published soon. Here's a sneak peek:

![zoe2 Stress Test Sneak Peek](/_assets/zoe2-stress-test-initial.png)

## Project status and purchasing info

Final prototypes are with testers at the moment and the design is going through its DFM review. We are planning the initial production batch to happen within March. It will come in two flavours:

  - [zoe2-lite - CC1352P Radio for Raspberry Pi (Radio only)](https://shop.electrolama.com/collections/raspberry-pi-addons/products/zoe2-cc1352p-radio-for-raspberry-pi?variant=37646452883617)
  - [zoe2 - CC1352P Radio + RTC + PoE for Raspberry Pi](https://shop.electrolama.com/collections/raspberry-pi-addons/products/zoe2-cc1352p-radio-rtc-poe-for-raspberry-pi?variant=37646454161569)

Please join the waitlist on the corresponding product pages if you’re interested so we can establish initial demand (and manufacture enough stock!)

<p class="info">ℹ️ zoe2 will be released soon! <a href="/list">Click here</a> to join the Electrolama mailing list to get updates.</p>

