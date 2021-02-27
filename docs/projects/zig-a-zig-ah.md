title: zig-a-zig-ah! (CC2652 Stick)

# Overview

![zzh PCBA](/_assets/zzh-pcba-green-v2.jpg)


 zig-a-zig-ah! (zzh, for short) is a tiny "USB stick" form-factor development board for multiprotocol RF tinkering.

 It features:

 - TI [CC2652R](http://www.ti.com/product/CC2652R) 2.4 GHz multi-protocol wireless microcontroller targeting Thread, Zigbee, Bluetooth 5 Low Energy, IEEE 802.15.4g, IPv6-enabled smart objects (6LoWPAN) and proprietary systems
 - Communicates with the host computer via the common CH340 USB-UART bridge, no manual driver installation needed in most cases (Windows, Linux, FreeBSD, OpenBSD, and macOS), no driver support for illumos
 - Self-programming via the TI [CC-series serial bootloader](http://www.ti.com/lit/an/swra466c/swra466c.pdf). As long as it is not explicitly disabled in code, no external programmer needed! Pushbutton on the default pin to trigger this mode
 - cJTAG debug header, in case you disable BSL by accident or want a proper debug interface
 - SMA antenna port for an external antenna of your choice
 - General purpose LED

It is designed to fit in a tiny *[Gōng mó](https://www.theatlantic.com/technology/archive/2014/05/chinas-mass-production-system/370898/)* "USB Shell" and looks a bit like this when paired with your favourite SBC:

![zzh plugged in to Raspberry Pi](/_assets/zzh-plugged-in-v2.jpg)

Think of it as an upgrade to the ubiquitous [CC2531 USB Sticks](https://www.google.com/search?q=cc2531+stick) commonly used for Zigbee tinkering. CC2652 has a much beefier processor, more memory and a sane free compiler that should enable easier development compared to the old 8051 based CC2530/1 devices.

## Purchase 

Assembled versions of zzh are available on the [Electrolama Tindie Store](https://www.tindie.com/stores/electrolama/). Orders ship from London, UK.

Each zzh order contains a fully assembled and tested PCBA along with a plastic enclosure and a small antenna:

![zzh case and antenna](/_assets/zzh-kit-v2.jpg)

An optional debug adapter kit of parts (requires assembly) can also be purchased:

![zzh debug adapter kit](/_assets/zzh-debug-adapter-kit-v2.jpg)

A portion of each sale will be donated to [@Koenkk](https://github.com/Koenkk/) to support his work on [Zigbee2mqtt](https://github.com/Koenkk/zigbee2mqtt) and the [public firmware images](https://github.com/Koenkk/Z-Stack-firmware) used by zzh and many other projects.


## User Manual

### Important Note

**Please keep in mind that zzh is a general purpose development board and as such, it is shipped "blank" with no code on the wireless microcontroller. You will need to program it before it does anything meaningful.** Given the application dependent nature of this board, limited after-sales support can be provided for Tindie purchases (For example: we can help you program this board but can't fix your Zigbee network range issues or offer specific software support). 

### Drivers for CH340

(Moved [here](/radio-docs/drivers/#ch340-zzh-only))


### Flashing using BSL

(Moved [here](/radio-docs/flash-cc-bsl/))


### Flashing using external debugger

Instructions on how to use CC-DEVPACK-DEBUG and other external debuggers are available [here](/radio-docs/advanced/flash-jtag/).


### Zigbee2mqtt

(Moved [here](/radio-docs/zigbee2mqtt/))


### Zigbee Home Automation (ZHA) integration in Home Assistant

(Moved [here](/radio-docs/zha-home-assistant/))

## Aside: TI Part Numbers

(Moved [here](/radio-docs/advanced/ti-part-numbers/))

## Downloads

  - EAGLE source files in [electrolama/zig-a-zig-ah](https://github.com/electrolama/zig-a-zig-ah)
  - [Schematic (pdf), Revision A](/_assets/zzh-revA-schematic.pdf)

## Changelog

In the repo, [click here](https://github.com/electrolama/zig-a-zig-ah/blob/master/CHANGELOG.md).

## License

zig-a-zig-ah! is designed by Electrolama / Omer Kilic and licensed under the [Solderpad Hardware License 2.0](https://solderpad.org/licenses/SHL-2.0/). 

### Regulatory Notice

This kit is designed to allow Product developers to evaluate electronic components, circuitry, or software associated with the kit to determine whether to incorporate such items in a finished product and Software developers to write software applications for use with the end product. This kit is not a finished product and when assembled may not be resold or otherwise marketed unless all required FCC (or any other local authority) equipment authorizations are first obtained. Operation is subject to the condition that this product not cause harmful interference to licensed radio stations and that this product accept harmful interference.

## ACKs

Thanks to:

  - [@GeorgeIoak](https://twitter.com/GeorgeIoak) and [@matthewvenn](https://twitter.com/matthewvenn) for design review and comments during early prototyping
  - [Fredrik K](https://www.linkedin.com/in/fredrik-kervel/) for his domain expertise, design review and (much appreciated!) RF help
  - [@KoenKK](https://github.com/koenkk/) for his work on the great Zigbee2mqtt project and testing prototypes
  - [@egelmex](https://twitter.com/egelmex) for testing prototypes, improving docs and being an all around cool dude
  - All the [contributors to the documentation repo](https://github.com/electrolama/docs/graphs/contributors)!

Name credit goes to [@9600](https://twitter.com/9600/), this had a much boring name before he suggested zig-a-zig-ah!

## Contact 

For general enquiries, suggestions and errors spotted: Email us at hello@this-domain. Community contributions to these pages are very much encouraged so you could also send pull requests on the [documentation repo](https://github.com/electrolama/docs) (source of these pages) with your proposed changes.

For support regarding Tindie purchases: support@this-domain.
