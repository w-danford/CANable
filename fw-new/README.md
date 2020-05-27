# CANable Firmware

[![Build Status](https://travis-ci.org/linklayer/cantact-fw.svg?branch=master)](https://travis-ci.org/linklayer/cantact-fw)

also found at
https://github.com/linklayer/cantact-fw

This repository contains sources for CANable firmware.

## Building

Firmware builds with GCC. Specifically, you will need gcc-arm-none-eabi, which
is packaged for Windows, OS X, and Linux on
[Launchpad](https://launchpad.net/gcc-arm-embedded/+download). or
[ARM](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads).
Download for your system and add the `bin` folder to your PATH.

With that done, you should be able to compile using `make`.
If you are compiling for a device that has no external crystal,
compile with `make INTERNAL_OSCILLATOR=1`.

## Flashing & Debugging

Debugging and flashing can be done with any STM32 Discovery board as a
programmer. You can also use other tools that support SWD.

To use an STM32 Discovery, run [OpenOCD](http://openocd.sourceforge.net/) using
the stm32f0x.cfg file: `openocd -f fw/stm32f0x.cfg`.

With OpenOCD running, arm-none-eabi-gdb can be used to load code and debug.

## Flashing with dfu-util

Install the 'boot' jumper to 'boot' position.
CANable comes up as dfu enabled device:
"ID 0483:df11 SGS Thomson Microelectronics STM Device in DFU Mode"

Then dfu-util will download firmware:
"sudo dfu-util -d 0483:df11 -c 1 -i 0 -a 0 -s 0x08000000 -D /path/to/file"
where here the file is "CANable-b*.bin"

Read back flash, will get 32kB
"sudo dfu-util -d ,0483:df11 c 1 -i 0 -a 0 -s 0x08000000 -U file_name"


dfu-util is available from (Debian) repositories:
"sudo apt-get install dfu-util"

Similarily should be in rpm repositories

## Contributors

- [Bill Danford](http://electronics-software.com) - Add "b\r" command/response, correct for RTR messages,
-                                                   add user input validation to prevent malformed messages,
-                                                   add check when offline to dump user CAN messages
- [Ethan Zonca](https://github.com/normaldotcom) - Makefile fixes and code size optimization
- [onejope](https://github.com/onejope) - Fixes to extended ID handling
- Phil Wise - Added dfu-util compatibility to Makefile

## License

See LICENSE.md
