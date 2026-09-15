# Programming Interface

## Overview

This document details the programming interface for version 0.4.0 of the RRIV datalogger. For version 0.4.1 and later, see [programming-interface.md](programming-interface-0.4.0.md)

On version 0.4.0 of the RRIV datalogger, the ST-Link programming pins and serial interface pin are exposed in J5 and J6.

These locations may have pin headers or JST XH size sockets installed, but either will accept Dupont connectors from the corresponding pins on the programming board. This is the preferred way to interface with and program the MCU.

## Boards and Locations

### RRIV PCB

![RRIV PCB](../../.gitbook/assets/rriv-0-4-0-datalogger-gpio.png)

### RRIV PCB Layout

![RRIV PCB Layout](../../.gitbook/assets/pcb-layout-stlink.png)

### Programming Board

![Programming Board](../../.gitbook/assets/programming-board.png)

### Programming Board Detail

![Programming Board](../../.gitbook/assets/programming-board-detail.png)

### Programming Board Pinout

![Programming Board](../../.gitbook/assets/debug-pinout.png)

## Connecting the RRIV datalogger for programming

1. Connect SWCLK, GND, SWDIO, RX, and TX from the programming board ot the RRIV datalogger using Dupont female-female connectors
2. Ensure that both jumpers at CN2 on the programmer board are removed
3. Plug the USB port of the programming board into the computer using a USB cable.
4. Power the RRIV board, using a second USB cable into the RRIV datalogger's USB port. (v0.4.1 boards may also be powered by battery)
5. You may now program the RRIV datalogger and monitor serial using platformio.

## Notes

* The USB port on the RRIV datalogger currently in ONLY for supplying power to the board on the bench. The RRIV datalogger cannot currently be programmed or interacted with thorugh this port.
* In some cases the MCU on the RRIV datalogger may need to be reset in order to program it. The recommended path for this is to power cycle the board.
