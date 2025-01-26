# Files required for Raspberry Pi modules to work, placed on the SD card

Please note that all of the following applies only to Raspberry Pi (3, 4) and does not apply to Raspberry Pico.

For all three modules to work, the root of the SD card must contain

## Bootloader and firmware

In case of using RPI 4:

- bcm2711-rpi-4-b.dtb
- start4cd.elf
- fixup4cd.dat

The process of creating files is described in the documentation for circle and the [BUILD](BUILD.md) file.

## Application file

- Compiled application file (kernel7l.img in case of 32bit RPI4)

## Boot and Kernel configs

In addition, there should be two files in the root of the SD card -

- config.txt
- cmdline.txt

Their contents are described in detail in the circle documentation, but you can use the files that are located in the `assests/SD` directory of each module.

## Main module files

All additional files required for the emulator to work are placed in the `PIP-11` folder on the SD card.
Example files are located in the module's `assets/PIP-11` directory.

### Overlay files

When working on a real pdp, the operator entered the initial bootloader code from the console or used the board's ROM. For convenience, the emulator can find and load code from *.OVL files.

The file format is simple - the first two bytes indicate the initial address of loading into memory, the following bytes - data.

    od BOOTSTRP.OVL

    0000000    157744  016701  000026  012702  000352  005211  105711  100376
    0000020    116162  000002  157400  005267  177756  000765  177550
    0000036

A bootstrap tape loader placed into memory starting from 157744 (octal).

Paper tape Absolute Loader (ABSLDR.OVL) was loaded by the operator using the bootstrap loader.
You can use it to download tapes in absolute format. The start address of the loader is 157500

Sample session loading absolute tape with PDP-11 Basic:

    PDP-11 MONITOR V1.0
    
    BOOT> 
    w 140076
    @r
    140076
    @g 157500
    
    PDP-11 BASIC, VERSION 007A
    *O 
    READY
    LIST
    
    READY


**BOOTMON.OVL** - DEC PDP-11 Boot Monitor is adopted version from the [PCjs project](https://www.pcjs.org/software/dec/pdp11/boot/monitor/)

    PDP-11 MONITOR V1.0
    
    BOOT> HELP
    COMMANDS ARE BOOT, HALT, TEST, DIAG, LIGHTS AND HELP
    BOOT DEVICES ARE RK? RL? OR RP?
    BOOT>

The `RP` device is a more convenient way to load from paper tape.

### Disks and magnetic tapes.

PIP-11 supports 8 RP05 disk units, 4 RL02 disk units and a single DECtape unit.
Data on real devices is mapped to files on the SD card. 
The names of these files are fixed and in most cases cannot be changed.

The format DEVICE_FILENUMBER.TYPE is used for naming files.

#### DECtape TC11 unit

File `TC11_00.TAPE` is 295936 bytes long as TC11 uses a tape with a capacity of 578 blocks, each block containing 512 bytes.
SIMH calls this format 16bit RT-11.

You can create an empty file of this length and initialize it later in the system.


Create:

    dd if=/dev/zero of=TC11_00.TAPE bs=512 count=578
    578+0 records in
    578+0 records out
    295936 bytes transferred in ...

Init:

    RT-11SJ (S) V05.03  
    
    .SET TT QUIET

    .DIR DT0:
    ?DIR-F-Error reading directory
    
    .INIT DT0:
    DT0:/Initialize; Are you sure? Y
    
    .DIR DT0:
    
    
    0 Files, 0 Blocks
    564 Free blocks
    
    .

Done.

#### RK11 RK05 units

8 files have the name RK11_0x.RK05, where x is the unit number, from 0 to 7 inclusive.

You can create empty file 2494464 bytes long (4872 blocks, 512 bytes each), or prepare and prefill it using SIMH.

You will need at least one non-empty file if you intend to boot the system from RK05.

#### RL11 RL02 units

4 files have the name RL11_0x.RL02, where x is the unit number, from 0 to 3 inclusive.

You can create empty file 10485760 bytes long (20480 blocks, 512 bytes each), or prepare and prefill it using SIMH.

Note: By default RT-11 configured to use only 2 RL units, you have to SYSGEN own custom version to use all 4 units.

You will need at least one non-empty file if you intend to boot the system from RL02.

### Boot disks configuration

PIP-11 allows one built-in default configuration (number 0) and up to 4 (1..4) additional configurations. The default configuration uses the above fixed file names and boots from disk RK0:

The additional configurations allow changing the file names of disks RK0: and/or RL0: and run BOOTMON to select the boot device by the user.

The configuration file should be placed in the `PIP-11` folder and named `CONFIG.INI`
A sample file is located in the `assets/PIP-11` directory of the module.

    ; this is a comment
    
    [Configuration name]
    ; the same as default but allows to start from BOOTMON
    RK=SD:/PIP-11/RK11_00.RK05
    RL=SD:/PIP-11/RL11_00.RL02
    
    [RL0: XXDP]
    ; replaces RL0 with XXDP disk
    RK=SD:/PIP-11/RK11_00.RK05
    RL=SD:/PIP-11/XXDP22.RL02
    
    [RK0: Unix V6]
    ; replace RK0: with UNIX V6 bootable media
    RK=SD:/PIP-11/UNIX_V6.RK05
    RL=SD:/PIP-11/RL11_00.RL02

[Home](README.md#further-reading)
