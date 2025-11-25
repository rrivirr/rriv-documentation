# DF Robot Analog pH Sensor

## Parts needed

* [DFRobot pH Sensor](https://www.dfrobot.com/product-1782.html)
* M20 IP67 Cable Gland (Supplier: [Elecdirect Dome Cap Cable Gland](https://www.elecdirect.com/cord-grips-strain-relief/cable-glands/dome-cap-cable-gland-m20-19-35-black-complete-with-o-ring-locknut))
* Lithium Moly Grease (e.g., [Lucasoil Lithium Grease](https://www.amazon.com/Lucas-Oil-10533-Lithium-Grease/dp/B004X70LZA/ref=asc_df_B004X70LZA/?tag=hyprod-20\&linkCode=df0\&hvadid=312151168520\&hvpos=\&hvnetw=g\&hvrand=12751387308192042965\&hvpone=\&hvptwo=\&hvqmt=\&hvdev=c\&hvdvcmdl=\&hvlocint=\&hvlocphy=9011858\&hvtargid=pla-364752123727\&th=1))
* 22 AWG hook0up wire (e.g., [Adafruit 22AWG Spool Set](https://www.adafruit.com/product/3175?gclid=Cj0KCQiA95aRBhCsARIsAC2xvfzUefNXaZgFmL8MpqskC52_lq_Huy3KYFDuIzKR2XJ_EnG1sNZSfuQaAtqzEALw_wcB))
* [Female 3-pin JST-PH plugs with crimp pins](https://www.amazon.com/CQRobot-Connector-Terminal-Industrial-Integrated/dp/B0731MZCGF)

## Hardware Integration

### Connectivity

* A cable must be built or modified to provide connectivity between the RRIV board and the Gravity analog pH meter. A female 3-pin JST-PH plug should be used for the end connecting to the pH meter. If using a RRIV v0.3 board, a female 3-pin JST-PH plug should be used for the end connecting to the RRIV board. For a RRIV v0.4 board, a female 3-pin _JST-XH_ plug should be used.
* Note: the sequence of pins on the RRIV and pH meter boards differ (see Figure 1). Construction of the cable should should follow the details in Figure 2

![Figure 1: Connecting Gravity analog sensors to the analog to digital converter (ADC) ports. A) RRIV V0.4 board with ADC interfaces indicated; B) Close-up of RRIV ADC interfaces indicating connection configuration; C) Glose up of Gravity pH meter interface. Note the sequence of pins for this connector differs from the sequence on the RRIV board](../../.gitbook/assets/ADC_RRIV_Connect.jpg)**Figure 1:** Connecting Gravity analog sensors to the analog to digital converter (ADC) ports. A) RRIV V0.4 board with ADC interfaces indicated; B) Close-up of RRIV ADC interfaces indicating connection configuration; C) Glose up of Gravity pH meter interface. Note the sequence of pins for this connector differs from the sequence on the RRIV board.

![Figure 2: Connecting Gravity analog sensors to the analog to digital converter (ADC) ports with closeup views of the cables used for connecting.](../../.gitbook/assets/ADC_Gravity_Cable.jpg)**Figure 2:** Connecting Gravity analog sensors to the analog to digital converter (ADC) ports with closeup views of the cables used for connecting.

### Case integration

* The pH sensor is mounted into the sensor plate of the RRIV logger case using a M20 IP67 cable gland (Figure 3).
* Apply lithium moly grease to the cable gland to help ensure a water-tight seal and preserve the life of the cable gland.

![Figure 3: Images showing how the pH sensor is mounted in the sensor plate.](../../.gitbook/assets/sensor_install.jpg)**Figure 3:** Images showing how the pH sensor is mounted in the sensor plate

## Application and CLI Use

### Initial Setup

* Works with the _generic\_analog\_driver_.
* The command `set-slot-config` is used to configure a sensor for use with the RRIV logger:
  * `slot` is a digital slot of data set aside in the EEPROM to hold a sensor configuration
  * `type` is what driver type occupies the slot, these can be found by looking in the registry.cpp and following the "\_TYPE\_STRING" definitions
  * `tag` is a 5 character prefix for column headers, these should be left alone unless there are multiple of the same sensor in a system
  * `burst_size` is the number of reading cycles that should occur per burst
  * `sensor_pin` only for DHT22 currently, indicates which specific GPIO pin is being used for the sensor
  * `adc_select` only for analog sensors, can be either 'internal' or 'external' and indicates whether the analog sensor data is being processed by the ADC in the MCU or the external one
  * `sensor_port` only for analog sensors, indicates which physical port the sensor is occupying
* These can and should be used as they are to setup the AHT, CO2, and CH4 sensors, though once configured should be retained:

```
  set-slot-config {"slot":1, "type":"generic_analog", "tag":"pH", "burst_size":10, "adc_select":"external", "sensor_port":2}
```

* `get-config` is used to check the configuration of the settings as they are, the first section displayed is the datalogger settings followed by sensor slot settings
* The command `set-config` is used to configure sensors and sampling parameters.
  * `loggerName` is a colloquial name that has been written on the back of the board in sharpie
  * `siteName` is a 7 character string to indicate where the RRIV is being deployed, this will also be used in the folder structure of CSV output, so should be unique
  * `deploymentIdentifier` is a 15 character string to indicate what experiment is being run
  * `wakeInterval` is in minutes and determines when the board wakes up to begin measurement cycles. 60 indicates to wake up every hour, 1 indicates every minute. The next interval is calculated at the end of a measurement cycle
  * `startUpDelay` is a duration in minutes to delay before starting the measurement cycle
  * `burstNumber` indicates how many burst cycles to complete during a measurement cycle
  * `interBurstDelay` now also works as an interval given in minutes for when to begin taking readings. 1 indicates to take readings at every minute
* example of set-config that can be further customized. This command sets up a logger named "writeOnBoard" that will wake up after sleeping for 1 minute with

```
set-config {"loggerName":"writeOnBoard", "siteName":"7char", "deploymentIdentifier":"15char", "wakeInterval":1, "startUpDelay":0, "burstNumber":60, "interBurstDelay":1}
```

* To check that all sensors are working properly use `start-logging`. This will display sensor readings at continuous intervals. You can evaluate the readings to confirm the sensor is operating properly. When you are done with this process type the command `stop-logging`. Data will continue logging so the keystrokes you type may become separated, but the command will register if you type the entire command and press enter. The data can be offloaded from the SD card to confirm that data collection was satisfactory.

### pH sensor calibration

* Calibration values are entered manually.
* Begin by typing the command `start-logging`. This will provide a continuous read of raw pH values in millivolts.
* While the sensor is logging, place hte sensor in the first calibration solution.
  * Once the raw voltage measurements have stabilized, record the pH of the calibration solution and the corresponding millivolt value of the sensor.
* Repeat the above step for one or two different other pH calibration solutions.
* Use the `calibrate` command to record the calibration values for the sensor. Each calibration point is entered with the following command, which has three values associated with it.
  * \[sensor slot #] \[step] \[value]
  * The first value, `sensor slot #`, is the slot number previously assigned (in this example slot 1 was used).
  * The second value, `step`, is the pH of the calibration solution.
  * The third value, `value`, is the raw analog reading in millivolts obtained by the sensor.
* Repeat the step above for all 3 calibration points.
