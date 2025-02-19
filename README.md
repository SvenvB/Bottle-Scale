# BabyBuddy Bottle Scale for Home Assistant
Bottle scale for timing and weighing baby food. The scale is integrated with the Baby Buddy integration in Home Assistant.

* The scale design is inspired by the great work from [sfgabe:](https://github.com/sfgabe/OITProjects/tree/master/BabyBuddy_ESP_HASS), but since I am by far not a woodworking expert, I designed a similar casing in FreeCAD that can be 3D printed. Attached are the files.
* The keypad is connected to HomeAssistant via [ESPHome](https://www.home-assistant.io/integrations/esphome/)
* The keypad automation is integrated with the NodeRED BabyBuddy project of [tango259](https://github.com/tango2590/baby-buddy)


<img src="https://github.com/SvenvB/Bottle-Scale/blob/main/Photos/scale_with_bottle.jpg" width="400">
<img src="https://github.com/SvenvB/Bottle-Scale/blob/main/Photos/scale_without_bottle.jpg" width="400">

## Ingredients
* 1x [Strain gauge load cell with HX711 amplifier / AD converter](https://www.aliexpress.us/item/3256807921661482.html?spm=a2g0o.order_list.order_list_main.28.21ef1802q4o1JS&gatewayAdapt=glo2usa). I used a 1 kg capacity load cell, but 5 kg should work also. 
* 1x [Lolin NodeMCU v3 ESP8266 with integrated 0.96" SSD1306 screen](https://www.aliexpress.us/item/3256806790582188.html?spm=a2g0o.order_list.order_list_main.34.21ef1802q4o1JS&gatewayAdapt=glo2usa). Screen could be bought and connected separately to the microcontroller.
* 2x [Blank Keypad Buttons](https://www.aliexpress.us/item/3256807496928162.html?spm=a2g0o.order_list.order_list_main.44.21ef1802GzlgdW&gatewayAdapt=glo2usa)
* 2x [Mechanical keyboard switches](https://www.aliexpress.us/item/3256807318817256.html?spm=a2g0o.order_list.order_list_main.38.21ef1802GzlgdW&gatewayAdapt=glo2usa)
* 3x 5mm through hole LEDs of different colors
* 3x through hole resistors of ~50 Ohm
* (2x M2 screws to fix the microcontroller in the box)
* (3x M3 screws to fix the weighing scale to the box)

## Electrical Connections
* The ESP8266 is getting power from the Vin + GND pins via a USB cable that has a soldered [2x1 female pin header](https://github.com/SvenvB/Bottle-Scale/blob/main/Photos/usb-cable.jpg) to connect to those pins. Using the USB-C connection on the board is not possible because the space is blocked by the push buttons in this CAD design.
* The D8 pin has an internal pull-down resistor, and D8 must be low at boot to avoid boot failure. Therefore, the button connected to D8 should be connected to the +3.3V pin, and not GND. The button connected to D7 makes use of an internal pull-up resistor and is therefore connected to GND.
* The D5 and D6 pins are used by the onboard SSD1306 screen.

<img src="https://github.com/SvenvB/Bottle-Scale/blob/main/Schematic/Schematic_bb.png" width="800">
<img src="https://github.com/SvenvB/Bottle-Scale/blob/main/Schematic/Schematic.png" width="800">

* The load cell is connected to the HX711 breakout board using 4-wires. Take a moment to familiarize yourself with the basic principle of how a single-point load cell [works](https://www.800loadcel.com/blog/single-point-load-cells-what-they-are-and-how-they-work.html). It relies on 4x strain gauges in a Wheatstone bridge configuration as indicated in the [schematic](https://github.com/SvenvB/Bottle-Scale/blob/main/Schematic/Schematic.png) above. The resistance of those gauges depends on the tension (of the 2x gauges on top) and compression (of the 2x gauges on the bottom) due to the weight applied to the aluminum. Two wires (red [E+] & black [E-]) are used to bias the bridge, whereas the signal potential (Vsignal = [A+] - [A-]) grows with increasing contrast to the tension and compression resistances. The signal is amplified and digitized by the HX711 breakout board. No more to it than that.

## CAD Modeling
* The scale is designed in freeware [FreeCAD](https://www.freecad.org/). Uploaded are the step files but also the FreeCAD project so you can make any changes desired:

**Important notes:**
* The screen location might differ since the screen is manually attached to the board using double-sided tape. Therefore you might need to adjust the CAD model based on your screen location.
* Similarly the mounting holes in the plastic plates of the bottle scale seem to be manually drilled. This also might warrant some manual changes in the CAD model so that your scale fits. The hole in the top plate is a tight fit.
* The electronics compartment is also quite compact. You will want to remove any excessive wire length otherwise it won't fit.
* The top plate and computer plate are not screwed down but glued using a glue pistol. If you don't have a glue pistol or strong double-sided tape, you might want to add some screw holes in the design.   

<img src="https://github.com/SvenvB/Bottle-Scale/blob/main/Photos/electronics_box1.jpg" width="400">
<img src="https://github.com/SvenvB/Bottle-Scale/blob/main/Photos/electronics_box2.jpg" width="400">

* The buttons are printed on a 4x6" photo at the local CVS store:

<img src="https://github.com/SvenvB/Bottle-Scale/blob/main/FreeCAD/buttonsticker/buttons_bottlescale.png" width="400">


## ESPHome and Automation
I won't go into much detail here, as this can be integrated however you like. I integrated the automation directly with the NodeRED BabyBuddy project of [tango259](https://github.com/tango2590/baby-buddy).

Attached you can find my [ESPHome code](https://github.com/SvenvB/Bottle-Scale/blob/main/esphome_code.yaml) for the device. The microcontroller receives one sensor and two text_sensors from the home assistant front-end:
* *input_number.bottle_scale_calibration_value*: which is the measured weight when pushing the start button on the left-hand-side. It then subtracts this calibration value from the measured value so that when you put the empty bottle on the scale to stop recording, you can directly see how much the baby ate.
* *sensor.stopwatch*: is the [stopwatch](https://community.home-assistant.io/t/stopwatch-with-start-stop-resume-lap-and-reset/443994) used in the NodeRED BabyBuddy project of [tango259](https://github.com/tango2590/baby-buddy). The stopwatch value is also shown on the screen.
* *input_text.bottle_scale_status*: is a text label on the bottom of the screen that either says *<-- Start feeding*, *Stop feeding-->*, or *Feeding recorded!*.

Don't forget to [calibrate](https://esphome.io/components/sensor/hx711.html) your scale in ESPhome code by removing my calibration and then find the sensor readings when using zero load and a known weight. 

Happy feeding!
