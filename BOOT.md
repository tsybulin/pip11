# System boot and firmware update

Shortly after the main module has successfully loaded, the terminal will display a configuration selection screen similar to the following:


    PiP-11/70: Jan 23 2025 22:58:46 800x480 (100x25) (8x19)
    
    > SHOW CONFIGURATION
    
        0. RK0: DEFAULT
        1. RK0: RT-11 v5.3
        2. RL0: XXDP
        3. RK0: Unix V6
        9. FIRMWARE UPDATE

    BOOT 9 s.>

Press ESC to stop the countdown timer. Otherwise, the default configuration will be loaded when the timer expires.

Before loading the default configuration, you can select the number of the configuration to load:

- 0 or ENTER - load default configuration
- 1 .. 4 - use additional configuration start BOOTMON
- 9 - run TFTP server for file exchange or firmware update


## File exchange and firmware update

RPI modules are available for TFTP file sharing over the network and use a static IP configuration.

1. IP address: 172.16.103.10x
2. Netmask: 255.255.255.0
3. Gateway: 172.16.103.254

IP address for main module: 172.16.103.101, panel module: 172.16.103.102, serial terminal: 172.16.103.103

The panel module is available for exchange whenever it is turned on.
To reboot the panel after updating the firmware, press the address mode selection knob (upper right).

To switch the terminal to firmware mode, press the F11 key. To reboot after updating, press the key combination (3 keys simultaneously) Left Ctrl - Left Alt - Del.

To switch the main module to firmware mode, select 9 on the configuration selection screen.
To reboot the main module to normal mode, press ENTER on the terminal keyboard.

An example session for updating the CONFIG.INI file of the main module is given below. Assuming file CONFIG.INi is located in the current folder on the host computer.

    tftp 172.16.103.101
    tftp> binary
    tftp> verbose
    Verbose mode on.
    tftp> put CONFIG.INI PIP-11/CONFIG.INI
    putting CONFIG.INI to 172.16.103.101:PIP-11/CONFIG.INI [octet]
    Sent 232 bytes during 0.0 seconds in 1 blocks [inf bits/sec]
    tftp> ^D%

done. reboot module to see updated config.

[Home](README.md#further-reading)
