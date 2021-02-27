title: disaster01 SAO

# Overview 

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">disaster01, a delightfully blinky SAO!<br><br>Details and files at <a href="https://t.co/Bo3KZ6MpBc">https://t.co/Bo3KZ6MpBc</a><br><br>At Supercon and have spare PCBs, find me (or <a href="https://twitter.com/matthewvenn?ref_src=twsrc%5Etfw">@matthewvenn</a> / <a href="https://twitter.com/sc_r?ref_src=twsrc%5Etfw">@sc_r</a>) if you want to build your own! <a href="https://t.co/6kPBOYpv6f">pic.twitter.com/6kPBOYpv6f</a></p>&mdash; Omer Kilic (@OmerK) <a href="https://twitter.com/OmerK/status/1195436338029285376?ref_src=twsrc%5Etfw">November 15, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

disaster 01 is an SAO compatible blinky thing debuted at Hackaday Supercon 2019. Designed by Anonymous Engineer from the Everwet Foundation, documented here for the benefit of the masses. 

Renamed during the design process due to the not-so-optimal graphics import facilities available in EAGLE.

Harkening the days when portable music required more dedication than shopping your fondle slab from your pocket, this is an homage to those good old days.

Doesn't need D cells but just as D-lightful! 

![](/_assets/disaster01.jpg)


## Schematic 

![](/_assets/disaster01-schematic.png)


## Bill of Materials

You are going to need a bunch of LEDs, 0402 current limiting resistors, one SPDT switch and a 2x3 male header.

Here's what our Taobao order looked like for the Supercon 2019 batch:

![](/_assets/disaster01-taobao.jpg)


## Downloads

  - EAGLE source files in [electrolama/disaster01](https://github.com/electrolama/disaster01)


## Build notes

  - Switch footprint is a little tight so you might have to get creative with it.
  - Top plane is VCC, bottom GND.
  - The random batch of LEDs we got were far too bright and when all lit, migraine inducing. Might want to do a test run and adjust your Rs accordingly.


## Changelog 

  - Revision A
    - Initial and most likely the final release (Nov 2019)
