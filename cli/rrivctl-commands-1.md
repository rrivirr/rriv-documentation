# rrivctl commands v2

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

Sets parameters relevant to the entire datalogger.\
\
These may be set individually, or read from a json file to set multiple parameters in one command invocation.

Setting a parameter individually:\
`set datalogger logger_name water2`

Use the -f option to load multiple parameters from a stored file:\
`set datalogger -f configurations/stored_datalogger.json`

#### All datalogger parameters

<table><thead><tr><th>Parameter</th><th width="142.9453125">Data Type</th><th>Description</th></tr></thead><tbody><tr><td>logger_name</td><td>string</td><td>a name for the logger</td></tr><tr><td>site_name</td><td>string</td><td>site code</td></tr><tr><td>deployment_identifier</td><td>string</td><td>identify a deployment</td></tr><tr><td>interactive_logging_interval</td><td>int</td><td>seconds to wait between measurements during interactive logging</td></tr><tr><td>sleep_interval</td><td>int</td><td>minutes between wakes while deployed</td></tr><tr><td>start_up_delay</td><td>int</td><td>minutes to wait between wakeup and measurement sensor initialization</td></tr><tr><td>bursts_per_cycle</td><td>int</td><td>number of bursts to run during each measurement cycle</td></tr><tr><td>burst_interval</td><td>int</td><td>minutes between burst cycle initialization</td></tr><tr><td>enable_telemetry</td><td>bool</td><td>enable or disable LoRaWAN telemetry</td></tr><tr><td>mode</td><td>string</td><td>changes the mode the datalogger is in. normally called as a single parameter command</td></tr></tbody></table>

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

### get datalogger

#### Synopsis

```
rrivctl get datalogger
```

#### Description

Get datalogger configuration. This command returns all datalogger configuration parameters as a JSON blob.

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

### get sensor

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

Subcommands to perform calibration steps on individual sensors. These subcommands are used to set, view, and remove calibration points, and to perform the fit as implemented by the sensor driver. The basic workflow is to add the number of calibration points required by the sensor driver, and then perform a fit.\\

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

<table><thead><tr><th width="119.7265625">Parameter</th><th width="124.6875">Data Type</th><th>Description</th><th>Response</th></tr></thead><tbody><tr><td>epoch</td><td>integer</td><td>Epoch time</td><td>seconds (integer)</td></tr><tr><td>version</td><td>json</td><td>board and firmware versions</td><td>{<br>"hv":"0.4.2",<br>"fv":firmware_version,<br>"br":branch,<br>"ref":gitref<br>}</td></tr></tbody></table>





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

Logs output from measurement cycle and telemetry events to the console. Exit watch mode using Control-C. Note that other commands cannot be sent to the device while watch is running.

Watch output is in CSV format and contains all sensor values currently configured to measure.

#### Options:

-d, --debug enabled debugging output (default: false)\
-f, --file name of a file to output sensor data to\
-p, --path \<serial\_path> serial path of the RRIV device\
\--project a project name for organizing watch files\\

## Connect

### connect

#### Synopsis

```
rrivctl connect
```

#### Description

Opens the USB serial connection with the rriv board and firmware.

## Cheat Sheet

```
rrivctl connect

rrivctl get datalogger 
rrivctl set datalogger <parameter> <value>
 
rrivctl list sensor 
rrivctl set sensor <sensor_id> -f <filename.json>
rrivctl get sensor <sensor_id> 
rrivctl remove sensor <sensor_id> 
rrivctl calibrate sensor <sensor_id> point <value> 
rrivctl calibrate sensor <sensor_id> list 
rrivctl calibrate sensor <sensor_id> fit

rrivctl get board version 
rrivctl get board epoch 
rrivctl set board epoch <epoch_time>  

rrivctl get device 

rrivctl watch
```

##

## Library Subcommand Set

### library save

#### Synopsis

```
rrivctl library save <sensor|datalogger|device> <tag> [-s|--sensor-id sensor_id] [-f|--filename filename.json]
```

#### Description

Saves a sensor, datalogger, or full device configuration with a **tag** for future reuse.  The first argument to the save subcommand is **configuration type**, which determines the type of configuration to save.

The configuration to be saved can loaded from a json file, an attached device, or the history of a device in the rriv database.  When the -f option is specified, the configuration is loaded and saved from the referenced file, without any changes to any attached device.  When -f is not specified, configuration is read from a device attached over USB.  Configuration type sensor requires the -s option if -f is not specified, in order to indicate which sensor configuration to read from the attached device.

#### Options

**-f, --filename**

&#x20;   Specify a json file containing configuration to save. &#x20;

**-s, --sensor\_id**

&#x20;   Specify the sensor id, required when reading sensor configuration from a device over USB

**-d, --device-id**

&#x20;   Get the configuration to tag from device other than the currently attached device.

**-t YYYY:MM:DD\[-HH:MM}**

&#x20;   Specify the timestamp for a configuration stored in history for either the currently attached device or another device the user has access to in the rriv database, and tag this historical configuration with the specified tag.



### library apply

#### Synopsis

