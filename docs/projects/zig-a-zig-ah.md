title: zig-a-zig-ah! (CC2652R Stick)

*Last updated: 08/03/2020, info about first prototype and initial testing*

# Overview

![zig-a-zig-ah! preview](/_assets/zzh-first-prototype.jpg)

 zig-a-zig-ah! (zzh, for short) is little USB-stick form factor dev board for multiprotocol RF tinkering.

 It features:

 - TI [CC2652R](http://www.ti.com/product/CC2652R) SimpleLink™ multi-standard wireless MCU, a multiprotocol 2.4 GHz wireless microcontroller targeting Thread, Zigbee®, Bluetooth® 5 Low Energy, IEEE 802.15.4g, IPv6-enabled smart objects (6LoWPAN) and proprietary systems.
 - [CC2652P](http://www.ti.com/product/CC2652P) also an option, has built-in PA (but no LNA?).
 - Communicates with the host computer via CP2102N/CP2104 USB-UART bridge.
 - Self-programming via the TI [CC-series serial bootstrap loader](https://github.com/JelmerT/cc2538-bsl) (as long as it is not disabled in code!), pushbutton on the default BSL pin to put the device into bootloader mode.
 - Cortex-M Debug Connector for SWD, in case you disable BSL by accident.
 - SMA antenna port for an external antenna of your choice. Secondary uFL port for measurements or an alternative antenna.

Think of it as an upgrade to the ubiquitous [CC2531 USB Sticks](https://www.google.com/search?q=cc2531+stick) commonly used for Zigbee tinkering. CC2652R has a much beefier processor, more memory and a sane free compiler option that should enable easier development compared to the old CC2531 based option.


## Current status

*08/03/2020*

First prototype unit built and passed all preliminary tests!

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr">SO SMOL <a href="https://t.co/T7pLxhy7zC">pic.twitter.com/T7pLxhy7zC</a></p>&mdash; Omer Kilic (@OmerK) <a href="https://twitter.com/OmerK/status/1236706883601412096?ref_src=twsrc%5Etfw">March 8, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

One of the nice things about these new chips from TI is the inclusion of a serial bootloader in the ROM. Enabled by default at the factory and available unless modified by the application otherwise, this means that you can burn code without needing an external programmer:

<blockquote class="twitter-tweet" data-conversation="none"><p lang="und" dir="ltr">👌 <a href="https://t.co/mYklA49yRr">pic.twitter.com/mYklA49yRr</a></p>&mdash; Omer Kilic (@OmerK) <a href="https://twitter.com/OmerK/status/1236715619657158657?ref_src=twsrc%5Etfw">March 8, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

Obligatory blinkenlights:

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr">BSL works and we have blinkenlights! <a href="https://t.co/z4zGFjes65">pic.twitter.com/z4zGFjes65</a></p>&mdash; Omer Kilic (@OmerK) <a href="https://twitter.com/OmerK/status/1236708880354328576?ref_src=twsrc%5Etfw">March 8, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

Debug adapter to get access to the SWD programming interface. Also can be used to perform RF tests using TI software:

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr">Debug adapter soldered up so I can tinker with TI SmartRF Studio. TI Eval Kit on left window for TX, zzh on the right RX (shows up as LAUNCHXL as the debugger is CC-DEVPACK-DEBUG) <a href="https://t.co/AQvvUWvBLy">pic.twitter.com/AQvvUWvBLy</a></p>&mdash; Omer Kilic (@OmerK) <a href="https://twitter.com/OmerK/status/1236725044153331712?ref_src=twsrc%5Etfw">March 8, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

Finally, a quick test of zigbee2mqtt:

<blockquote class="twitter-tweet" data-conversation="none"><p lang="en" dir="ltr">Quick test with ZNP coordinator firmware burnt via BSL, plugged into a Raspberry Pi and a fresh checkout of zigbee2mqtt with an IKEA remote test device. Ignore MQTT errors, device pairs successfully! Config below, had to specify pan_id and change serial details /cc: <a href="https://twitter.com/egelmex?ref_src=twsrc%5Etfw">@egelmex</a> <a href="https://t.co/HA4F4KhplM">pic.twitter.com/HA4F4KhplM</a></p>&mdash; Omer Kilic (@OmerK) <a href="https://twitter.com/OmerK/status/1236743034701824006?ref_src=twsrc%5Etfw">March 8, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

A little more work is needed before I am happy releasing this but it is close!

Revision A, Draft 3 design files [in the repository](https://github.com/electrolama/zig-a-zig-ah), some minor changes expected before the first proper release. Follow the development progress [on this Twitter thread](https://twitter.com/OmerK/status/1212864418155028480).

Interested in this? [Ping me](https://twitter.com/omerk) and let me know what you think

## Purchase 

Assembled versions of zig-a-zig-ah! will be made available on Tindie when it is ready.

[Click here](https://mailchi.mp/1746be86dd81/electrolama) to subscribe to the Electrolama mailing list to be notified of project updates and when kits/assembles units go on sale.

# Downloads

  - coming soon

# License

zig-a-zig-ah! is designed by Electrolama / Omer Kilic and licensed under the [Solderpad Hardware License 2.0](https://solderpad.org/licenses/SHL-2.0/). 

# ACKs

Name credit goes to [@9600](https://twitter.com/9600/), this had a much boring name before he suggested zig-a-zig-ah!

Special thanks to [@GeorgeIoak](https://twitter.com/GeorgeIoak) and [@matthewvenn](https://twitter.com/matthewvenn) for design review and comments.

# Contact 

Ping [@OmerK](https://twitter.com/omerk)
