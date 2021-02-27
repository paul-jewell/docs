title: Driver Installation

# Driver Installation


## CH340 (zzh only)

The USB-Serial functionality is handled all externally by CH340 and as far as CC2652 is concerned, communication happens over straight UART. First step in getting set up with zzh is to ensure that the host computer has the right drivers for the CH340 installed.

Plug your device in (don't worry about the firmware just yet) and ensure that zzh is recognised by your operating system before proceeding to the flashing steps.

### Linux

Issue `dmesg` and observe the device enumeration:

```Shell
[152343.203201] usb 1-1.4: new full-speed USB device number 5 using dwc_otg
[152343.336384] usb 1-1.4: New USB device found, idVendor=1a86, idProduct=7523, bcdDevice= 2.62
[152343.336400] usb 1-1.4: New USB device strings: Mfr=0, Product=2, SerialNumber=0
[152343.336409] usb 1-1.4: Product: USB2.0-Serial
[152343.338315] ch341 1-1.4:1.0: ch341-uart converter detected
[152343.341440] usb 1-1.4: ch341-uart converter now attached to ttyUSB0
```

CH340 drivers have been in the kernel for a while and as long as you are using a relatively new version ([driver changelog](https://github.com/torvalds/linux/commits/master/drivers/usb/serial/ch341.c)), you shouldn't have any issues.

### Windows

The drivers for CH340 should be automatically be picked up and you should see your device under "Ports (COM & LPT)" in Device Manager:

![serial port windows](/_assets/zzh-port-windows.png)

If you need to install the drivers manually, head over [here](http://www.wch.cn/downloads/CH341SER_ZIP.html) for the official drivers.

### macOS

Issue `dmesg` and observe the device enumeration:

```
IOUserSerial::AppleUSBCHCOM::<private>: 127 0x6000013e4058
IOUserSerial::<private>: 456 0x6000013e4058
IOUserSerial::<private>: 41 0x6000013e4058
DK: AppleUSBCHCOM-0x1000030ea::start(IOUSBHostInterface-0x1000030e5) ok
```

### Synology

The drivers for the CH340 chip appear to be missing on some (all?) Synology NAS devices. If you're not seeing any serial devices when you issue `dmesg` or `lsusb`, this is probably the case for your device as well.

`UsbSerialDrivers DSM 6.2 v6-4` from [this third party repository](http://www.jadahl.com/drivers_6.2) installs the `ch341.ko` needed.


## CP2102/4 (zzhp and zzhp-lite)

(tbd)


## zoe and zoe2

Both zoe and zoe2 are connected to the UART pins on the Raspberry Pi directly and do not require any drivers. You will need to disable the console to reclaim the UART lines though, follow instructions [here](XXX).