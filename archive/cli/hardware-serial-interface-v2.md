# Hardware Serial Interface

## Overview

This document defines a set of commands for configuring the rriv firmware installed on a compliant PCB.



Command documentation conventions:

* \<required>
* \[optional]
* {...} json blob

RRIV compatible devices are configured using declaritive commands transmitted as JSON over serial as

`{command: <command>, object: <object>, key: value, key: value}`

Commands common to most objects are as follows:

### set

Creates or updates a resource.

### get

Gets current parameters of a resource

### remove

Removes a resource

### list

Lists all resources of a particular type

### calibrate

Performs an (optionally implemented) calibration on a resource





## Datalogger

Data logger identification, timing, and metadata.

#### datalogger set

```
{	
	"object" : "datalogger",
	"command" : "set",
	"logger_name" : "my device",
	"site_name" : "OAK2:,
	"deployment_identifier" : "X12",
	"interactive_logging_interval" : 10,
	"sleep_interval" : 1,
	"start_up_delay" : 1,
	"bursts_per_cycle" : 10,
	"burst_interval" : 2,
	"enable_telemetry" : true
}
```

| Parameter                      | Data Type | Description                                                          |
| ------------------------------ | --------- | -------------------------------------------------------------------- |
| logger\_name                   | string    | a name for the logger                                                |
| site\_name                     | string    | site code                                                            |
| deployment\_identifier         | string    | identify a deployment                                                |
| interactive\_logging\_interval | int       | seconds to wait between measurements during interactive logging      |
| sleep\_interval                | int       | minutes between wakes while deployed                                 |
| start\_up\_delay               | int       | minutes to wait between wakeup and measurement sensor initialization |
| bursts\_per\_cycle             | int       | number of bursts to run during each measurement cycle                |
| burst\_interval                | int       | minutes between burst cycle initialization                           |
| enable\_telemetry              | bool      | enable or disable LoRaWAN telemetry                                  |

#### get datalogger&#x20;

{command: get, object: datalogger}

Get datalogger configuration.&#x20;

#### set datalogger {mode: \<mode\_request>, ...}

