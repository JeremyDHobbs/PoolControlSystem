# PoolControlSystem
ESP8266 16channel Relay to control pumps and values

This board has 16 relays that are available in Normal Closed (NC) or Normal Open (NO).  For these devices, I want to utilize the NC position.  

## Summary of parts and equipment
I am using actuators puchased from Amazon and have a combination of Swimables, Tork, and TPE24VA. They all seem to work identical from a wiring perspective.

The 24vac Pool Value actuators use a three wire system. Black, White, Red
Black is the common. When you apply voltage through the black to either the white or Red it will turn the actuator in one direction or the other. Im using two relays to control one actuator. 

---
Pool pumps equipment is:
Black and Decker 3hp varible speed pumps
Replace the control panel on the pumps with an automation capable controller. It is an exact patch for the control and works perfectly.
https://poolpartstogo.com/products/automation-variable-speed-adapter?_pos=6&_sid=be0c76efc&_ss=r

The pool pumps automation controller has a four wire system. Black, White, RED, Yellow
Red is 5vac that comes from the pump control panel.  When you connect Red to one of the other colors, it will enable one of the first three speed selection on the pump.  The speeds have to be manually set on the pump control interface.  

## Power for  the ESP8266 board and actuators
For the ESP8266 board I am running a usb cable from a 5v block.
For the actuators I am utilizing a 24V 40VA Control Transformer to step down the voltage. 
Since I needed to utilize the voltage coming from the trasformer for many relays, I decided to use some 18g wire and "Quick Splice Disconnect Wire Terminals T-Tap Spade" connectors.  


## Automations
Automations will be configured through both HomeAssistant and ESPHome.  HomeAssistant is great for standard automations like changing speeds of the pumps during the day for cleaning. However more advanced automations, like changing the value positions, I perfer to keep in ESPHome so that there is not a chance of two relays getting activated at the same and causing damage to the pumps or acuators.

## Initial Setup of ESP8266 16channel Board
I started with loading the 16ChannelArduino.ino file through the Arduino IDE via USBC cable to the board. To be able to access the board through the USDC cable, I had to load the CH341SER driver. This allowed the USB port to act like a COM port.  I then use the pool-value-control.yaml file with the ESPHome command line utility to run the command
~~~ 
esphome run pool-value-controls.yaml device COM6 
~~~
Once uploaded onto the board, I was able to manage the config through ESPHome Web Interface.

## User Interface
Im using HomeAssistant as my primary interface for all controls.  
One I apply the ESPHome configuration initially with a USBC cable, then I can manage it via the ESPHome interface. Then any configuration is automatically added to my HomeAssistant. 


