title: Flash Firmware using cc2538-bsl

One of the nice things about these new chips from TI is the inclusion of a serial bootloader in the ROM. Enabled by default and available unless explicitly modified by the application (see `CCFG:BL_CONFIG`), you can flash code without needing an external programmer. In fact, if the device is empty (either fresh from the factory or after an erase cycle), it automatically enters the bootloader mode.

A summary of when the bootloader is invoked can be seen in this flowchart below:

![bsl flowchart](/_assets/bsl-flowchart.png)

(["CC2538/CC26x0/CC26x2 Serial Bootloader Interface"](http://www.ti.com/lit/an/swra466c/swra466c.pdf), Figure 1)

The default "backdoor enable" pin on CC2652R is `DIO_13` ([not `DIO_11` as noted in SWRA466C!](https://e2e.ti.com/support/wireless-connectivity/bluetooth/f/538/t/871984?LAUNCHXL-CC26X2R1-Bootloader-backdoor-enable-pin)) and zzh has a small pushbutton on this pin to make tinkering with it easier.

To trigger the ROM bootloader, follow these steps:

  - Unplug zzh from the host
  - Press the `BSL` button on the board and keep holding while plugging the device back into the host:

![zzh BSL pushbutton](/_assets/zzh-bsl-button.jpg)

  - Give it a few seconds for the device to settle and set up and release the BSL button
  - zzh should now be in ROM bootloader mode

[TI CC13xx/CC2538/CC26xx Serial Boot Loader (cc2538-bsl for short)](https://github.com/JelmerT/cc2538-bsl) is a Python script that can be used to flash the board and should work fine on pretty much any OS.

#### Linux
To run cc2538-bsl.py you need to have python and pip installed on your system. If you don't have them installed, refer to your distribution package manager to get it set up. (On Debian/Ubuntu, `sudo apt update && sudo apt-get install python3-pip` should work. `sudo pip ...` is not the optimal way of installing packages but Python package management is out of scope for this document.)

##### Download and extract cc2538-bsl

``` bash
wget -O cc2538-bsl.zip https://codeload.github.com/JelmerT/cc2538-bsl/zip/master && unzip cc2538-bsl.zip
```
##### Install required dependencies 

```bash
sudo pip3 install pyserial intelhex
```

##### Flash firmware

At this point you are going to need a firmware file to flash to your device. As a test, you can grab [this small program (blink.bin)](/_assets/blink.bin) that toggles the LED connected to `DIO_7`.

To flash `blink.bin`, run:

```Shell
$ ./cc2538-bsl.py -p /dev/ttyUSB0 -evw blink.bin
```

**Don't forget to change `/dev/ttyUSB0` to the port used on your machine!**

This shouldn't take long and if successful, you will see blinkenlights!

If you want to re-flash zzh with new firmware, put it in bootloader mode and follow the flashing instructions. **This will work as long as BSL is not disabled by the firmware you burn to these devices.**

##### Erase flash

To completely erase the device flash, run:

```Shell
$ ./cc2538-bsl.py -p /dev/ttyUSB0 -e
```

#### Windows
To run cc2538-bsl.py you need to have Python installed on your system. Download [Python for Windows](https://www.python.org/downloads/) and install. After installation verify Python is correctly installed by running `python -V` in Command Prompt. It should return Python and the version number.

If you receive a message similar to `Python is not recognized as an internal or external command, operable program or batch file.`, this means Python is either not installed or the system variable PATH hasn’t been set. You’ll need to launch Python from the folder in which it is installed or adjust your system variables to allow it to be launched from any location.

###### Install required dependencies 
Open Command Prompt and check if `pip` is installed by running `pip -V` which will show its version and install location.

From the same Command Prompt run:

```bash
pip3 install pyserial intelhex
```

###### Download and extract cc2538-bsl

Download the [zipped code](https://github.com/JelmerT/cc2538-bsl/archive/master.zip) and extract to a folder.


###### Flash firmware

At this point you are going to need a firmware file to flash to your device. As a test, you can grab [this small program (blink.bin)](/_assets/blink.bin) that toggles the LED connected to `DIO_7`. It is recommended to download it to the same folder cc2538-bsl is extracted to.

To flash `blink.bin`, navigate to the folder where you extracted cc2538-bsl and open a Command Prompt there

```bash
cc2538-bsl.py -p COM14 -evw blink.bin
```

**Don't forget to change `COM14` to the port used on your machine!**

This shouldn't take long and if successful, you will see blinkenlights!

If you want to re-flash zzh with new firmware, put it in bootloader mode and follow the flashing instructions. **This will work as long as BSL is not disabled by the firmware you burn to these devices.**

##### Erase flash

To completely erase the device flash, run:

```bash
cc2538-bsl.py -p COM14 -e
```

_Example of a successful flash of Z-Stack coordinator firmware under Windows:_
![zzh flash complete](/_assets/zzh-flash-complete.jpg)

#### macOS
To run cc2538-bsl.py you need to install some extra python dependencies, python3 should already be shipped with macOS (Catalina).

##### Download and extract cc2538-bsl

``` bash
wget -O cc2538-bsl.zip https://codeload.github.com/JelmerT/cc2538-bsl/zip/master && unzip cc2538-bsl.zip
```
##### Install required dependencies

As we cannot write to the system's location we need to install the dependencies with in the user location.
The downside is this has to be installed for every user that will use cc2538-dsl.

```bash
$ /usr/bin/python3 -m pip install --user pyserial intelhex
```

##### Flash firmware

At this point you are going to need a firmware file to flash to your device. As a test, you can grab [this small program (blink.bin)](/_assets/blink.bin) that toggles the LED connected to `DIO_7`.

To flash `blink.bin`, run:

```bash
$ ls -l /dev/tty.usbserial-*
$ ./cc2538-bsl.py -p /dev/tty.usbserial-2212420 -evw blink.bin
```

**Don't forget to change `/dev/tty.usbserial-2212420` to the port used on your machine!**

This shouldn't take long and if successful, you will see blinkenlights!

If you want to re-flash zzh with new firmware, put it in bootloader mode and follow the flashing instructions. **This will work as long as BSL is not disabled by the firmware you burn to these devices.**

##### Erase flash

To completely erase the device flash, run:

```bash
$ ./cc2538-bsl.py -p /dev/tty.usbserial-2212420 -e
```
