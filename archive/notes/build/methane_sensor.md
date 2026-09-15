# Waterproof Methane Sensor

Sensor and waterproof case specifically for use with the Figaro NGM2611-E13, and Adafruit AHT20.

## Bill of Materials

| Item                                                       | Case Qty   | Buy Qty   |  Supplier Part # / CAD link |
| ---------------------------------------------------------- | ---------- | --------- |  -------------------------- |
| NGM2611-E13        | 1  | 1          | https://www.figarosensor.com/product/entry/ngm2611.html source w/ 2 month lead |
| AHT20              | 1  | 1           | https://www.adafruit.com/product/4566 |
| 1-1/4" PVC Sch 40         | 1 | 1 | |
| 1-1/4" PVC Sch 40 End Cap | 1 | 1 | |
| 1-1/4" PVC Sch 40 Hub x Hub Coupler | 1 | 1 | |
| 8 conductor cable* | 7.5" |1m | digikey |
| MiniPax Dessicant | 1 | | |
| .005" PTFE film 6" Wide | Consumable | | |
| 8" cable tie | 2 | | |
| Solder | Consumable | | |
| Plastidip  | consumable | |
| Tall round cylinder container | | | |
| Epoxy | Consumable | | |
| Epoxy Putty | Consumable | | |
| Protoboard/stripboard* | Consumable | | |
| Mini glue gun stick | Consumable | | |
| RDC13NR Cord Grip | 1 | | |
| Jst-PH 3pin plug | 3 | | |
| Dupont 1pin socket plug | 1 | | |
| Jst-XH 4pin socket* | 1 | | |
| Jst-XH 4pin plug* | 1 | | |


## Schematics

Wiring diagrams.

### Communication protocol

### Power solution

## Diagrams

Mechanical drawings.

## Build Process

### Tools & Skills

* Drill
* 1/4" drill bit
* Rigid Quick-acting tubing cutter (model 151)
* Deburring tool (find the right sized one for 1-1/4" pvc)
* Scalpel / art knife
* Wire stripper
* Wire cutter
* Dupont Crimping Pliers
* Engineer PA-21 Crimping Pliers
* Soldering iron
* Mini glue gun
* Gloves
* Fume hood / well ventilated area
* Tension rod (for fume hood)
* Shower rings & clips

### Parts Fabrication

1. Drill 1/4" hole in center of cap
1. Cut PVC to 2.25" and deburr both ends, until they are smooth to touch (only have to do one end if you keep track of it as the end that contacts the PTFE)
1. Drill two offset rings of 8x 1/4" holes in the bottom half of PVC coupler (can do 4 holes if you drill all the way across)
1. Solder DHT22 to proto board (4x4) w/ JST-XH 4pin socket, 10k ohm resistor
1. Cut cable to 8.5", strip 1" off one end, then 2mm off each wire attach crimps and slide into JST-XH 4pin plug and Dupont 5pin socket
1. Cut PTFE film to 3" x 3" square


### Assembly & Waterproofing

1. Thread cable through the cap, and attach sensors
2. Strip 4" off cable, and 2mm off each wire, then crimp and add JST-PH connectors and Dupont connector
3. Test that the sensors still work, if not, check wiring, if they do, use a scalpel/art knife to lift the tabs holding connectors from step 2 in place, and remove them
4. Sandwich 3"x3" square of PTFE film between 1.5" PVC section and end of PVC coupler without holes, carefully compress the parts as far as possible.  If you hear a tearing sound, start over with new PTFE
5. Use the glue gun to coat the exposed contacts on the bottoms of one or both sensors, then add the sensors and dessicant pack inside the cap to the top of the PVC section, compress as much as possible
6. Add interlock two zipties and place around the coupler over the set of holes closest to the bottom
7. Add a small amount of Epoxy putty to block the whole in the cap around the cable, it might help to hold it upside down when pushing the putty into the gap slightly, so the cable does not move around as much
8. Add Epoxy around seam between PVC cap and coupler, or mainly the seam from those two components to the PVC pipe section
9. Let both Epoxy and Epoxy putty cure for 1 hour, hanging upside down using the zipties and shower ring clips in the fume hood or well ventilated space
10. Fill cylinder container with Plastidip and mix thoroughly
11. Use masking tape to cover the exposed wires and crimps in a tube
12. Slowly insert and extract masking tape side first into Plastidip filled container (1" every 5 seconds), taking care to evenly coat each area.  Dip up to ~1" of the coupler, not covering the drilled holes, hang to cure for 30 min, and apply a second coating
13. After 30 min, inspect for any gaps that can be filled using a spatula, taking care not to create bubbles
14. Hang to cure for 8 hours in ventilated space, and inspect and fill gaps as necessary
15. Remove the zip ties, remove around 4.5" of the Plastidip around the cable and masking tape, carefully use a cutting tool and the wire stripper to do this
16. Remove the masking tape, then add the cable grip on over the plastidipped section, and place the connectors back on the wires
17. Test the sensors are working correctly, it's only possible to correct wiring issues at the external part without opening the case and essentially starting over.
