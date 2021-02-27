title: Flash Firmware using c/JTAG

# Flash Firmware using c/JTAG

**Please Note**: <ins>For general purpose usage, you will not need an external debugger and [BSL method](/radio-docs/flash-ti-flash-prog/) will be enough for your flashing needs</ins>. If you have accidentally disabled BSL on your stick by flashing it with an incompatible firmware, or if you are a firmware developer needing proper debugging facilities and/or want to get access to the RF tools in TI SmartRF Studio, follow along.


## cJTAG vs JTAG

TI's [newer generation chips](/radio-docs/advanced/ti-part-numbers/) use cJTAG as the default debug interface. While it may look like it (reduced pin count on the debug header), **cJTAG is not SWD**. cJTAG (IEEE 1149.7) is an extension to the JTAG standard (IEEE 1149.1), that reduces the number of required pins by multiplexing the TMS, TDI and TDO signals on a single bi-directional pin, providing all the normal JTAG debug and test functionality ([ref](https://www.segger.com/products/debug-probes/j-link/technology/interface-description/#cjtag-compatibility)).

The debug header on zzh only exposes TMS/TCK and as such a cJTAG compatible debug adapter is needed. On zzhp and zzhp-lite (Rev B3 onwards), all pins are brought out to the debug header so you can use a JTAG compatible debug adapter.


## Flashing using CC-DEVPACK-DEBUG (or TI XDS110)

The cheapest option for an officially supported debugger is the [CC-DEVPACK-DEBUG](http://www.ti.com/tool/CC-DEVPACK-DEBUG), available from most common electronics distributors. Here'a handy pinout reference for CC-DEVPACK-DEBUG:

![CC-DEVPACK-DEBUG Pinout](/_assets/cc-devpack-debug-pinout.png)

GUI tools to use with CC-DEVPACK-DEBUG are [SmartRF Flash Programmer v2](https://www.ti.com/tool/FLASH-PROGRAMMER) (recommended, Windows only) or [UniFlash](https://www.ti.com/tool/UNIFLASH) (cross-platform).

Due to space constraints, the debug header on zzh is (sadly) non-standard:

![zzh debug header pinout](/_assets/zzh-debug-pinout.png)

To convert the zzh 5-pin debug header to a standard 10-pin Cortex Debug Connector, a small adapter PCB is needed (unless you hack and solder an IDC cable to the board directly). Design files for this adapter can be found [in the repo](https://github.com/electrolama/zig-a-zig-ah/tree/master/Debug-Adapter).

With this adapter board plugged in to zzh, you can connect any debugger you wish to get access to the c/JTAG port. This little adapter board kit (some soldering required) is available as an optional add-on to zzh on [Electrolama Tindie Store](https://www.tindie.com/stores/electrolama/).

![The Debug Sandwich](/_assets/zzh-debugger-devpack.jpg)

(The Debug Sandwich: CC-DEVPACK-DEBUG on top of the zzh-debug-adapter on top of zzh.)

**zzhp and zzhp-lite do not require this adapter as there is enough space on the board for the standard 10-pin c/JTAG header.**



## Flashing using J-Link

Make sure power is provided to your stick (i.e: plug it in) and use "J-Link Commander" to erase and flash your stick: 


``` doscon
J-Link>connect ?
Please specify device / core. <Default>: ARM7
Type '?' for selection dialog
Device>?
Please specify target interface:
  J) JTAG (Default)
  S) SWD
  T) cJTAG
TIF>T
Device position in JTAG chain (IRPre,DRPre) <Default>: -1,-1 => Auto-detect
JTAGConf>
Specify target interface speed [kHz]. <Default>: 4000 kHz
Speed>
Device "CC2652R1F" selected.


Connecting to target via cJTAG
InitTarget: Found ICE-Pick with ID: 0x3BB4102F
InitTarget: Found CPU TAP 0x4BA00477
DPv0 detected
Scanning AP map to find all available APs
AP[1]: Stopped AP scan as end of AP map has been reached
AP[0]: AHB-AP (IDR: 0x24770011)
Iterating through AP map to find AHB-AP to use
AP[0]: Core found
AP[0]: AHB-AP ROM base: 0xE00FF000
CPUID register: 0x410FC241. Implementer code: 0x41 (ARM)
Found Cortex-M4 r0p1, Little endian.
FPUnit: 6 code (BP) slots and 2 literal slots
CoreSight components:
ROMTbl[0] @ E00FF000
ROMTbl[0][0]: E000E000, CID: B105E00D, PID: 000BB00C SCS-M7
ROMTbl[0][1]: E0001000, CID: B105E00D, PID: 003BB002 DWT
ROMTbl[0][2]: E0002000, CID: B105E00D, PID: 002BB003 FPB
ROMTbl[0][3]: E0000000, CID: B105E00D, PID: 003BB001 ITM
ROMTbl[0][4]: E0040000, CID: B105900D, PID: 000BB9A1 TPIU
Cortex-M4 identified.
J-Link>erase
Without any give address range, Erase Chip will be executed
Erasing device...
J-Link: Flash download: Total time needed: 0.505s (Prepare: 0.072s, Compare: 0.000s, Erase: 0.415s, Program: 0.000s, Verify: 0.000s, Restore: 0.017s)
Erasing done.
J-Link>loadfile D:\blink.bin
No address passed for .bin file. Assuming address: 0x0
Downloading file [D:\blink.bin]...
J-Link: Flash download: Bank 0 @ 0x00000000: 2 ranges affected (40960 bytes)
J-Link: Flash download: Total: 0.903s (Prepare: 0.166s, Compare: 0.145s, Erase: 0.021s, Program & Verify: 0.449s, Restore: 0.119s)
J-Link: Flash download: Program & Verify speed: 89 KB/s
O.K.
```

**Error: "Selected interface (cJTAG) is not supported by the connected probe."**

It appears that some J-Link pods do not support cJTAG and this error message is displayed when performing the steps above. If this is the case, select JTAG as the target interface:

``` doscon
J-Link>connect ?
Please specify device / core. <Default>: ARM7
Type '?' for selection dialog
Device>?
Please specify target interface:
  J) JTAG (Default)
  S) SWD
  T) cJTAG
TIF>J
...
```

This won't work on zzh, as the extra pins needed for full JTAG are not brought out on the 5-pin debug header.