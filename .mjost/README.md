vim platformio.ini

# Info of my board
ATmega2560
TriGorilla

Z bed levelling: inductor sensor.

# Useful commands

platformio lib search "header:LiquidCrystal.h"
platformio lib install LiquidCrystal
platformio lib install U8glib

# Tuning procedure

1. Configuration -> Probe Z Offset = 0
2. Motion -> Auto Home
3. Put a paper under the nozzle
4. Motion -> Move Axis -> Move Z -> Move 0.025mm
5. Go down until the paper does hardly slide under the nozzle, write down the read in the LCD screen (negative Z value)
6. Configuration -> Probe Z Offset = VALUE READ (as read in the above step, should be negative)
7. Configuration -> Store settings

That's all.

# Commands

## Z probe calibration (regular)

```
                        0. put paper on bed
M851 Z-2.57             1. try a value
G28                     2. level bed again
G1 Z0                   3. go to Z0 (should block the paper, otherwise expand delta Z on 1. and iterate)

M500                    4. once good store on eeprom

```

## Checks and initial calibration

```
                       measure maximum range X and Y and Z and set them into X/Y_BED_SIZE
                       (this assumes no bed start before endstops)

M111 S247              use to enable maximum logging

G28                    should auto-home X & Y at least (make sure you stop the printer at Z attempt)

G1 X0 Y0 Z0            should go towards endstops (home)
G1 X20 Y20 Z20         should go opposite of endstops


M851                   after auto-home G28 see the xyz probe offset
                       (if not right, you will have to adjust with
M851 X-15 Y-41 Z-2.57  
                       or clear EEPROM with
M502                   (reset the eeprom, many bed leveling metrics are there)
                       and default firmware defs will be used, this fixed the issue for me.
                         

```

## Useful commands

```
G28                    to home
G29                    probe the bed

G1 X180 Y0             go to
G1 X0 Y180
G1 X0 Y0 Z20

G1 X+20 Y+20

M851                   tell the probe offset

M140 S60               start heating the bed to 60 degrees Celsius
M104 S200 T0           start heating T0 to 200 degrees celsius

```
