# Programming Interface

## Overview

On version 0.4.1 and later of the RRIV datalogger, the ST-Link programming pins and serial interface pin are exposed in J5 and J6.

These locations may have pin headers or JST XH size sockets installed, but either will accept Dupont connectors from the corresponding pins on the programming board. This is the preferred way to interface with and program the MCU.

## Boards and Locations

### RRIV PCB

![RRIV PCB](../../.gitbook/assets/rriv-0-4-1-datalogger.jpeg)

### Programming Board

![Programming Board](../../.gitbook/assets/programming-board.png)

### Programming Board Detail

![Programming Board](../../.gitbook/assets/programming-board-detail.png)

### Programming Board Pinout

![Programming Board](../../.gitbook/assets/debug-pinout.png)

## Connecting the RRIV datalogger for programming

1. Connect SWCLK, SWDIO, RX, and TX from the programming board ot the RRIV datalogger using Dupont female-female connectors
2. Power the board using USB. Generally if the board is powered by USB, it is not necessary to connect an additional ground cable between the programming board and the PCB
3. Ensure that both jumpers at CN2 on the programmer board are removed
4. Plug the USB port of the programming board into the computer using a USB cable.
5. Power the RRIV board, using a second USB cable into the RRIV datalogger's USB port. (v0.4.1 boards may also be powered by battery)
6. You may now program the RRIV datalogger and monitor serial using platformio.
7. If the board fails to program, the following two additional steps may help it get into programming mode
8. Connect a Dupont cable between GND on the programmer one of the GND pins on the RRIV datalogger. Typically you may use the GND pin on an open I2C socket.
9. Press the reset button just before the board is programmed. You may do this immediately before or immediately after pressing the 'run' button in platformIO.

## Notes

* The USB port on the RRIV datalogger currently in ONLY for supplying power to the board on the bench. The RRIV datalogger cannot currently be programmed or interacted with through this port.
* In some cases the MCU on the RRIV datalogger may need to be reset in order to program it. The recommended path for this is to power cycle the board.
