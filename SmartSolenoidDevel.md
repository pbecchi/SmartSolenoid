**SmartSolenoid Developments**

![](.\/media/image1.jpeg){width="3.560416666666667in"
height="3.0027777777777778in"}

**The Idea**

To address the need of all people the have to irrigate where no power is
available and do not like to run long wire to connect the controller to
the irrigation valves, we got the ideas of embedding a small battery
operated controller to a latching solenoid , and we name it
SmartSolenoid.

**BLE SmartSolenoid**

Originally, when we started in September 2017, the unit was based on a
long range BLE chip , with a very low current draw and an acceptable RF
range . We have developed a code to be run on a nRF52 BLE 5.0 chip that
could be RF connected to a Smartphone or to and OpenSprinkler running on
a ESP32 processor. The Espressif ESP32 processor have an embedded BLE
4.0 unit capable to be connected to nRF52 units. Unfortunately the ESP32
BLE library are not yet fully developed and adding BLE to OpenSprinkler
require functions and capabilities not available yet.

The SmartSolenoid code running on nRF52 is available on
https://GitHub.com/pbecchi/SmartSolenoid and can be compiled with
Arduino IDE.

We have used Fanstel Bt832 and BT832X modules.

The test we have performed with BT832 show expected range of 20 to 50 m
and depend a lot on module position . Modules need to be in line of
sight and any obstacle need to be avoided.

Current drawn by the module is very low, in average 50 to 120 uA ,
leading to a duration of 2500 h (100 day) with a small coin battery.

With BT832X module , than include a power amplifier, with have a
substantial range increase up to about 500 m LOS.This may be more than
enough for most of the user applications!

But since range is never really enough, recently we started a new
SmartSolenoid development replacing Bluetooth link with a LoRa one.

**LoRa SmarSolenoid**

LoRa is a family of new spread spectrum RF transceiver working on 430
980 mHz bands.

Several low cost modules are today available on the market with 100mA RF
(20 dB) Power transmission. For our SmartSolenoid nodes, we have
selected a Semteck 1278 (433mHz) based module combined with an Atmel328p
processor . This combination is supported by a wide choice of libraries
(Arduino) and lead to a good low-power code.

Our prototype is based on a Electrodragon LoraArduino board and a small
board to switch one or two latching solenoid.

http://www.electrodragon.com/product/wifi-lora-32-dev-board/

The power to the solenoid is provided by a 9v battery, while a small 1s
lipo battery power LoraArduino. Our measurement of current consumption
lead to a 2000mAh battery duration of 1 to 2 month, while the 9v battery
should last more than 1000 actuations.

Using a 5000mA battery or adding a small solar panel , will be
sufficient to increase the battery duration to 6 12 month.

We have performed several test to measure range of LoRa SmartSolenoids!

Range is far superior from the one of BLE units and span in open air
from 300m to 2 km. Test has show that RSSI (receiver signal strength
indicator) is highly dependent on antenna and his position. Most LoRa
modules have a built-in helical dipole antenna and give his best if
mounted vertical on a metallic structure at least 1mt over the ground
surface. Obstacles can greatly limit the range and it is therefore
better to locate antennas in LOS (line of sight). In order to allow a
more free positioning of SmartSolenoid units we have developed a node
mesh SW : remote units can be controlled thanks to other units relaying
the commands to the unreachable devices. This way you can locate
SmartSolenoids underground, inside building, or in any area out of
controller sight.

SW is open source and available on GitHub.com/pbecchi/smartsolenoidsmall
, the code is equivalent to the BLE version and use same API and is
compatible to a modified version of OpenSprinkler code that can control
remote LoRa units.

**Hardware**

HW details are available on github.com/pbecchi/SmartSolenoid .

![](.\/media/image2.jpeg){width="4.291509186351706in"
height="2.4480741469816274in"}

A set of prototype boards compatible to Fanstel modules and to
ArduinoLora have been built and assembled. Recently using
stereolitography we have built a proof of concept waterproof
Smartsolenoid enclosure that contain in addition to the solenoid coil
the PCB and the batteries.

![](.\/media/image3.jpeg){width="5.364583333333333in"
height="2.8020833333333335in"}

New production boards will be shortly available and will be integrated
in the same waterproof containers. Production enclosures require a high
initial investment due to tooling cost, production will be started when
we will reach sufficient requests.

![](.\/media/image4.jpeg){width="3.9583333333333335in"
height="3.0729166666666665in"}

As simpler alternative, for 2+ solenoid units, a standard waterproof box
with or without solarpanel is available. The Box will be mounted near to
the existing latching valve and will be wired to it.

You can find information on SmartSolenoid units in
smartgarden.cloud/SmartSolenoid.

SmartSolenoids will be controlled by a controller transmitter unit or by
an Esp32 OpenSprinkler.

**OpenSprinkler**

OpenSprinkler 2.1.7 code has been ported to Esp32 MCU. This code is
derived from Esp8266 version and use Oled 128x64 graphic LCD.

The capability to control LoRa SmartSolenoid has been added as an
optional special RF stations. You can associate each OpenSprinkler
station to a SmartSolenoid unit and without any wire you can operate,
from inside your home , several Smartsolenoids located in your garden
even 1000 m away. This way you can just get one Esp32 LoRa Oled unit and
run a full featured OpenSprinkler controller only using remote
LoraSmartsolenoid stations.

Two brand of Esp32 LoRa Oled modules are today available on the market
Heltec and TTGO and can be found here:

<https://www.banggood.com/Wemos-TTGO-LORA-SX1278-ESP32-0_96OLED-16-Mt-Bytes-128-Mt-bit-433Mhz-For-Arduino-p-1205930.html>

Esp32 OpenSprinkler code can be found on
GitHub.com/pbecchi/Esp32Opensprinkler/.
