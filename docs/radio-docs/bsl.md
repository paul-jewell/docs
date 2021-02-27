title: ROM Bootloader (BSL)

# ROM Bootloader (BSL)

One of the nice things about the new chips from TI is the inclusion of a serial bootloader in the ROM. Enabled by default and available unless explicitly modified by the application, you can flash code without needing an external debugger/programmer.

<p class="warn">⚠️ <b>WARNING:</b> Given that the bootloader is configurable, it is crucial that you download the correct firmware for your stick as using the wrong firmware will disable the BSL and you will need an external debugger/programmer to flash your stick again. Instructions for that can be found <a href="/radio-docs/advanced/flash-jtag/">here</a>.</p>


## How to enter BSL mode

To trigger the ROM bootloader, follow these steps:

  - Unplug your stick from the host
  - Press the `BSL` pushbutton and keep holding while plugging the device back into the host:

![zzh BSL pushbutton](/_assets/zzh-bsl-button.jpg)

  - Give it a few seconds for the device to settle and set up and release the BSL button
  - Your stick should now be in ROM bootloader mode

<ins>It is imperative that you press and hold the BSL pushbutton **before** plugging it in to the host and release it **after a few seconds**.</ins>

If you're doing this on a newly-received board that still has the factory test firmware running on it (LED blinking continously): When the device gets into BSL mode, the LED should stop blinking as the MCU would be running the BSL code as opposed to what the firmware tells the processor to do. If the LED is still flashing, this suggests that the stick is not entering the BSL mode.

If you're using zzhp or zzhp-lite with software that supports "auto-BSL" (cc2538-bsl.py only, for now), then you don't need to press the BSL button. See [here](#auto-bsl) for an explanation.


## Backdoor

The BSL "backdoor" is very simple mechanism: If the chip is blank or if the backdoor trigger pin is at the expected signal level (both defined in `CCFG:BL_CONFIG`) when power is applied then the processor enters the BSL mode.

A summary of when the bootloader is invoked can be seen in this flowchart below:

![bsl flowchart](/_assets/bsl-flowchart.png)

Refer to the ["CC2538/CC26x0/CC26x2 Serial Bootloader Interface"](http://www.ti.com/lit/an/swra466c/swra466c.pdf) as reference.

The de facto (see [here](https://github.com/Koenkk/Z-Stack-firmware/issues/210)) backdoor enable level is `LOW` and pins defined are:

  - `DIO_13` for  CC2652R (zzh)
  - `DIO_15` for CC1352P/CC2652P (zzhp/zzhp-lite/zoe2)

All Electrolama boards have a pushbutton on these pins, labelled "BSL".


## Auto-BSL

zzhp and zzhp-lite use a different USB-Serial converter chip than zzh, which exposes extra signals that are used to control the `BSL` and `RESET` pins of the wireless microcontroller. These pins are connected in the following manner:

  - Computer side `DTR` - WMCU `BSL`
  - Computer side `RTS` - WMCU `RESET`

Purpose of this arrangement is to get the device into BSL mode by cleverly toggling these pins in a special sequence so that automatic firmware updates could be done with, say, zigbee2mqtt without the need to unplug the coordinator board used. cc2538-bsl.py already supports this, so you don't actually have to press the BSL button to enter BSL mode on zzhp and zzhp-lite.


## CCFG Configuration

If you're building firmware yourself and would like to keep BSL working on Electrolama boards, make sure that the following settings are applied to the project when you're building it:

  - **Enable Bootloader:** Checked
  - **Enable Bootloader Backdoor:** Checked
  - **Bootloader Backdoor DIO:** 13 (for zzh only) or 15 (for zzhp/zzhp-lite/zoe2)
  - **Trigger level of Bootloader Backdoor:** Active Low

If the settings are different, then you won't be able to use the BSL pushbutton on your board to enter the BSL mode and will need a debugger to flash your boards (details [here](/radio-docs/advanced/flash-jtag/)).