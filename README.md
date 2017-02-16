# Arduino RC Flight Control

Welcome to the Arduino based remote flight controller. This repo provides source code for an RC
remote controller (with an Arduino, PS4 controller, Radio transmitter module) and for an receiver 
(Arduino, Radio receiver module, Servos).

## Requirements

For the transmitter electronics
- Arduino AtMega 2560
- Arduino USB Host Shield
- NRF24L01 Transmitter/Receiver Module
- PS4 Controller

For the receiver electronics
- Arduino Nano
- 4 Servo Motors
- LiPo Accumulators, or similar
- Motor controller with 5V DV Output

## USB Host Shield modification

In order to use the LCDTFT Shield on top of the USB Host Shield rev 2.0, there are a few things to be done before. As both shields share the same pins (Digital 9 and 10) it make sense to change the USB Host shield pins. The tft shield occupies pins D5-D13, so the USB host shield can use e.g. D1 and D2.Therefore I rewired the SS (original D10) to D2 and the INT (originally D9) to D1. There have to be a few changes in the UsbCore.h file in the USB Host Shield Library. Go to line 43 and change it  to 
```c
typedef MAX3421e<P2, P1> MAX3421E; // Official Arduinos (UNO, Duemilanove, Mega ...
```
Now your Usb Host Shield will work as well, if you rewired it correctly.

## Installation

The *_nano.ino file is the logic for the Arduino Nano and the *_mega.ino file is the source code
for controlling the Arduino AtMega 2560 (would work with an Uno R3 as well). The pin configuration for
the NRF24L01 modules looks as follows

| Description | Nano | AtMega 2560 |
|-------------|------|-------------|
| VCC         | 5V   | 5V          |
| GND         | GND  | GND         |
| SCK         | 13   | 52          |
| MOSI        | 11   | 50          |
| MISO        | 12   | 51          |
| CE          | 7    | 53          |
| CSN         | 8    | 49          |

Notice that the CE and CSN pins require just a digital pin, it doesn't matter which ones you are choosing. The configuration
of an Uno R3 should be similar to the Nano one, but no guarantee for that.

The servo pin configuration is set to

| Motor | Roll-aileron left | Roll-aileron right | Pitch elevator | Side rudder |
| ---   | ---               | ---                | ---            | ---         |
| 2     | 3                 | 4                  | 5              | 6           |

# References

- http://shieldlist.org/adafruit/tft-2.8-touch-lcd
- http://shieldlist.org/circuitsathome/usbhost-v2
- https://github.com/felis/USB_Host_Shield_2.0#interface-modifications
- https://github.com/JoaoLopesF/SPFD5408