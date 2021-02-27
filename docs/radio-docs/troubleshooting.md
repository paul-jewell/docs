# Troubleshooting

## cc2538-bsl.py


## zigbee2mqtt

**"Error: Failed to connect to the adapter (Error: SRSP - SYS - ping after 6000ms)"**

This is a general error if there are communication problems with the adapter used.

A checklist to go through if you get this error message:

  * Try re-plugging in zzh once or twice.
  * Make sure you have the correct serial port and `rtscts: false` option set in your `configuration.yaml`
  * Make sure you have the correct firmware burned on your adapter. **Remember, zzh boards ship blank** so you will need to burn the appropriate firmware before using it with any application.
  * Are you using any virtualisation/container pass-through for the USB device? There have been reports of these potentially causing problems so for debugging purposes try communicating with the adapter directly from the host OS it is connected to (i.e: see if it works without the bypass)
  * Make sure you are using an up-to-date version of Zigbee2mqtt on the host and firmware on the adapter.


**"Error: Coordinator failed to start, probably the panID is already in use, try a different panID or channel"**

This error can appear when migrating an existing installation of zigbee2mqtt to use zzh. Changing the Zigbee channel used or Personal Area Network Identifier (PAN ID) should be sfficient to prevent conflicts with previous configurations. This can be accomplished by editing [`configuration.yaml`](https://www.zigbee2mqtt.io/information/configuration.html), specifying a custom `channel` or `pan_id` under the `advanced` section. Valid channels are in the range 11 to 26, however channels in the Zigbee Light Link (ZLL) range are recommended; channel 11 (default), 15, 20, or 25. PAN ID can by any 16-bit value (default: `0x1a62`). Note that these changes will require re-pairing of existing devices.


