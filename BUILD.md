# Building PIP-11

## Raspberry Pi modules

Create a Config.mk file in the root directory of the module as described in the circle documentation. Assuming you are building the module for Raspberry Pi 4, its contents will be as follows:

    RASPPI = 4
    PREFIX = arm-none-eabi-
    STANDARD = -std=c++17

Navigate to module root dir.

Build a library

    ./makeall


Build bootloader

    cd boot
    make all

You will need the following files for RP4, which will need to be copied to the root of the SD card:

- bcm2711-rpi-4-b.dtb
- start4cd.elf
- fixup4cd.dat

Return to the module root dir.

    cd ..

Note: If you use the same hardware model for all modules, the bootloader can be built once and the files can be copied to different SD cards.


Build a module

    cd app
    ./makeall

Result file will be `<appname>/kernel7l.img` for 32bit RP 4 config, where `<appname>` is pip-11, pipanel or piterm. Result file will need to be copied to the root of the SD card.

## Raspberry Pico module

    cd pip-11-pclp11
    mkdir build
    cd build/
    cmake ..
    make

Result file will be `PCLP11.uf2`

[Home](README.md#further-reading)
