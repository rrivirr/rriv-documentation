# Methane and Carbon Dioxide Case

Case specifically for use with the Figaro NGM2611-E13, Adafruit DHT22, AtlasScientific EZO-CO2 sensor, and an external power source. Which informs the sensor plate, cable glands, and power supply (length of case).\
\[TODO: If we removed / generalized the sensor plate and cable glands requirements / instructions this could generally be for a 12" elongated case]: #

## Bill of Materials and Potential Supplier or Drawing

| Item                                                       | Case Qty   | Buy Qty   | Supplier Part # / CAD link                                                                                                                                                                                                    |
| ---------------------------------------------------------- | ---------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 3" ABS Schedule 40 Pipe                                    | 11"        | 10'       | [Menards 6881155](https://www.menards.com/main/plumbing/pipe-fittings/abs-pipe-fittings/10-abs-sch-40-plain-end-cellular-core-dwv-pipe/abs033000600hc/p-1444426392509-c-8562.htm)                                             |
| 3" ABS Hub x Hub Coupler                                   | 2          | 1         | [Menards 6881537](https://www.menards.com/main/plumbing/pipe-fittings/abs-pipe-fittings/nibco-reg-hub-abs-dwv-coupling/i00975h/p-1444449159767-c-8562.htm)                                                                    |
| -341 EPDM 70A O-ring                                       | 2          | 15        | [McMaster-Carr 9557K316](https://www.mcmaster.com/9557K316/)                                                                                                                                                                  |
| 18-8 Stainless Steel Threaded Rod 3/8" -16                 | 3          | 2'        | [McMaster-Carr 98920A031](https://www.mcmaster.com/98920A031/)                                                                                                                                                                |
| 18-8 Stainless Steel Hex Nuts 3/8" -16                     | 24         | 100       | [McMaster-Carr 91845A031](https://www.mcmaster.com/91845A031/)                                                                                                                                                                |
| 18-8 Stainless Steel Washers 3/8"                          | 24         | 100       | [McMaster-Carr 92141A031](https://www.mcmaster.com/92141A031/)                                                                                                                                                                |
| 5" Copper Mesh/Gauze                                       | 20"        | 100'      | [McMaster-Carr 6361T16](https://www.mcmaster.com/6361T16/)                                                                                                                                                                    |
| Dow Corning 111 Molykote                                   | Consumable | 5.3 Fl oz | [McMaster-Carr 1204K32](https://www.mcmaster.com/1204K32/)                                                                                                                                                                    |
| Dessicant Packet                                           | 1          | 1000      | [McMaster-Carr 2189K34](https://www.mcmaster.com/2189K34/)                                                                                                                                                                    |
| 11" Cable Ties                                             | 4          | 100       | [McMaster-Carr 7130K55](https://www.mcmaster.com/7130K55/)                                                                                                                                                                    |
| Dome Cap Cable Gland 1/2" NPT .19-.35" w/ O-Ring & Locknut | 1          | 1         | [elecDirect RDC13NR](https://www.elecdirect.com/cord-grips-strain-relief/cable-glands/dome-cap-cable-gland-1-2-npt-19-35-black-complete-with-o-ring-locknut)                                                                  |
| Dome Cap Cable Gland .11-.26" w/ O-Ring & Locknut          | 1          | 1         | [elecDirect RDC07AA](https://www.elecdirect.com/cord-grips-strain-relief/cable-glands/dome-cap-cable-gland-pg7-11-26-black-complete-with-o-ring-locknut)                                                                      |
| 3/4" wide Velcro                                           | 1"         | 5'        | [McMaster-Carr 9273K13-9273K133](https://www.mcmaster.com/9273K13-9273K133/)                                                                                                                                                  |
| 18-8 Stainless Steel Phillips Flat Head #6 x 1/2" Screws   | 6          | 100       | [McMaster-Carr 90065A148](https://www.mcmaster.com/90065A148/)                                                                                                                                                                |
| 3/4" x 3/4" Nylon Bar                                      | 1'         | 1'        | [McMaster-Carr 8732K17](https://www.mcmaster.com/8732K17/)                                                                                                                                                                    |
| 1/4" Clear Acrylic Lid Plate\*                             | 1          | NA        | [CAD Drawing 3inch](https://github.com/rrivirr/sonde/tree/master/panels)                                                                                                                                                      |
| 1/4" Clear Acrylic Sensor Plate\*                          | 1          | NA        | [CAD Drawing 3inch](https://github.com/rrivirr/sonde/tree/master/panels)                                                                                                                                                      |
| 1/4" Clear Acrylic Cage Plate\*                            | 1          | NA        | [CAD Drawing 3inch](https://github.com/rrivirr/sonde/tree/master/panels)                                                                                                                                                      |
| ABS Cement                                                 | Consumable | NA        | [Menards 6932185](https://www.menards.com/main/plumbing/plumbing-installation-repair/pipe-cements-cleaners-primers/oatey-reg-medium-black-abs-cement-4-oz/309995/p-1444449932067-c-8530.htm?tid=-7621218153408053791\&ipos=1) |

\*[Flare Tech Laser & Design](https://flaretechlaser.com/)

## Diagrams

\[TODO: add images to markdown file ![alt text](https://github.com/\[username]/\[reponame]/blob/\[branch]/image.jpg?raw=true) ]:#

[Annotated Case Diagram](methane_case_1ft.md)[3" Acrylic Plates CAD drawing](https://github.com/rrivirr/sonde/tree/master/panels)

## Build Process

### Tools & Skills

* [Horizontal/Vertical Metal Cutting Band Saw](https://www.harborfreight.com/horizontal-vertical-metal-cutting-bandsaw-93762.html) to cut steel threaded rod to length
* [Reed TC4QP Tubing Cutter for plastic pipe](https://www.reedmfgco.com/en/products/plastic-pipe-tools/quick-release-tubing-cutters-for-plastic-pipe/tc4qp/) to cut ABS to length
* 2x [9/16 SAE combination wrench](https://www.mcmaster.com/56255A34/) for hex nuts
* [Milwaukee 6in Diagonal Cutting Pliers](https://www.milwaukeetool.com/Products/Hand-Tools/Pliers/Diagonal-Cutters/48-22-6106) for copper mesh and cable ties
* Measuring tape
* \#2 phillips head screw driver / drill bit

### Parts Fabrication

* Cut steel threaded rod in half to 1' lengths
* Cut two 1-21/32" length sections of ABS, 20/32 to 22/32 is acceptable, too little won't hold the o-ring in place, too much won't compress the o-ring enough to seal properly
* Cut 20" of copper mesh x2
* Attach both cable glands through their respective holes in acrylic sensor plate

### Assembly & Waterproofing

1. Add cable glands to sensor plate
2. Insert ABS 1-21/32" length into each end of coupling
3. Add O-Rings around ABS
4. Add nuts & washers to rods
5. Add plates & housing to rods
6. Wrap copper mesh around sensor cage and use cable ties to hold in place
