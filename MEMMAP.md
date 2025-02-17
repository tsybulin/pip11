# PIP-11/70 Memory Map


| ADDRESS | ADDRESS | DESCRIPTION |
| :--: | :--: | -- |
| **FROM** | **TO** |  |
| 00 000 000 | 16 777 777 | System Memory, 3840K |
| 17 000 000 | 17 757 777 | Unibus Memory Map |
| 17 760 000 |            | **I/O PAGE** |
| 17 770 200 | 17 770 367 | KT11 Unibus Map registers |
| 17 772 000 | 17 772 040 | VT11 registers ¹ yet |
| 17 772 100 | 17 772 137 | MK11 Control ans status registers ¹ |
| 17 772 200 | 17 772 366 | KT11 SS/KK PAR/PDR |
| 17 772 516 |            | KT11 MSR3 |
| 17 774 400 | 17 774 420 | RL11 |
| 17 776 500 | 17 776 506 | DL11 ² |
| 17 777 310 | 17 777 330 | KE11 ¹ |
| 17 777 340 | 17 777 350 | TC11 |
| 17 777 400 | 17 777 412 | RK11 |
| 17 777 514 | 17 777 516 | LP11 |
| 17 777 526 | 17 777 534 | TOY  |
| 17 777 540 | 17 777 544 | KW11-P |
| 17 777 546 |            | KW11-L |
| 17 777 550 | 17 777 556 | PC11 |
| 17 777 560 | 17 777 566 | KL11 |
| 17 777 570 |            | Panel Switch/Display Register |
| 17 777 572 |            | KT11 MSR0 |
| 17 777 574 |            | KT11 MSR1 |
| 17 777 574 |            | KT11 MSR2 |
| 17 777 600 | 17 777 666 | KT11 UU PAR/PDR |
| 17 777 740 |            | KB11 Low Error Address register ¹ |
| 17 777 742 |            | KB11 High Error Address register ¹ |
| 17 777 744 |            | KB11 System Memory Address register ¹ |
| 17 777 746 |            | KB11 Memory Control register ¹ |
| 17 777 750 |            | KB11 Memory Maintenance register ¹ |
| 17 777 752 |            | KB11 Cache Hit/Miss register ¹ |
| 17 777 760 |            | Memory Lower Size register |
| 17 777 762 |            | Memory Upper Size register |
| 17 777 764 |            | System ID register |
| 17 777 766 |            | KB11 Error register |
| 17 777 770 |            | KB11 MicroBreak register ¹ |
| 17 777 772 |            | KB11 PIR register |
| 17 777 774 |            | KB11 Stack Limit register |
| 17 777 776 |            | KB11 PSW |

¹ Read 0, Write ignored, no implementation

² No hardware support

³ n/a

[Home](README.md#further-reading)
