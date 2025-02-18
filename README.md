# Bottle-Scale
Bottle scale for timing and weighing baby food. The scale is integrated with the Baby Buddy integration in Home Assistant.

* The scale design is inspired by the great work from [sfgabe:](https://github.com/sfgabe/OITProjects/tree/master/BabyBuddy_ESP_HASS), but since I am by far not a woodworking expert, I designed a similar casing in FreeCAD that can be 3D printed. Attached are the files.
* The keypad is connected to HomeAssistant via [ESPHome](https://www.home-assistant.io/integrations/esphome/)
* The keypad automation is integrated with the NodeRED BabyBuddy project of [tango259](https://github.com/tango2590/baby-buddy)


<img src="https://github.com/SvenvB/Bottle-Scale/blob/main/Photos/IMG-20250217-WA0000.jpg" width="500">


## Electrical Connections
* The ESP8266 is getting power from the Vin + GND pins via a USB cable that has a soldered 2x1 female pin header to connect to those pins. Using the USB-C connection on the board is not possible because the space is blocked by the push buttons. 

## CAD Modeling

* The screen location might differ since the screen is manually attached to the board using double-sided tape. Therefore you might need to adjust the CAD model based on your EPS8266.
* Similarly the mounting holes in the plastic plates of the bottle scale seem to be manually drilled. This also might warrant some manual changes in the CAD model so that your scale fits.
