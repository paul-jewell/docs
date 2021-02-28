title: zoe2 (Zigbee, RTC and PoE for RPi)

<p class="info">ℹ️ zoe2 will be released soon! <a href="/list">Click here</a> to join the Electrolama mailing list to get updates.</p>


# Overview

zoe2 is the newer version of [zoe](/projects/zoe), a multi-protocol/frequency development board designed to be used alongside a Raspberry Pi. It follows the [Raspberry Pi HAT Mechanical specification](https://github.com/raspberrypi/hats) but it does not have the ID EEPROM therefore it is not technically a HAT.

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

Final prototypes are with testers at the moment and 

<p class="info">ℹ️ zoe2 will be released soon! <a href="/list">Click here</a> to join the Electrolama mailing list to get updates.</p>