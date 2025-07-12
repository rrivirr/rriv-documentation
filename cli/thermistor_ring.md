# Thermistor Ring Protocols

## Thermistor Ring Calibration
* Thermistor ring outputs two sets of values: the raw °C values from the digital thermistors using the factory calibration and the calibrated values using the offset produced by calibration.
* This calibration requires two points to be configured so that a linear calibration can be fit to the raw readings.

### Thermistor Ring Calibration Commands
Note: These commands use RING01 as the id for the configured sensor.  Use the correct id you have configured on your board for the thermistor ring sensor.<br>
Note: Calibration requires two known, stable temperature environments that the sensor can be exposed to.

1. Configure the thermistor ring sensor (skip if already configured)<br>
```rrivctl sensor set RING01 -f configuration/ring_temprature.json```
2. Clear existing calibration<br>
```rivctl calibrate sensor RING01 clear```
3. Place the sensor in a known temperature environment, let it equilibrate, and set the first calibration point  (here we are calibrating when the known temperature is 22.3°C, you must enter the correct temperater for your known temperature environment)<br>
```rrivctl calibrate sensor RING01 point 22.3```
3. Place the sensor in a second, different known temperature environment, let it equilibrate, and set the first calibration point  (here we are calibrating when the known temperature is 19.4°C, you must enter the correct temperater for your second temperature environment)<br>
```rrivctl calibrate sensor RING01 point 19.4```
5. This command will list the current calibration values, which can be used to check your calibration points<br>
```rivctl calibrate sensor RING01 list```
6. Apply the calibration points to the raw data.  A linear model is fit to the raw data.<br>
```rivctl calibrate sensor RING01 fit```
7. Now we can run the command below and we will see all the configs including the calibration.<br>
```rivctl sensor get RING01```
