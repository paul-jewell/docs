title: ZHA (Home Assistant)

# ZHA (Home Assistant)

[Zigbee Home Automation (ZHA)](https://www.home-assistant.io/integrations/zha/) integration is a built-in component in Home Assistant for native support, this makes the initial configuration very simple as you connect to the zzh adapter directly from Home Assistant's UI.

Note! **Support for Texas Instruments chips (especially CC2562) in Home Assistant's ZHA is still experimental as in early development!**

ZHA depends on the [zigpy python library (plus radio libraries for zigpy)](https://github.com/zigpy/) to support different Zigbee adapters/modules, and the radio library for TI CI chips supports the [same Z-Stack coordinator firmware as Zigbee2mqtt](https://github.com/Koenkk/Z-Stack-firmware/tree/master/coordinator).

## Configuration

Make sure zzh is recognised and available to your Home Assistant's ZHA instance. Navigate to _Configuration -> Integrations_, click on the `+` icon, find _Zigbee Home Automation_ and click on it.

![ZHA Integration](/_assets/zzh-zha-install.png)

Choose the device path of zzh and wait for installation to complete. Navigate to the ZHA integration at the bottom of the Configuration page. You will now have "Texas Instruments ZNP Coordinator" as the first device in ZHA. 

![ZHA Coordinator](/_assets/zzh-zha-coord.png)

In case the autodetection fails, a manual setup menu will be displayed. Check the device path and set _Radio Type_ as **ti_cc**. Leave other options as they are.

If ZHA is unable to connect to the zzh adapter then try re-plugging in the zzh USB adapter or try moving it to another USB-port.