# STC-1000-Arduino-Temperature-Controller
STC-1000 Style temperature controller
This system uses a arduino board with NTC temperature sensors and a VGA video module(OctaPentaVeega board) to display the data on a VGA monitor.
Built this unit control a ice maker to cool my K40 laser engraver.
Found it to work very well.

The comments out of the code.
/*
   June 30,2020 "Wanderingmoose Tinkering"
   *****IceMaker K40 Chiller Controller ****
           ***** V 6.10 Final *****
             This version changed epprom from write to update to increase eeprom life****
  STC-1000 Style cooling temperature controller (found a help site, do not remember where, might have been a forum)
  Features:
  Save setpoints in eeprom for temp, swing, compressor timer and other menu items.
  Recommend using a seperate program to format eeprom before loading this program. *****or results may vary*****
  Recommend makeing a script and loading into the Arduino to write the values needed, then loading this script. One is supplied below.
  Simple code to write the eeprom for the first time. ONLY NEED TO LOAD THIS SCRIPT ONCE IN THE ARDUINO to format the eeprom.
              ----------------------------------------------------------------------------------------
  -----copy into new window and load into arduino. only takes seconds to achieve,  Then load the main program into the Arduino.-------
  #include <EEPROMex.h>
  #include "Arduino.h"
  void setup()
  { EEPROM.writeFloat(0, 20);   //address 0
  EEPROM.writeFloat(4, 2);    //address 4
  EEPROM.writeInt(8, 30);     //address 8
  EEPROM.writeFloat(12, 25);  //address 12
  EEPROM.writeFloat(16, 15);  //address 16
  EEPROM.writeInt(20, 1);     //address 20
  EEPROM.writeInt(24, 1);     //address 24
  EEPROM.writeInt(28, 1);     //address 28
  EEPROM.writeInt(32, 1);     //address 32  }
  void loop()
  { // Nothing to do during loop }
  ---------------------------------------------------------------------------------------------------------------------------
            ----------------------------------------------------------------------------------------
  ***Outputs***
  Output for Alarm relay and LO disable laser
  Output for Buzzer
  Output for compressor control
  VGA Display support using OctaPentaVeega board. Pin 8 serial output(32x16 character display using VGA monitor).
    -Great for across the room viewing or blind people like me!
  ***Inputs****
  Four switch pad so not using the left button. But still works great for me. (designed for a 5 button switches)
  Pulse flow meter
  2xThermistor 10k. First Temp is for cooling compressor control, the second is for visual info.
              +5volts
              |
              |
              10k Thermister
              |
              |
  Analog Ax---
              |
              |
              10k ohm resistor
              |
              |
              GND
  ***Libraries***
  EEPROMex for eeprom https://playground.arduino.cc/Code/EEPROMex/
  Thermistor used https://github.com/panStamp/thermistor
  SoftwareSerial.h generic one in the interface
  OctaPentaVeega module can be found at https://github.com/rakettitiede/octapentaveega
  Built the B&W module for this project and have the information on the VGA monitor. Pretty slick.


           +5v
              |
             2k2
              |
  Analog A0---   ---- Button1 ---- |
              |                   |
            620ohm                |
              |                   |
                ---- Button2 ---- |
              |                   |
             1k2                  |
              |                   |
                ---- Button3 ---- |
              |                   |
             3k3                  |
              |                   |
              | ---- Button4 ---- |
                                  |
                                  |
                                Ground

  Menu: All done with code in the main loop
  Set Temperature--> Set Temp--> Swing Set--> Comp Delay--> High Temp Alarm--> Low Temp Alarm--> Min Flow--> Door--> Buzzer--> Alarms--> EXIT



*/

