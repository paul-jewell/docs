title: NANDCat!

# Overview

NANDCat is an [SAO](https://hackaday.com/2019/03/20/introducing-the-shitty-add-on-v1-69bis-standard/) compatible [logic gate](https://en.wikipedia.org/wiki/NAND_gate) demonstrator/cute badge accessory. 

<blockquote class="twitter-tweet" data-dnt="true"><p lang="en" dir="ltr">NANDCAT IS ALIVE!<br><br>Will put design files and BOM up online in a few days.<br><br>It&#39;s SAO compatible and I&#39;ll pack a handful of them for Supercon next week, find me if you want to home a NANDCAT 😺 <a href="https://t.co/qNjOtDVKzT">pic.twitter.com/qNjOtDVKzT</a></p>&mdash; Omer Kilic (@OmerK) <a href="https://twitter.com/OmerK/status/1191759819155419138?ref_src=twsrc%5Etfw">November 5, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

The output (LED: D1) is a function of the inputs (Pushbuttons: SW1, SW2), here's the truth table for a NAND gate: 

A (SW1) | B (SW2) | Y (D1)
--------|---------|-------
0       | 0       | 1
1       | 0       | 1
0       | 1       | 1
1       | 1       | 0

The [artwork](https://www.flickr.com/photos/psd/6014043655) is by [@psd](https://twitter.com/psd), who kindly let me turn it into a silly PCB. Thanks, Paul!


# Schematic

![](/_assets/nandcat-schematic.png)


# Bill of Materials
Designator | Part | Description
-----------|------|------------
SW1, SW2 | [Omron B3S](https://octopart.com/search?q=+B3S-1000P+) or similar | 6mm SMD SPST-NO Tactile Switch
Q1, Q2 | [BC847B](https://octopart.com/search?q=BC847B) or similar  | NPN Transistor, SOT23 package
R1, R2, R4 | 1kΩ | Generic 0603 resistor
R3, R5 | 100kΩ | Generic 0603 resistor
D1 | 3mm LED | Generic LED, diffused lenses are better
J1 | 2x3 100mil header | Generic header
BAT1 | [Keystone 3034](https://octopart.com/search?q=Keystone+3034) or similar | SMD 20mm coin cell holder

SW1 and SW2 use the ubiquitous 6mm SMD pushbutton footprint, the Omron part is for reference only and there should be many other, cheaper, parts that can be used there. Same goes for BAT1.

Q1 and Q2 can be pretty much any NPN transistor in SOT23 package that has the following pinout:

![Transistor pinout](/_assets/npn-sot23.png)


# Downloads
  - KiCAD source files in [electrolama/nandcat](https://github.com/electrolama/nandcat)


# Changelog

  - Revision A (Oct 2019)
    - Initial release.
  - Revision B (Nov 2019)
    - Added a battery holder (CR2032) and some exposed copper for a brooch/pin back.


# Contact 

Ping <a href="https://twitter.com/omerk">@OmerK</a>
