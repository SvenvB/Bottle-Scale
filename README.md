# Bottle Scale
Bottle scale for timing and weighing baby food. The scale is integrated with the Baby Buddy integration in Home Assistant.

* The scale design is inspired by the great work from [sfgabe:](https://github.com/sfgabe/OITProjects/tree/master/BabyBuddy_ESP_HASS), but since I am by far not a woodworking expert, I designed a similar casing in FreeCAD that can be 3D printed. Attached are the files.
* The keypad is connected to HomeAssistant via [ESPHome](https://www.home-assistant.io/integrations/esphome/)
* The keypad automation is integrated with the NodeRED BabyBuddy project of [tango259](https://github.com/tango2590/baby-buddy)


<img src="https://github.com/SvenvB/Bottle-Scale/blob/main/Photos/IMG-20250217-WA0000.jpg" width="400">
<img src="https://github.com/SvenvB/Bottle-Scale/blob/main/Photos/20250217_172956.jpg" width="400">

## Ingredients
* 1x [Lolin NodeMCU v3 ESP8266 with integrated 0.96" SSD11306 screen](https://www.aliexpress.us/item/3256806790582188.html?spm=a2g0o.order_list.order_list_main.34.21ef1802q4o1JS&gatewayAdapt=glo2usa). Screen could be bought and connected separately to the microcontroller.
* 2x [Blank Keypad Buttons](https://www.aliexpress.us/item/3256807496928162.html?spm=a2g0o.order_list.order_list_main.44.21ef1802GzlgdW&gatewayAdapt=glo2usa)
* 2x [Mechanical keyboard switches](https://www.aliexpress.us/item/3256807318817256.html?spm=a2g0o.order_list.order_list_main.38.21ef1802GzlgdW&gatewayAdapt=glo2usa)
* (2x M2 screws to fix the microcontroller in the box)
* (3x M3 screws to fix the weighing scale to the box)

## Electrical Connections
* The ESP8266 is getting power from the Vin + GND pins via a USB cable that has a soldered 2x1 female pin header to connect to those pins. Using the USB-C connection on the board is not possible because the space is blocked by the push buttons. 

<img src="https://github.com/SvenvB/Bottle-Scale/blob/main/Schematic/Schematic_bb.png" width="400">
<img src="https://github.com/SvenvB/Bottle-Scale/blob/main/Schematic/Schematic_BottleScale.pdf" width="400">

## CAD Modeling

* The screen location might differ since the screen is manually attached to the board using double-sided tape. Therefore you might need to adjust the CAD model based on your EPS8266.
* Similarly the mounting holes in the plastic plates of the bottle scale seem to be manually drilled. This also might warrant some manual changes in the CAD model so that your scale fits.
