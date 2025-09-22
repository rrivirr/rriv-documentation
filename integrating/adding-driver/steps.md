# Steps

The driver class creation script will create a .h file with all necessary variables and functions to define the class, and a .ccp file that contains stubs for all functions that need to be implemented. Implementing a driver thus then proceeds by writing logic into the function stubs in the .cpp file, and no modifications to the generated .h file are necessary except where explicitly described in this document.

The new C++ class file created by the driver template script contains the complete skeleton of variables and functions needed to create a working driver for your sensor. However, some functions and variables will need to be updated to complete the implementation of the driver. Other functions and variables only need to be updated to implement optional features. There are also functions and variables that do not need to be updated at all, they are just part of the driver skeleton code itself.

An approach to updating necessary functions and variables should proceed as follows:

1. Implement sensor setup and measurement functionality.
2. Implement data output functionality.
3. Implement sensor specific configuration functionality (optional).
4. Implement callibration functionality (optional).

## Implement sensor setup and measurement functionality.

Sensor setup and measurement functionality is implemented by updating the following functions:

1. setup()
2. stop()
3. isWarmedup()
4. takeMeasurement()

### setup()

The _setup()_ function should preform any logic that is needed to start collecting readings from the sensor. An analog sensor typically has no setup logic. iDigital sensors, such as I2C, SPI, or GPIO protocol sensors, often _will_ have commands that must be sent to them to start collecting readings, or select certain functionality. Details on this can be found in the documentation for the sensor being integrated. This logic all goes in the setup() function.

### stop()

_stop()_ is called for each sensor right before the datalogger goes to sleep between measurement cycles. Some digital sensors have specific logic for halting readings, or have specific low power modes. Any related logic from the sensor's documentation should be implemented in the stop() function.

### isWarmedUp()

`isWarmedUp()` returns a boolean value, indicating if the sensor is ready to start returning values. `isWarmedUp()` is called after _setup()_, and the datalogger will wait for _isWarmedUp()_ to return true before starting to read measurements from the sensor. The logic of _isWarmedUp()_ will typically be a time delay or command that checks with a digital sensor for readiness. More advanced implementations might look at a standard deviation of returned values, such as for an analog sensor.

### takeMeasurement()

This function attempts to take a single measurement from the sensor, and returns true or false depending on if the measurement was successfully taken. Additionally, this function must save the measurement value into the _this.value_ and add this value into the burst summary calculation logic. In the case where a sensor returns multiple variable, the class must be updated to provide private storage for as many variables as necessary and all must be populated on a successful sensor read. To update the class with the appropriate private storage variables, go to the .h file and define the appropriate value variable or variables in the private storage class.

Burst summary calculation is the mechanism by which multiple readings during a burst are combined to produce a single reading, typically a mean value. addValueToBurstSummaryMean(tag, value) is used to track these values and later produce a mean. To use this function in takeMeasurement, use a #define to define a tag for each variable returned by the sensor, and call addValueToBurstSummaryMean with this tag in the first parameter and a measuremented value in the second parameter for each variable measured successfully by the sensor.

## Implement data output functionality.

Data output to the SDCard is implemented by updating the following functions:

1. `getRawDataString()`
2. `getSummaryDataString()`

Additionally, the following privet instance variables must be updated:

1. `baseColumnHeaders`
2. `dataString`

### getRawDataString()

This function simply returns a comma delimited string of the values stored by the last successfully reading from the sensor. This is typically done by using sprintf to print into character array, and then returning this character array. Such as the following code snipped for a single variable. Using the instance variable dataString for storage allows a char \* to be returned without concerns about storage scope.

```
sprintf(dataString, "%d",value);
return dataString;
```

### getSummaryDataString()

This function is similar to `getRawDataString()` execpt that instead of returning values from the last successful sensor reading, it returns a summary value for a burst cycle. This is typically a mean value, which can be retrieved from the values stored by `addValueToBurstSummaryMean(tag, value)` by using the function `getBurstSummaryMean(tag)`. `getBurstSummaryMean(tag)` must be called with the appropriate tag for each variable returned by the sensor. The return value from `getSummaryDataString()` is a comma delimited list of a summary value for each variable returned by the sensor.

For advanced use cases, summary logic other than a mean value may be desired, in which case it is left to the developer to implement appropriate storage and summarization functions in the driver class to support this feature.

### baseColumnHeaders

The baseColumnHeaders private variable stores a const value that contains a comma delimited list of the column header strings for each variable returned by the sensor. If a sensor returns a single, uncalibrated value then this variable will just contain a single variable name such as `const char *baseColumnHeaders = "value";`. When both a raw and calibrated value are returned, a string such the following can be used `const char *baseColumnHeaders = "raw,cal";`. For more complex sensors as many column headers as necessary should be included, such as const char `const char *baseColumnHeaders = "temperature,humidity,CO2";`. Note that drivers are also configured with a prefix tag that will be added to each of these column headers for each instantiaion of the driver.

### dataString

`dataString` is a private variable used to temporarily stored returned output from the sensor during output to the SDCard. The size of this character array must be increased to account for the largest possible number of characters that `getRawDataString()` or `getSummaryDataString()` could need to write for output.

## Implement sensor specific configuration functionality (optional).

Not all sensors will have specific configurations beyond what is provided by the sensor driver superclass already, but many will. To implement these configurations and expose them over the CLI, the following functions and the driver\_configuration struct must be updated.

1. configureSpecificConfigurationsFromBytes(...);
2. getDriverSpecificConfigurationBytes();
3. configureDriverFromJSON(...);
4. appendDriverSpecificConfigurationJSON(...);
5. setDriverDefaults();

## Implement callibration functionality (optional).

## Style Guide

For C++ variable naming and other style conventions, reference the [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html).\
Variable naming reference:

* Class names use studly caps (e.g., StudlyCaps).
* Variable and function names use camel caps (e.g., camelCaps).
* Preprocessor macros (e.g., for use with #define) use screaming snake case (e.g., SCREAMING\_SNAKE\_CASE).
