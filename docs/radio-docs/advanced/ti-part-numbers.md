title: TI WMCU Part Numbers

# TI Part Numbers

TI has quite a few different chips and they are all used/mentioned in open-source Zigbee world which can be daunting if you are just starting out. Here's a quick summary of part numbers and key features.

The older generation:

  - [CC2530](https://www.ti.com/product/CC2530): 2.4GHz Zigbee and IEEE 802.15.4 wireless MCU. Intel 8051 core, 256 Flash, only has 8kB RAM. Needs expensive compiler license for official TI stack to built your own firmware.
  - [CC2531](https://www.ti.com/product/CC2531): CC2530 with built-in USB. Used in the cheap "Zigbee sticks" sold everywhere. Intel 8051 core, 256 Flash, only has 8kB RAM. Needs expensive compiler license for official TI stack to built your own firmware.

The "middle" generation:

- [CC2538](https://www.ti.com/product/CC2538): 2.4GHz Zigbee, 6LoWPAN, and IEEE 802.15.4 wireless MCU. ARM Cortex-M3 core with with 512kB Flash and 32kB RAM.

The newer generation:

  - [CC2652R](https://www.ti.com/product/CC2652R): 2.4GHz only multi-protocol (Zigbee, Bluetooth, Thread, ...) wireless MCU. Cortex-M0 core for radio stack and Cortex-M4F core for application use, plenty of RAM. Free compiler option from TI. **zzh uses this chip**.
  - [CC2652RB](https://www.ti.com/product/CC2652RB): Pin compatible "Crystal-less" CC2652R (so you could use it if you were to build your own zzh and omit the crystal) but **not firmware compatible**.
  - [CC2652P](https://www.ti.com/product/CC2652P): CC2652R with a built-in RF PA. Not pin or firmware compatible with CC2652R/CC2652RB. **zzh-p will use this**.

  Multi frequency chips:

  - [CC1352R](https://www.ti.com/product/CC1352R): Sub 1 GHz & 2.4 GHz wireless MCU. Essentially CC2652R with an extra sub-1GHz radio.
  - [CC1352P](https://www.ti.com/product/CC1352P): CC1352R with a built in RF PA.

Auxiliary chips:

  - [CC2590](https://www.ti.com/product/CC2590), [CC2591](https://www.ti.com/product/CC2591), and [CC2592](https://www.ti.com/product/CC2592): 2.4 GHz range extenders. **These are not wireless MCUs, just auxillary RF [PA (Power Amplifier)](https://en.wikipedia.org/wiki/RF_power_amplifier) and [LNA (Low Noise Amplifier)](https://en.wikipedia.org/wiki/Low-noise_amplifier) in the same package.**.