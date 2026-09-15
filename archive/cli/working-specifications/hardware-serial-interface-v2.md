---
description: >-
  This document defines a set of commands for configuring the rriv firmware
  installed on a compliant PCB.
---

# Hardware Serial Interface Original Spec

## Overview

Command documentation conventions:

* \<required>
* \[optional]
* {...} json blob

RRIV compatible devices are configured using declarative commands as

`<command> <object> {key: value, key:value}`

or

`{command: <command>, object: <object>, key: value, key: value}`

Commands common to most objects are as follows:

### set

Creates or updates a resource.

### get

Gets current parameters of a resource, in a machine readable format.

### rm

Removes a resource

### reset

Resets parameters of an object back to defaults. Can accept a property to focus reset on that property.

### ls

Lists all resources of a particular tyle, in a tabular human readable format. This is not part of the standard, but implemented for ease of development. rrivctl does support this command, but by calling `get` and filtering the results down to a human readable format.

Consider if ls should be an abbreivate response for telemetry reasons, as in an index of objects without full properties.

### calibrate

Any object can potentially support a calibration routine

### run

Custom actions

## Commands

### Datalogger

Configurate data logger timing and metadata.

#### set datalogger {...}

{...} is JSON blob tha contains one or more datalogger parameter variables

```
{	
	"logger_name":"my device",
	"site_name":"OAK2:,
	"deployment_identifier":"X12",
	"interval": 10,
	"burst_number": 10,
	"start_up_delay": 1,
	"burst_delay": 2,
	"user_note": "none",
	"user_value": 12
}
```

| Parameter              | Data Type | Description                                                          |
| ---------------------- | --------- | -------------------------------------------------------------------- |
| logger\_name           | string    | a name for the logger                                                |
| site\_name             | string    | site code                                                            |
| deployment\_identifier | string    | identify a deployment                                                |
| wake\_interval         | int       | minutes between wakes while deployed                                 |
| warm\_up\_delay        | int       | minutes to wait between wakeup and measurement sensor initialization |
| burst\_interval        | int       | minutes between burst cycle initialization                           |
| user\_note             | string    | a note to add to each reading                                        |
| user\_value            | int       | a value to add to each reading                                       |

#### get datalogger \[{property: $property}]

* get datalogger \[property]

{command: get, object: datalogger, parameter: \<parameter>}

Get datalogger configuration. When called with a parameter argument, returns just the parameter requested. Otherwise returns the entire JSON blob.

#### reset datalogger \[{property: $property}]

* reset datalogger \[property]

Resets datalogger to factory default configuration, or just resets a particular property.

#### set datalogger {mode: \<mode\_request>, ...}

Changes the mode the datalogger is in

| Mode Request        | Description                                                                                                       |
| ------------------- | ----------------------------------------------------------------------------------------------------------------- |
| interactive         | Moves to interactive mode, which allows configuration                                                             |
| bench               | Moves to bench mode, which adds continuous serial output of measurements in addition to interactive mode features |
| deploy              | Moves immediately to deployment, sleeps the devices and awaits the next measurement cycle                         |
| deploy \<timestamp> | Moves to wait mode and sleeps the device. When timestamp is reached, the device wakes and deploys                 |

Datalogger also supports a shorthand which is outside the standard for mode switching over direct serial\
connection:

```
mode <mode_request>
```

### Sensor

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

#### board restart

```
run board {'commmand' : 'restart'}
```

#### board i2c ls

#### board memory check

#### board mcu \[stop,sleep]

#### board signal \[high,low]

| Signal   | Description                        |
| -------- | ---------------------------------- |
| exADC    | enable/disable exADC               |
| 3v3Boost | enable/disable 3v3 boost converted |

### Device

Top level commands that dump and load all for the device in one payload

#### get

#### set

#### reset \<STM\_ID>
