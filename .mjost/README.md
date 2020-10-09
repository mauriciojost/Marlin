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

```

M111 S247           to enable maximum logging
G28                 to home
G29                 probe the bed

G1 X0 Y0            go to
G1 X180 Y0
G1 X0 Y180
G1 X0 Y0 Z20

G1 X+20 Y+20
G1 X+40 Y+40 -> shoudl go to the right, to the front


 When jogging, if you increase X the extruder should move to the right, and if you increase Y the bed should move towards the front of the printer. If either of these are incorrect we need to fix that first.



```
