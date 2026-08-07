# Methane Chamber
description
## Bill of Materials

| Item          | Chamber Quantity | Buy Quantity  | Supplier part # / URL   |
| ------------- | ---------------- | ------------- | ------------- |
| 8 quart bucket | 1 | 6  | https://www.usplastic.com/catalog/item.aspx?itemid=23173&catid=818 |
| 2.5 LPM, 4.5 V air pump | 1 | 6 | https://www.adafruit.com/product/4699 |
| NGM2611-E13 | 1 | | |
| AHT20 * | 1 | | https://learn.adafruit.com/adafruit-aht20 |
| PNP transistor | 1 | 10 (1 pack) | https://www.adafruit.com/product/756 |
| Diode | 1 | 10 | https://www.adafruit.com/product/755 | 
| 330 ohm Resistor ** | 1 | 20 (1 pack) | https://www.sparkfun.com/products/14490 |
| NiMH D cell bateries | 4 | 16 | http://power.tenergy.com/tenergy-d-10-000mah-nimh-rechargeable-battery-16pcs/ |
| battery holders | 4 |  | https://www.digikey.com/en/products/detail/mpd-memory-protection-devices/BH2DL/56225 |
| Protoboard / stripboard | consumable | | |
| Jst-PH 3pin plug | 4 | | |
| Jst-PH 2pin plug | 1 | | |
| Dupont 1pin socket plug | 1 | | |
| Jst-XH 4pin socket | 1 | | |
| Jst-XH 4pin plug | 1 | | |
| 3 mm Tubing(1 m long) | 3 | 18 | https://www.adafruit.com/product/4661 |
| tube Connectors | 1 | 10 (2 packs) | https://www.adafruit.com/product/4764 |
| bulk head | 1 | 10 (2 packs) | https://www.ebay.com/itm/325299130979 |
| Dessicant Packet | 2 | 1000 | https://www.mcmaster.com/2189K34/ |
| PVC enclosure box (4" x 4" x 4") | 2 | 12 | https://www.menards.com/main/electrical/electrical-boxes-covers/electrical-boxes/carlon-reg-pvc-enclosure-box/e987nr/p-1444444973425-c-6425.htm?tid=5250369202477893839&ipos=7 |
| Polyethylene (HDPE) Sheet ( 3 inch width, 4 foot length, 1/8 inch thickness ) |  |  | https://www.mcmaster.com/8671K56/ |
| Jumbo pool noodles | 2 | 12 | https://www.walmart.com/ip/Oodles-of-Noodles-Pool-Noodles-5-PACK-Random-Colors/746213215?fulfillmentIntent=Shipping&athbdg=L1600 |
| 11" Zip ties | 16| 100 | https://www.menards.com/main/electrical/electrical-tools-accessories/cable-ties/gardner-bender-reg-11-natural-cable-ties-100-pack/46-210/p-1444430994083-c-6443.htm?tid=-1577002442902513490&ipos=9 |  
| Zinc plated machine screws *** (size 10, 32 x 1-1/2") | 8 | 70 (1 box)| https://www.menards.com/main/hardware/fasteners-connectors/screws/machine-screws/grip-fast-reg-10-32-x-1-1-2-combo-drive-zinc-round-head-machine-screw-70-count/77116520241/p-1444452011002-c-8933.htm?tid=523259707822814569&ipos=7 |
| Small Heat Shrink Tubing| consumable | | |
| Hot Glue | consumable | | |
| Solder | consumable | | |
| Silicone Sealant | consumable | | |
discontinued product, may need to switch to AHT20, an i2c sensor, if can't find stock. This would also affect the XH socket and plug +1
** 330 resistors actually  used from variety pack, link is for just 330 resistors 
*** 3/4" machine screws would be a better length, 1 1/2" used 

## Diagrams
diagram air pump circuit
![Screenshot 2023-02-15 at 3 29 16 PM](https://user-images.githubusercontent.com/103074569/219152341-593cb96a-a043-4425-9710-3bf024a7f128.jpg)

diagram of cutting & drilling for Polyethelene 
![IMG_40C85594B607-1](https://user-images.githubusercontent.com/103074569/219152421-98b87355-d171-4ba4-b86e-77568957aac7.jpeg)

diagram of drilling bucket
![IMG_E75C9200ADB3-1](https://user-images.githubusercontent.com/103074569/219155273-d93df3ff-158f-412d-9075-35c896966eec.jpeg)

diagram of fitting stuff in PVC boxes

-------------------

## Build Process

### Tools & Skills
Drill, 5/32" drill bit, Scalpel / art knife, Wire stripper, Wire cutter, Dupont Crimping Pliers, Engineer PA-21 Crimping Pliers, Soldering iron, Mini glue gun, heat gun

### Parts Fabrication
Air Pump Ciricut:
 1. cut 4 x 4 square of protoboard with strips going horizontal
 2. Use exacto knife to sever connection between (2,4) and (2,3) holes 
 3. solder wires to air pump, add heat shring tubing to exposed part of air pump - wire ends 
 4. Solder transistor, resitor, diode and wires to protoboard 
 5. Attach Dupont 1 pin plug to the yellow, GPIO wire
 6. Attach Jst-PH 3pin plug to the red and black wire
    See diagram  X

DCell batery 
 strip and solder wires in parallel. Crimp Jst-PH 2Pin plug to wires

Chamber Fabrication
note bucket is refered to un an inverted way the "top" is the flat not open end and the rim is at the "bottom" 
 1. Remove handle from bucket
 3. Drill 4 additional holes so the 6 total are evenly spaced 
 4. Cut 11" x 4" sheet of polyethylene 
 5. Drill hole in center
 6. Align PVC boxes, drill designated holes through polyethylene sheet
 7. Drill designated holes through PVC boxes
 8. Align PVC boxes, bucket and polyethylene sheet
 9. Drill aligned holes, easiest to do if done separtly 
 10. Drill a hole through the side of one of the PVC boxes. This box will hold air pump
 11. Wrap pool noodles around the bottom of the bucket. Secure with zip ties.
     Sip tie first pool noodle directly to the holes in the rim of the bucket.
     Combine 2 zipites to wrap around both noodles when adding the second layer. Also secure to the holes in the bucket

### Assembly & Waterproofing
 1. Place sensors in bucket chamber
 2. Pull wires without Jst-PH 2Pin plug ends through aligned bucket, polyethelyne sheet and PVC box hole. 
 3. For temporary use hot glue wires on insde of bucket at desired position to hold in place
 5. Screw polyethelyne sheeet and PVC boxes into place 
 6. Pull short length of tubing through the other aligned holes  
 7. Hold tubing in palce with hot glue on the insdie of the bucket 
 8. Put air pump and sensors in deisingated PVC boxes. Each box can fit 2 D cell battery packs plus the waterbear board
    See diagram 4
 10. Check wire and tubing lengths, add tubing from air pump to hole in side of PVC box 
 11. Plug in wires to the waterbear test sensors and airpump 
 12. Screw on PVC lids 
 13. Test floatability of device plus the weight of the batteries and waterbear. Adjust anythign as needed
 15. Seal inside of bucket where tubing and wiring is using silicone / waterproof sealant
 
