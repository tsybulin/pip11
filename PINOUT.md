# Connecting modules

## Main module

Basically, PIP-11 is the only module needed to run a working pdp-11/70 emulator.

The terminal, printer, paper reader/punch and panel are nice additions to the kit, but they are not necessary for the main module to work.

Connect monitor to HDMI or DSI socket, insert prepared SD card, attach power supply.

You will also need to connect a serial terminal to the RX / TX pins:

| HEADER PIN | GPIO | DESCRIPTION | DESTINATION |
|   --       | :--: |     --      |     --      |
| 6          |      |   Ground    |  Ground     |
| 8          | 14   | UART0 TXD   | TTL-RS232 TX or terminal RX |
| 10         | 15   | UART0 RXD   | TTL-RS232 RX or terminal TX |

If necessary, configure the external terminal parameters - 115200 bit/s, No parity, 1 Stop bit.

The following pins are used to connect to the I²C "paper" module:

| HEADER PIN | GPIO | DESCRIPTION | DESTINATION |
|   --       | :--: |     --      |     --      |
| 14         |      |   Ground    |  Ground     |
| 4          |      |   5V        |  5V         |
| 3          |  2   |   I²C1 SDA  |  I²C SDA    |
| 5          |  3   |   I²C1 SCL  |  I²C SCL    |

## Terminal module

Similar to the main module, connect the serial interface to the pins.

| HEADER PIN | GPIO | DESCRIPTION | DESTINATION |
|   --       | :--: |     --      |     --      |
| 6          |      |   Ground    |  Ground     |
| 8          | 14   | UART0 TXD   | TTL-RS232 TX or main module RX |
| 10         | 15   | UART0 RXD   | TTL-RS232 RX or main module TX |

Optionally, connect active low-level Buzzer to a header pin 16 (GPIO 23).

## Panel module

The panel module does not require a monitor or keyboard to operate, only an Ethernet cable for network connection and SD card to boot from.

The connection of the panel itself is carried out exactly according to the instructions on the manufacturer’s website.

## "Paper" module

A most complex one.

The module is powered by 5 volts from the I²C bus.

| HEADER PIN | GPIO | DESCRIPTION | DESTINATION |
|   --       | :--: |     --      |     --      |
| 4          |  2   |   A button  |             |
| 5          |  3   |   B button  |             |
| 6          |  4   |   I²C0 SDA  | I²C SDA bus |
| 7          |  5   |   I²C0 SDA  | I²C SCL bus |
| 8          |      |   Ground    |    I²C bus  |
| 39         |      |    VSYS     | 5V I²C bus  |
| 9          |  6   |   X button  |             |
| 10         |  7   |   Y button  |             |
| 11         |  8   |   LCD dc    |    LCD      |
| 12         |  9   |   SPI1 CS   |    LCD      |
| 14         |  10  |   SPI1 SCK  |    LCD      |
| 15         |  11  |   SPI1 MOSI |    LCD      |
| 16         |  12  |   LCD rst   |    LCD      |
| 17         |  13  |   LCD bl    |    LCD      |
| 19         |  14  |  Up button  |             |
| 20         |  15  | Down button |             |
| 21         |  16  |  SPI0 MISO  | SD card     |
| 22         |  17  |  SPI0 CS    | SD card     |
| 23         |      |  Ground     | SD card     |
| 24         |  18  |  SPI0 SCK   | SD card     |
| 25         |  19  |  SPI0 MOSI  | SD card     |
| 26         |  20  | Left button |             |
| 27         |  21  | Right button|             |
| 29         |  22  |Select button|             |

Also you will need to connect Vcc (5v or 3v) to SD card interface, depends on interface model.

[Home](README.md#further-reading)
