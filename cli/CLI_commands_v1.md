# V1 CLI Commands - Legacy

## Overview

Command structure:
* `<command> [arguments]`

## Commands
### `<help>`
List all commands

### `<show-warranty>`
Display warranty information

### `<show-conditions>`
Display licensing information

### `<get-config>`
List the general datalogger settings followed by each slot configuration

### `<set-config> [JSON]`
Set the general datalogger configuration using a JSON which includes:
```
{
  "loggerName":[7 characters],
  "siteName":[7 characters],
  "deploymentIdentifier":[15 characters],
  "wakeInterval":[value in minutes],
  "startUpDelay":[value in minutes],
  "burstCycle":[value],
  "interBurstDelay":[value in minutes]
}
```
Example:
`set-config {"loggerName":"CAL3","siteName":"bucket3","deploymentIdentifier":"cold-cal1.3","wakeInterval":1,"startUpDelay":0,"burstNumber":60,"interBurstDelay":1}`

### `<set-slot-config> [JSON]`
Set the slot configuration, all slots have:
```
{
  "slot":[value],
  "type":[sensor type],
  "tag":[5 characters],
  "warmup":[value in seconds],
  "readingCycle":[value]
}
```
Additional items may be added depending on sensor type, current sensor types:
* generic_analog
* atlas_ec
* driver_template
* adafruit_dht22
* atlas_co2
* BME280
* adafruit_ahtx0

### `<clear-slot> [slot #]`
Clear the slot configuration for a specific slot #, number of slots is determined by size of EEPROM and value set for `EEPROM_TOTAL_SENSOR_SLOTS` in system/eeprom.h

### `<get-rtc>`
Get the current time in epoch and ISO8601

### `<set-rtc> [epoch timestamp]`
Set the DS3231 real time clock value

### `<calibrate> [sensor slot #]`
#### `<calibrate> [sensor slot #] [step] [value]`
Calibration commands for a sensor slot, generic analog driver calibration steps are `low` and `high` for a two-point calibration resulting in a linear relationship y=mx+b

### `<set-user-note> [note]`
Populate userNote column in CSV, will continuously populate with `[note]` until `[note]` is replaced

### `<set-user-value> [value]`
Populate userValue column in CSV, will continuously populate with `[value]` until `[value]` is replaced

### `<start-logging>`
Beging serial output of reading samples from configured sensors, 1 reading every 2 seconds

### `<stop-logging>`
Stop serial output of sensor reading samples

### `<deploy-now>`
Switch to deployment mode--wake at next interval and begin measurement cycles until running out of power

### `<i>`
Switch to interactive mode for user input

### `<restart>`
Restart the firmware
