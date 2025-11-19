# Troubleshooting

## Board won't flash

1.  Unplug and replug all cables
2.  Check cables.
3.  Is the core locked up?
    1.  "The core is in locked up status as a result of an unrecoverable exception ERROR"
    2.  You need to 'connect under reset'
        1.  Fix 1: Randomly press the reset button at just the right moment will flashing the board
            1.  This one works within vscode
        2.  Fix 2: Call probe-rs with the connect under reset flag
            1.   This one needs a special script
            2.  probe-rs download board/target/thumbv7m-none-eabi/debug/app \\  
                        --chip STM32F103RE \\  
                        --protocol swd \\  
                        --connect-under-reset \\  
                        --allow-erase-all \\  
                        --chip-erase
                
            3.  You need to probe-rs command line tool installed for this
            4.  Scripts are stored in https://github.com/rrivirr/rriv-utilities
4.  Is the jlink able to talk to the MCU
    1.  Type 1: Can't connect to the MCU
        1.  The MCU might not be power check power cables
    2.  Type 2: Connected, but had a problem talking to the MCU
        1.  "A protocol error occurred in the SWD communication between probe and device".
        2.  The Jlink has crashed or is not plugged in correctly.
    3.  Solutions:
        1.  Is the Jlink plugged in properly, note: the cable can be plugged in upside down
        2.  Is the board powered
        3.  Is the Jlink powered
        4.  If all of the above are true, you need unplug cables and power cycle, and it will eventually work.
        5.  If all else fails, try pressing the reset button at just the right time.

&nbsp;

## Board won't connect or start

### rrivctl connect doesn't work

1.  rrivctl connect doesn't find the board
    1.  look for the serial port in /dev
        1.  what's in /dev/serial
        2.  what's in /dev/ttyACM\*
        3.  connect to the board using rrvictl connect -p /dev/ttyACM\* or /dev/serial/by-id/{the id that is there} 

&nbsp;

### after trying the above, still can't connect to the board or view rrivctl watch

1.  Capture the probe-rs debug logs
    1.  Method 1: use the 'attach' launch task in vscode
    2.  Method 2: use a script that is found in https://github.com/rrivirr/rriv-utilities
        1.  probe-rs attach board/target/thumbv7m-none-eabi/debug/app \\  
                    --chip STM32F103RE \\  
                    --protocol swd \\  
                    --allow-erase-all \\  
                    --chip-erase
            
2.  Does the board finish setup, or is it crashing and restarting
3.  If it does not finish setup
    1.  Unplug all your sensors
        1.  If the board starts, it's an electrical problem with your sensors 
    2.  Check all electrical configurations on the board
        1.  Are the VDD/voltage levels all correct - 3.3V vs 5V vs no power
            1.  For your sensors
            2.  For any other thing that is plugged in
            3.  Are jumper wires installed correctly
                1.  Extra jumper wire to supply 5V from USB5V - is it installed
                    1.  This wire can be soldered permanently on the bottom of the board
            4.  Is the blue LED on board on?
                1.  If this LED is not on, you have short circuit or no power supply
        2.  Are the solder bridges correctly configured for your use case
            1.  SB25/SB26 control voltage supply to I2C sensors
            2.  ......  control voltage supply to exADC ports
            3.  SB6 enables the ex5V pin, if that is needed
            4.  Check the manual that lists all the solder bridges on the board
        3.  Are sensors wired/plugged in correctly
            1.  Note: sometimes they can be plugged in upside down
    3.  Verify your firmware version, or install known working version
        1.  Unless you are doing firmware development, use rrivctlv2 to install firmware
        2.  rrivctlv2 flash v1.1.0
        3.  versions are listed here: https://github.com/rrivirr/rriv-firmware/releases
    4.  Check the logs for explicit hardware failures, such as
        1.  EEPROM not installed properly or wrong EEPROM
        2.  DS3231 broken (real time clock chip)
        3.  Other conditions

### board starts but doesn't log data

1.  Check that drivers are configured correctly
    1.  rrivctl list sensor
    2.  rrivctl get sensor &lt;ID&gt;
2.  Use a different physical sensor to diagnose sensor hardware failure
3.  Make sure you have the right driver software for your hardware

&nbsp;
