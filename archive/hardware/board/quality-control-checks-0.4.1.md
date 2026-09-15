# Quality Control Checklist

## Checklist
* [pass] Powers up over USB
* [pass] Programmable
* [pass] Serial
* [pass] RGB LED
* [mod] Switchable power cycling
* [pass] 2.4V boost converter
* [pass] 3.3V boost converter
* [pass] 5V boost converter
* [pass] VIN measure
* [pass] intADC
* [pass] exADC
* [ ] I2C 3.3V
* [pass] I2C 5V
* [pass] exADC MOSFET
* [pass] Battery level MOSFET 
* [pass] intADC MOSFET
* [ ] Wake switch
* [mod] Voltage ORing VDD
* [pass] Voltage ORing 3.3V

## Noted Defects
* Orientation of reset button still wrong
  * Mitigation: remove reset button	
  * Alternate: may be possible to disconnect pads diagonally and get intended functionality
* Switchable power cycling resets on set low
  * Root cause: both ideal diodes are turning off at threshold
  * Mitigation: replace R21 with 357K
  * Fix: use mitigation or use ST pin on ideal diode for synchronized switching
* i2c hangs
  * this appears to be due to going low when 3v3 is switch off.
  * Fix: pullups should be agains VDD, not 3V3 

## Other Notes
* When VIN measure is disable, the ADC still reads a nonzero value
  * Suspect this is a floating voltage, test using current meter
* 5V boost has a very limited swing, around 100mV.  Still, the ripple pattern is spiky.  We could add a ferrite bead to smooth it.  This could go in the place of SB27 to feed the the exADC with smooth 5v.  To feed i2c we could place a bead in a similar solder bridge location.
* BOM included wrong pin count socket for J11 and J12