{command: set, object: datalogger,&#x20;

Changes the mode the datalogger is in

| Mode Request        | Description                                                                                                       |
| ------------------- | ----------------------------------------------------------------------------------------------------------------- |
| interactive         | Moves to interactive mode, which allows configuration                                                             |
| bench               | Moves to bench mode, which adds continuous serial output of measurements in addition to interactive mode features |
| deploy              | Moves immediately to deployment, sleeps the devices and awaits the next measurement cycle                         |
| deploy \<timestamp> | Moves to wait mode and sleeps the device. When timestamp is reached, the device wakes and deploys                 |



## Sensor

Commands to configure installed sensors.

#### set sensor \<id> {...}

Creates or updates a sensor configuration. If a sensor with the provided id is currently configured, it is updated. Otherwise, a new sensor configuration is created.

The JSON blob can contain some or all configuration parameters for indicated sensor driver. "type" specifies the kind of sensor installed and its corresponding driver, and is required when creating a new sensor.

Example (for generic analog sensor):

```
{	
	"type":"generic_analog",
	"burst_size":10,
	"adc_select":"internal",
	"sensor_port":1,
}
```

#### get sensor \[id] \[{property: }]

* rrivctl shorthand get sensor \[id] \[property]

Get a sensor configuration, corresponding to the id. When called with a parameter argument, returns just the parameter requested. Otherwise returns the entire JSON blob.

If id is not specified, returns a JSON array containing all sensor configurations.

get sensor also supports an aggregate property 'calibration' which returns all calibration parameters only

```
{
	'high_val': 5,
	'low_val': 2,
	'high_read': 2000,
	'low_read' : 300,
	'm': 2,
	'b': 0.2
}
```

#### rm sensor \<id>

Remove the sensor configuration matching the corresponding id

#### ls sensor

List all configured sensors in a tabluar format

#### calibrate sensor \<id> {action: $action, ...}

**action: point**

Sets a calibration point

`calibrate sensor <id> point {point: \$point_value, tag: $tag}`

**action: list, ls**

Lists all the calibration points currently registered

`calibrate sensor <id> list`

**action: remove, rm**

Removes a registered calilbration point

`calibrate sensor <id> remove {tag: $tag}`

**action: fit**

Calculates fit based on calibration points that have been registered, and stores the fit.

`calibrate sensor <id> fit { type: 'linear'}`

#### reset sensor {property: $property}

* reset sensor
* reset sensor {property: $property}
* reset sensor {property: 'calibration'}
* rrivctl shorthand: reset sensor $property

### Telemeter

Summary: telemeter set, get, rm, ls

#### set telemeter \[id] {...}

Creates or updates an telemeter configuration. If an actuator with the provided id is currently configured, it is updated. Otherwise, a new sensor configuration is created.

#### get telemeter \<id> \[parameter]

Get a actuator configuration, corresponding to the id. When called with a parameter argument, returns just the parameter requested. Otherwise returns the entire JSON blob.

If id is not specified, returns a JSON array containing all telemeter configurations.

#### rm telemeter \<id>

Remove the telemeter configuration matching the corresponding id

#### ls telemeter

List all configured telemeters in a tabluar format

#### reset telemeter {property: $property}

### Board

The commands access features of the board itself and firmware metadata

This consists of three types of commands

* get/set commands in the standard that report hardware properties.
* warranty/license shorthands for human operators on the serial connection
* debugging shorthands for human developers on the serial connection

This is a custom namespace at the top level.

#### board version

```
get board { property: 'version'}
```

rrivctl: get board version

#### board firmware warranty

```
get board { property: 'firmware-warranty'}
get board { property: 'firmware'}
```

#### board firmware conditions

#### board firmware license

#### board rtc set \<epoch>

```
set board {'epoch': \$epoch} 
```

Set real time clock epoch time

#### board rtc get

Get the current real time clock epoch time stored on a RRIV device

```
get board { property: 'epoch'}
```

## Run Mode

```
{
 "command-set" : "board",
 "command" : "restart"
}
```

```
{
 "command-set" : "board",
 "command" : "stop"
}
```

```
{
 "command-set" : "board",
 "command" : "sleep"
}
```

```
```

### board list

```
{
    "command-set" : "board",
    "command" : "list"
    "object" : "i2c"
}
```

### Check

```
{
   "command-set" : "board",
   "command" : "list",
   "object" : "memory"
}
```

### board set power&#x20;

| Signal   | Description                          |
| -------- | ------------------------------------ |
| exADC    | enable/disable exADC                 |
| 3v3Boost | enable/disable 3v3 boost converter   |
| intADC   | enable/disable power to intADC ports |

### Various Commands

<table><thead><tr><th width="112.890625">set</th><th>command</th><th>object</th><th>params</th></tr></thead><tbody><tr><td>board</td><td>restart</td><td></td><td></td></tr><tr><td>board</td><td>sleep</td><td></td><td></td></tr><tr><td>board</td><td>stop</td><td></td><td></td></tr><tr><td>board</td><td>list</td><td>i2c</td><td></td></tr><tr><td>board</td><td>read</td><td>clock</td><td></td></tr><tr><td>board</td><td>read</td><td>version</td><td></td></tr><tr><td>board</td><td>list</td><td>adc</td><td></td></tr><tr><td>board</td><td>write</td><td>epoch</td><td></td></tr><tr><td>board</td><td>read</td><td>epoch</td><td></td></tr><tr><td>board</td><td>write</td><td>gpio</td><td>id, &#x3C;high, low></td></tr><tr><td>board</td><td>read</td><td>gpio</td><td>id</td></tr><tr><td>board</td><td>read</td><td>power_ctl</td><td>&#x3C;on, off></td></tr><tr><td>board</td><td>write (switch)</td><td>power_ctl</td><td>id, &#x3C;on, off></td></tr><tr><td>board</td><td>save (write)</td><td>power_ctl</td><td>id, &#x3C;on, off></td></tr><tr><td>board</td><td>list</td><td>power_ctl</td><td></td></tr><tr><td>board</td><td>get</td><td>adc</td><td>&#x3C;ex, int>, [port]</td></tr><tr><td>board</td><td>get</td><td>eeprom</td><td></td></tr><tr><td>board</td><td>write</td><td>i2c</td><td></td></tr><tr><td>board</td><td>set</td><td>watchdog</td><td>[iwd, int], timeout </td></tr><tr><td>board</td><td>write</td><td>serial</td><td>&#x3C;message></td></tr><tr><td>board</td><td>read</td><td>serial</td><td>&#x3C;message></td></tr></tbody></table>

### Device

Top level commands that dump and load all for the device in one payload

#### get

#### set

#### reset \<STM\_ID>
