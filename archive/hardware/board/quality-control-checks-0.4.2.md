# Quality Control Checklist

[x] Powers up over USB
[DNI] RGB LED
[ ] 2.4V boost converter
[ ] 3.3V boost converter
[DNI] 5V boost converter
[ ] Switchable power from battery
[x] intADC
[ ] exADC
[x] I2C 3.3V
[ ] I2C 5V
[ ] exADC MOSFET
[ ] Battery level MOSFET 
[ ] intADC MOSFET
[ ] Wake switch
[x] RTC set 
[x] RTC battery power

# Noted Defects
* Tab on U15 is connected to pin 2, incorrectly connected to ground
  * Mitigation: remove component, cut three traces, replace component.
* The USB port can break off easily
  * Mitigation: use a USB cord with less agressive holds
  * Final solution: epoxy
* The 5v default solder bridge supplying VDD to exADC causes i2c to hang
  * Mitigation: Change the default to 3v3
  * Solution: build the 5v boost daughter board
* i2c is set up to default to 5v, but no 5v supply 

# Other Notes
* Text labeling solder bridges should be bigger 
* Some solder bridges missing their text labeling
* Reed switch breaks easily
* Better access to USB 5V ?
* USB C port
* Need a way to wipe the EEPROM
* Leaving off a diagnostic LED as a bad move!

