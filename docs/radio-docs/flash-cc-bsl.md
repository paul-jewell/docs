title: Flash Firmware using cc2538-bsl

# Flash Firmware using cc2538-bsl

[cc2538-bsl.py](https://github.com/JelmerT/cc2538-bsl) is a cross-platform Python script that allows you to flash firmware on TI's newer chips. All Electrolama boards are supported by cc2538-bsl.py.


## Installation

### Linux

To run cc2538-bsl.py you need to have python and pip installed on your system. If you don't have them installed, refer to your distribution package manager to get it set up. (On Debian/Ubuntu, `sudo apt update && sudo apt-get install python3-pip` should work. `sudo pip ...` is not the optimal way of installing packages but Python package management is out of scope for this document.)

Download and extract cc2538-bsl: `wget -O cc2538-bsl.zip https://github.com/JelmerT/cc2538-bsl/archive/refs/heads/master.zip && unzip cc2538-bsl.zip`

Install required dependencies: `sudo pip3 install pyserial intelhex`


### Windows
To run cc2538-bsl.py you need to have Python installed on your system. Download [Python for Windows](https://www.python.org/downloads/) and install. After installation verify Python is correctly installed by running `python -V` in Command Prompt. It should return Python and the version number.

If you receive a message similar to `Python is not recognized as an internal or external command, operable program or batch file.`, this means Python is either not installed or the system variable PATH hasn’t been set. You’ll need to launch Python from the folder in which it is installed or adjust your system variables to allow it to be launched from any location.

Download the [zipped code](https://github.com/JelmerT/cc2538-bsl/archive/master.zip) and extract to a folder.

Install required dependencies: Open Command Prompt and check if `pip` is installed by running `pip -V` which will show its version and install location. From the same Command Prompt run: `pip install pyserial intelhex`


### macOS
To run cc2538-bsl.py you need to install some extra python dependencies, python3 should already be shipped with macOS (Catalina onwards?).

Download and extract cc2538-bsl: `wget -O cc2538-bsl.zip https://codeload.github.com/JelmerT/cc2538-bsl/zip/master && unzip cc2538-bsl.zip`

Install required dependencies: `$ /usr/bin/python3 -m pip install --user pyserial intelhex` (As we cannot write to the system's location we need to install the dependencies with in the user location. The downside is this has to be installed for every user that will use cc2538-bsl.)

### FreeBSD
To run cc2538-bsl.py you need to install some extra python dependencies.

Install python3 and the required dependancies:
```bash
root@freebsd:~ # pkg install python37 py37-pip py37-pyserial py37-setuptools
root@freebsd:~ # pip-3.7 install intelhex
```

Download and extract cc2538-bsl:
```bash
root@freebsd:~ # fetch -o cc2538-bsl.zip https://codeload.github.com/JelmerT/cc2538-bsl/zip/master ; unzip cc2538-bsl.zip cc2538-bsl-master/cc2538-bsl.py
root@freebsd:~ # mv cc2538-bsl-master/cc2538-bsl.py /usr/local/bin/
root@freebsd:~ # rmdir cc2538-bsl-master/
```

You can now run `cc2538-bsl.py` from anywhere.

Wghen using cc2538-bsl.py you might need to add the `--bootloader-active-high` argument, this was needed on FreeBSD when testing prototype zzhp-lite adaptors.

## Put your stick in BSL mode

Please follow the following instructions to put your stick in BSL mode:

  - Unplug your stick from the host
  - Press the `BSL` pushbutton and keep holding while plugging the device back into the host:

![zzh BSL pushbutton](/_assets/zzh-bsl-button.jpg)

  - Give it a few seconds for the device to settle and set up and release the BSL button
  - Your stick should now be in ROM bootloader mode

<ins>It is imperative that you press and hold the BSL pushbutton **before** plugging it in to the host and release it **after a few seconds**. If you don't follow this, your stick will not enter BSL mode and flashing will fail.</ins>


## Flash firmware

To flash firmware, run:

`python3 cc2538-bsl.py -p PORT -evw FIRMWARE`

...where `PORT` is the serial port your board is connected to and `FIRMWARE` is the hex file you want to flash (see [here](/radio-docs/#step-2-download-the-correct-firmware-for-your-stick) for help on choosing firmware).

<p class="warn">⚠️ <b>WARNING:</b> It is crucial that you download the correct firmware for your stick as using the wrong firmware will disable the BSL and you will need an external debugger / programmer to flash your stick again. Instructions for that can be found <a href="/radio-docs/advanced/flash-jtag/">here</a>.</p>


## Erase device

To completely erase the device flash, run:

`python3 cc2538-bsl.py -p PORT -e`

...where `PORT` is the serial port your board is connected to.


## Auto-BSL
cc2538-bsl.py supports "Auto-BSL" (details [here](/radio-docs/bsl/#auto-bsl)) on zzhp and zzhp-lite, so you can skip the BSL pushbutton press for flashing these boards. <ins>zzh and zoe2 does not support Auto-BSL!</ins>
