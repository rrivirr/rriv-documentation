# Board Configuration


## Solder Bridges

Solder bridges, also know has jumpers, allow the board to be placed in alternative electrical configurations.  
They are marked with the reference designator prefix 'SB' and are placed exclusive on the back side of the board.
They often occur in pairs that must not both be connected. Certain solder bridges come pre-installed with a zero
ohm resistor in a default configuration.  The configuration is changed by removing the resistor, and connecting alternative
configurations is done by either installation of a zero ohm resistor on the solder bridge of interest, or simply connected both
pads of the bridge with solder.

### Selection of voltage supply for external ADC

* SB27 - Power VREF on the external ADC from the 5V rail
* SB28 - Power VREF on the external ADC from the 3.3V rail

Note: SB27 and SB28 are mutually exclusive and must not both be installed.

Note: The 5V rail is not powered by default on v4.0.2 boards.  An external supply must be routed to supply this rail.

### Selection of primary voltage supply for I2C bus

* SB25 - Power the power pin on I2C ports from the 5V rail
* SB26 - Power the power pin on I2C ports from the 3.3V rail

Note: SB25 and SB26 are mutually exclusive and must not both be installed.

Note: The 5V rail is not powered by default on v4.0.2 boards.  An external supply must be routed to supply this rail.

### Selection of secondary voltage supply for I2C bus

The 4th I2C port, J6, can be configured to supply 3.3V on its power pin even though the SB25, the 5V selection for the I2C ports, is installed.



### Power routing

...




