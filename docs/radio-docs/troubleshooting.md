# Troubleshooting

## The LED on my stick is blinking continously

Each stick is shipped with a test firmware that blinks the on-board LED, on and off continously. This is a "sanity check", to show that the device has survived its journey to you but it does not mean that it is ready for use. You will need to flash the correct firmware before your stick can be used, please refer to the [Quick Start guide](/radio-docs/).


## Check coordinator firmware

To check if the [coordinator firmware](/radio-docs/#step-2-download-the-correct-firmware-for-your-stick) is working correctly on your stick, grab a copy of the [znp-uart-test.py Python script](https://gist.github.com/omerk/0ee0e447a9e36786b4ff71d8f8126a23) and run it, changing the serial port to match yours.

If you get the `ModuleNotFoundError: No module named 'serial'` error message, install pyserial: `sudo pip3 install pyserial`

This script sends a ZNP command and checks that you get the expected response back. A `PASS` result means that you've sucessfully flashed your stick with the coordinator firmware. A `FAIL` result could either mean you have not flashed your stick properly, or you might not have specified the correct serial port (especially if you have multiple devices connected to you computer).


## cc2538-bsl.py

**"ERROR: Timeout waiting for ACK / NACK after ‘Synch (0x55 0x55)’**

This error is almost always seen when the device is not put into BSL mode correctly. Please follow the [instructions here](/radio-docs/bsl/#how-to-enter-bsl-mode) and try again.


## zigbee2mqtt

**Frequently asked questions**

Please refer to the [zigbee2mqtt FAQ](https://www.zigbee2mqtt.io/information/FAQ.html) for the most common issues.

**Error: "Failed to connect to the adapter (Error: SRSP - SYS - ping after 6000ms)"**

This is a general error if there is a communication problems with the adapter used.

A checklist to go through if you get this error message:

  * Make sure you have the correct serial port and `rtscts: false` option set in your `configuration.yaml`
  * Make sure you have the correct firmware burned on your adapter. **Remember, Electrolama boards do not ship with RF firmware** so you will need to burn the appropriate firmware before using it with any application (see [here](/radio-docs/#step-2-download-the-correct-firmware-for-your-stick)).
  * Are you using any virtualisation/container pass-through for the USB device? There have been reports of these potentially causing problems so for debugging purposes try communicating with the adapter directly from the host OS it is connected to (i.e: see if it works without the bypass)
  * Make sure that there aren't any concurrent serial port access issues (i.e: multiple pieces of software all trying to communicate with the same serial port at the same time)
  * Make sure you are using an up-to-date version of Zigbee2mqtt on the host and firmware on the adapter.


**Error: "Coordinator failed to start, probably the panID is already in use, try a different panID or channel"**

This error can appear when migrating an existing installation of zigbee2mqtt to use zzh. Changing the Zigbee channel used or Personal Area Network Identifier (PAN ID) should be sfficient to prevent conflicts with previous configurations. This can be accomplished by editing [`configuration.yaml`](https://www.zigbee2mqtt.io/information/configuration.html), specifying a custom `channel` or `pan_id` under the `advanced` section. Valid channels are in the range 11 to 26, however channels in the Zigbee Light Link (ZLL) range are recommended; channel 11 (default), 15, 20, or 25. PAN ID can by any 16-bit value (default: `0x1a62`). Note that these changes will require re-pairing of existing devices.


## ZHA

(tbd)
