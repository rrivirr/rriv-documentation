# Driver integration steps

1. Make your local copy of the main [RRIV github repo](https://github.com/rrivirr/rriv) up-to-date.

make a branch that is appropriate for your sensor driver.

When starting to make a new driver you need to copy the driver template .cpp and .h

start renaming variables that are specific to the new device you are writing the driver for. Ultimately should have a script that does this for us. Everything that says driver_tempalte in here needs to be changed to match the driver that you're using.

Jake will write a bash script using sed that will prompt you for the new driver name (can also have it copy the file) and then it will replace the generic names with the new names.

after you rename and add everything and it compiles you have to edit the registry. eventually we should automate but for now we're going to do this manually. In the registry there are steps written for how to add your new driver in registry.cpp. THis includes edits to registry.h

under build sensor driver map there are three parts to sensor maps class_name, sensor_code, and sensor string name (which is the name given when data are delivered via JSON object.

Now comes the hard part. you have to implement the driver. this can be easy if there's an existing driver that you can wrap. 

when you are wrapping drivers you would fork them and then put the fork in the platformio.ini.

[Code Implementation Steps](steps.md)
