# rrivctl commands

## Overview

This document defines a set of commands offered by the rrivctl command line interface to configure devices compliant with the rriv hardware serial interface.



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

Gets current parameters of a resource

### remove

Removes a resource

### list

Lists all resources of a particular type

### calibrate

Performs an (optionally implemented) calibration on a resource



## Datalogger

### set datalogger

#### Synopsis

```
set datalogger [option] <property> <value>
```

#### Description

Sets parameters relevant to the entire datalogger.  \
\
These may be set individually, or read from a json file to set multiple parameters in one command invocation.

Setting a parameter individually:\
`set datalogger logger_name water2`

Use the -f option to load multiple parameters from a stored file:\
`set datalogger -f configurations/stored_datalogger.json`

#### All datalogger parameters

<table><thead><tr><th>Parameter</th><th width="142.9453125">Data Type</th><th>Description</th></tr></thead><tbody><tr><td>logger_name</td><td>string</td><td>a name for the logger</td></tr><tr><td>site_name</td><td>string</td><td>site code</td></tr><tr><td>deployment_identifier</td><td>string</td><td>identify a deployment</td></tr><tr><td>interactive_logging_interval</td><td>int</td><td>seconds to wait between measurements during interactive logging</td></tr><tr><td>sleep_interval</td><td>int</td><td>minutes between wakes while deployed</td></tr><tr><td>start_up_delay</td><td>int</td><td>minutes to wait between wakeup and measurement sensor initialization</td></tr><tr><td>bursts_per_cycle</td><td>int</td><td>number of bursts to run during each measurement cycle</td></tr><tr><td>burst_interval</td><td>int</td><td>minutes between burst cycle initialization</td></tr><tr><td>enable_telemetry</td><td>bool</td><td>enable or disable LoRaWAN telemetry</td></tr><tr><td>mode</td><td>string</td><td>changes the mode the datalogger is in.  normally called as a single parameter command</td></tr></tbody></table>

#### Datalogger modes

| Mode        | Description                                                                               |
| ----------- | ----------------------------------------------------------------------------------------- |
| interactive | Moves to interactive mode, which allows configuration                                     |
| field       | Moves immediately to deployment, sleeps the devices and awaits the next measurement cycle |

#### Example datalogger configuration file

```
{	
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



### get datalogger&#x20;

#### Synopsis

```
rrivctl get datalogger
```

#### Description

Get datalogger configuration.   This command returns all datalogger configuration parameters as a JSON blob.





## Sensor

Commands to configure installed sensors.

### set sensor

#### Synopsis

```
 set sensor <sensor_id> -f <FILE>
```

#### Description

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

###

### get sensor&#x20;

#### Synopsis

```
get sensor <sensor_id>
```

#### Description

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

### remove sensor

#### Synopsis

```
remove sensor <sensor_id>  
```

#### Description

Remove the sensor configuration matching the corresponding id

### list sensor

#### Synopsis

```
list sensor 
```

#### Description

List all configured sensors

####

### calibrate sensor

#### Synopsis

```
calibrate sensor <id> <subcommand> [params...]
```

#### Description

Subcommands to perform calibration steps on individual sensors.  These subcommands are used to set, view, and remove calibration points, and to perform the fit as implemented by the sensor driver.  The basic workflow is to add the number of calibration points required by the sensor driver, and then perform a fit.\


**Example calibration workflow**

```
rrivctl calibrate sensor TEMP point 12.3   # set a calibration point at 12.3°  
rrivctl calibrate sensor TEMP point 25.3   # set a calibration point at 25.3°
rrivctl calibrate sensor list              # list calibration points        
rrivctl calibrate sensor fit               # perform the calibration fit
rrivctl watch                              # watch outputs on the console
```



**Subcommand: point**

Sets a calibration point

```
calibrate sensor <sensor_id> point <value>
```



**Subcommand: list**

Lists all the calibration points currently registered

```
calibrate sensor <sensor_id> list
```



**Subcommand: fit**

Calculates fit based on calibration points that have been registered, and stores the fit.

```
calibrate sensor <sensor_id> fit 
```



## Board

The commands access features of the board itself and firmware metadata

This consists of three types of commands

* get/set commands in the standard that report hardware properties.
* warranty/license shorthands for human operators on the serial connection
* debugging shorthands for human developers on the serial connection

This is a custom namespace at the top level.

### get board

#### Synopsis

{% code fullWidth="false" %}
```
rrivctl get board [version,epoch]
```
{% endcode %}

#### Description

Get the parameters specific to the board

| Parameter | Data Type | Description                 |
| --------- | --------- | --------------------------- |
| epoch     | integer   | Epoch time                  |
| version   | json      | board and firmware versions |

###

### set board

#### Synopsis

```
rrivctl set board epoch <epoch_time>
```

#### Description

Set real time clock epoch time

####

## Device

Commands relevant to the entire device

### get device

Get details about the device, including unique identifiers and hardware assignment status.

```
rrivctl get device
```

```
{
"gpio_bound": {
"gpio1": "",
"gpio2": "",
"gpio3": "disabled",
"gpio4": "disabled",
"gpio5": "",
"gpio6": "",
"gpio7": "",
"gpio8": "",
"usart": ""
},
"serial_number": "A0000",
"uid": "FF325D93737554657136931"
}
```

## Watch

### watch

#### Synopsis

```
rrivctl watch [OPTIONS]
```

#### Description

Watch data output and optionally log to an output file.

Logs output from measurement cycle and telemetry events to the console.  Exit watch mode using Control-C.  Note that other commands cannot be sent to the device while watch is running.

Watch output is in CSV format and contains all sensor values currently configured to measure.

#### Options:

-d, --debug enabled debugging output (default: false)\
-f, --file name of a file to output sensor data to\
-p, --path \<serial\_path> serial path of the RRIV device\
\--project a project name for organizing watch files\


###
