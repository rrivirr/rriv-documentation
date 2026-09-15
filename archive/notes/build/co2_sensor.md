# Waterproof CO2 Sensor

Sensor and waterproof case specifically for use with the Atlas EZO-CO2 sensor

## Bill of Materials

| Item                                | Case Qty   | Buy Qty | Supplier Part # / CAD link |
| ----------------------------------- | ---------- | ------- | -------------------------- |
| Atlas Scientific EZO-CO2 sensor     | 1          | 1       | https://...                |
| 1-1/4" PVC Sch 40                   | 1          | 1       |                            |
| 1-1/4" PVC Sch 40 End Cap           | 1          | 1       |                            |
| 1-1/4" PVC Sch 40 Hub x Hub Coupler | 1          | 1       |                            |
| MiniPax Dessicant                   | 1          |         |                            |
| .005" PTFE film 6" Wide             | Consumable |         |                            |
| 8" cable tie                        | 2          |         |                            |
| Solder                              | Consumable |         |                            |
| Plastidip                           | consumable |         |                            |
| Tall round cylinder container       |            |         |                            |
| Epoxy                               | Consumable |         |                            |
| Epoxy Putty                         | Consumable |         |                            |
| RDC13NR Cord Grip                   | 1          |         |                            |
| Jst-PH 4pin plug                    | 1          |         |                            |
| Dupont 1pin socket plug             | 1          |         |                            |

## Schematics

Wiring diagrams.

### Communication protocol

### Power solution

## Diagrams

Mechanical drawings.

## Build Process

### Tools & Skills

Drill\
1/4" drill bit\
Ridgid Quick-acting tubing cutter (model 151)\
Deburring tool (find the right sized one for 1-1/4" pvc)\
Scalpel / art knife\
Wire stripper\
Wire cutter\
Dupont Crimping Pliers\
Engineer PA-21 Crimping Pliers\
Soldering iron\
Gloves\
Fume hood / well ventilated area\
Tension rod (for fume hood)\
Shower rings & clips

### Parts Fabrication

1. Cut PTFE film to 3" x 3" square
2. Drill 1/4" hole in center of cap
3. Cut PVC to 2.25" and deburr both ends, until they are smooth to touch (only have to do one end if you keep track of it as the end that contacts the PTFE)
4. Drill two offset rings of 8x 1/4" holes in the bottom half of PVC coupler (can do 4 holes if you drill all the way across)
5. Cut CO2 cable down to 8.5"

### Assembly & Waterproofing

1. Thread sensor cable through the cap
2. Strip 1" off cable, and 2mm off each wire, then crimp and add JST-PH connector and Dupont connector
3. Test that the sensor still works, if not, check wiring or switching to I2C mode, once it works, use a scalpel/art knife to lift the tabs holding connectors from step 2 in place, and remove them
4. Sandwich 3"x3" square of PTFE film between 1.5" PVC section and end of PVC coupler without holes, carefully compress the parts as far as possible. If you hear a tearing sound, start over with new PTFE
5. Add interlock two zipties and place around the coupler over the set of holes closest to the bottom
6. Add a small amount of Epoxy putty to block the whole in the cap around the cable, it might help to hold it upside down when pushing the putty into the gap slightly, so the cable does not move around as much
7. Add Epoxy around seam between PVC cap and coupler, or mainly the seam from those two components to the PVC pipe section
8. Let both Epoxy and Epoxy putty cure for 1 hour, hanging upside down using the zipties and shower ring clips in the fume hood or well ventilated space
9. Fill cylinder container with Plastidip and mix thoroughly
10. Use masking tape to cover the exposed wires and crimps in a tube
11. Slowly insert and extract masking tape side first into Plastidip filled container (1" every 5 seconds), taking care to evenly coat each area. Dip up to \~1" of the coupler, not covering the drilled holes, hang to cure for 30 min, and apply a second coating
12. After 30 min, inspect for any gaps that can be filled using a spatula, taking care not to create bubbles
13. Hang to cure for 8 hours in ventilated space, and inspect and fill gaps as necessary
14. Remove the zip ties, remove around 4.5" of the Plastidip around the cable and masking tape, carefully use a cutting tool and the wire stripper to do this
15. Remove the masking tape, then add the cable grip on over the plastidipped section, and place the connectors back on the wires
16. Test the sensor is working correctly, if i2c errors are shown then try manually switching the CO2 sensor to I2C mode by powering on the device with blue and green wire shorted together for a few seconds
