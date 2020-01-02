title: zig-a-zig-ah! (CC2652R Stick)

*Last updated: 02/01/2020, added preliminary information*

# Overview

![zig-a-zig-ah! preview](/_assets/zzh-pcb-draft.png)

 zig-a-zig-ah! (zzh, for short) is little USB-stick form factor dev board for multiprotocol RF tinkering.

 It features:

 - TI [CC2652R](http://www.ti.com/product/CC2652R) SimpleLink™ multi-standard wireless MCU, a multiprotocol 2.4 GHz wireless microcontroller targeting Thread, Zigbee®, Bluetooth® 5 Low Energy, IEEE 802.15.4g, IPv6-enabled smart objects (6LoWPAN) and proprietary systems.
 - [CC2652P](http://www.ti.com/product/CC2652P) also an option, has built-in PA (but no LNA?).
 - Communicates with the host computer via CP2102N/CP2104 USB-UART bridge.
 - Self-programming via the TI [CC-series serial bootstrap loader](https://github.com/JelmerT/cc2538-bsl) (as long as it is not disabled in code!), pushbutton on the default BSL pin to put the device into bootloader mode.
 - Cortex-M Debug Connector for SWD, in case you disable BSL by accident.
 - SMA antenna port for an external antenna of your choice. Secondary uFL port for measurements or an alternative antenna.

Think of it as an upgrade to the ubiquitous [CC2531 USB Sticks](https://www.google.com/search?q=cc2531+stick) commonly used for Zigbee tinkering. CC2652R has a much beefier processor, more memory and a sane free compiler option that should enable easier development compared to the old CC2531 based option.

Name credit goes to [@9600](https://twitter.com/9600/), this had a much boring name before he suggested zig-a-zig-ah! :)

## Current status

![zig-a-zig-ah! fit test](/_assets/zzh-fit-test.jpg)

As of 02/01/2020 I have captured most of the schematic and will publish it over the weekend for comments. Expecting to do a prototype run late Jan/early Feb.

Interested in this? [Ping me](https://twitter.com/omerk) and let me know what you think!


## Purchase 

Assembled versions of zig-a-zig-ah! will be made available on Tindie when it is ready.

[Click here](https://mailchi.mp/1746be86dd81/electrolama) to subscribe to the Electrolama mailing list to be notified of project updates and when kits/assembles units go on sale.

# Downloads

  - coming soon

# License

zig-a-zig-ah! is designed by Electrolama / Omer Kilic and licensed under the [Solderpad Hardware License 2.0](https://solderpad.org/licenses/SHL-2.0/). 

# Contact 

Ping [@OmerK](https://twitter.com/omerk)