```
rrivctl library apply <sensor|datalogger|device> <tag|repository[:version]> [-s|--sensor-id sensor_id]
```

#### Description

Applies a saved library configuration to the attached device, as specified by saved tag.   The first argument to the save subcommand is **configuration type**, which indicated the type of configuration to look up in the library.<br>

The configuration to apply may be determined by tag or repository.  A tag is attached to a configuration by the library save command, and is private to the user.  When a user uses the library publish command to make a library available to other users, the configuration is published a repository, where is versioned.  These configurations may be applied by specifying the repository name, and an optional version number.  If a version number is not specified, then the latest configuration published to the repository is applied.

Repositories have an optional owner prefix, as \[owner:]\<repository>, which specified the owner of the repository.  When owner is not specified, the current user is used as the owner. &#x20;

#### Options

**-s, --sensor\_id**

&#x20;   Optionally a sensor id to create or update when applying a tagged sensor configuration.  If this option is not set, then a sensor id is automatically generated.





### library publish

#### Synopsis

```
rrivctl library publish <sensor|datalogger|device> <repository> [-s,--sensor-id sensor_id] [-t,--tag tag] [-n,--note note]
```

#### Description

Makes a sensor, datalogger, or device configuration available for use by other users via the library apply subcommand.  The configuration to publish may read directly from an attached device, or may be specified by a previously saved tag.  A repository name is always specified.  If a repository does not already exist in the cloud storage, it will be automatically created.

If not tag is specified, then the configuration is read off the attached device.

Versions are computed automatically, as monotonically increasing integers.

#### Options

**-n, --note**

&#x20;   Store a descriptive note with the published version

**-s, --sensor\_id**

&#x20;   Specify the sensor id, required when reading sensor configuration from a device over USB

**-t, --tag**

&#x20;   When specified, published the configuration stored under this tag to the named repository



### library list

#### Synopsis

```
rrivctl library list <sensor|datalogger|device>
rrivctl library list repository [repository]
```

#### Description

List contents of configuration tags and repositories.

When sensor, datalogger, or device configuration type list is specified, then all tags belonging to the current user are displayed.

When repository list is specified, all repository names accessible to the current user are listed.  If the further specific repository name is specified, then all versions and their corresponding notes are listed.

Repositories have an optional owner prefix, as \[owner:]\<repository>, which specified the owner of the repository.  When owner is not specified, the current user is used as the owner. &#x20;

####



### library get

#### Synopsis

```
rrivctl library get <sensor|datalogger|device> <tag|repository[:version]>
```

#### Description

Query and display library configurations, but do not apply to any attached device.

The first argument specifies the configuration type.

The second argument is either a named tag or a respository to read the confirmation from.  If no version is specified when repository is specified, then the latest version is shown.<br>

Output of history get may be redirected to a file in order to store the configuration as a json file, for instance `rrivctl library get datalogger wetland > wetland_datalogger.json`<br>



## History Subcommand Set

### history list

#### Synopsis

```
rrivctl history list <sensor|datalogger|device> 
        [-d,--device-id device_id] [-s,--sensor-id sensor_id]
        [-n entries]
```

#### Description

List history of configuration changes for sensor, datalogger, or device configurations.&#x20;

Output is tabluar, showing the time of the configuration change followed by the configuration changes made.

#### Options

**-d, --device-id**

&#x20;  The device to list configuration history for.  If this option is not specified then the history of the currently attached device is listed.&#x20;

**-n**&#x20;

&#x20;   The number of entries to show at once.

**-s, --sensor\_id**

&#x20;   Specify the sensor id, required when listing sensor configuration history



### history get

#### Synopsis

```
rrivctl history get <sensor|datalogger|device> <YYYY:MM:DD>[THH:MM]
        [-d,--device-id device_id] [-s,--sensor-id sensor_id]
      
```

#### Description

Show the full sensor, datalogger, or device configuration on a given date and time

Specifying a date is mandatory, however time is optional.  If a time is not specified then the configuration display should be the most recent configuration before the the start of the specified date.

Output of history get can be redirected to a file in order to store the configuration as a json file, for instance `rrivctl history get device wetland 2024-11-01T12:00 > desert_device.json`

#### Options

**-d, --device-id**

&#x20;  The device to list configuration history for.  If this option is not specified then the history of the currently attached device is listed.&#x20;

**-s, --sensor\_id**

&#x20;   Specify the sensor id, required when listing sensor configuration history



### history apply

#### Synopsis

```
rrivctl history apply <sensor|datalogger|device> <YYYY:MM:DD>[THH:MM] [-d,--device-id device_id] [-s,--sensor-id sensor_id]
      
```

#### Description

Apply the full sensor, datalogger, or device configuration from a given date and time to the currently attached device.  Historical configurations to apply can be queried from either the currently attached device or any other device the user has access to.

#### Options

**-d, --device-id**

&#x20;  The device history to query to get the configuration to apply.  If this option is not specified then the history of the currently attached is used to query the configuration to apply.

**-s, --sensor\_id**

&#x20;   Specify the sensor id, required when listing sensor configuration history

