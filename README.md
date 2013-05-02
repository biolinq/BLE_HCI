BLE_HCI
=======

Allows external MCU to connect BLE (CC2540) using Bluetooth HCI such as Windows/Linux/Mac, Arduino, Respberry Pi, etc.

The libraries was written for Python and Arduino. Tested on Windows and Mac OS X, but this is still a work in progress, not all HCI commands and events have been implemented or fully tested.

Example 1
=========

PC/Mac as BLE central role and via the BLE link, connecting to BLE Mini running Biscuit firmware as peripheral role

Typical connections:<br/>
1. PC <-> USB <-> BLE Mini (HCI) <----- BLE Link ------> BLE Mini (Biscuit) <-> Serial <-> Ardino<br/>
2. Mac <-> USB <-> BLE Mini (HCI) <----- BLE Link ------> BLE Mini (Biscuit) <-> USB <-> Raspberry Pi<br/>
3. Raspberry Pi <-> USB <-> BLE Mini (HCI) <----- BLE Link -----> BLE Mini (Biscuit) <-> Serial <-> Arduino

Requirements:<br/>
1. A PC running Windows, Linux or a Mac running Mac OS X<br/>
2. Raspberry Pi with Linux is also possible<br/>
3. HCI firmware (USB) and Biscuit firmware (USB or Serial)<br/>
4. Two BLE Mini boards, first one running the HCI firmware, another one running the Biscuit firmware<br/>
5. Install Python 2.7.2 32-bit<br/>
6. Install PySerial 2.5<br/>
7. For Windows, install USB CDC driver<br/> 
8. Biscuit central Python script

How it works:<br/>
When you connect the BLE Mini (HCI) to your PC via the USB port, it will function as an USB CDC (Virtual COM Port). On Windows, it will ask for a device driver, so you need to install the USB CDC driver. It shows as a COM port (e.g. COM5). For Linux or Mac OS X, it will work as a tty device (e.g. ttyACM0 or tty.usbmodem1311).<br/>

The Biscuit central Python script controls the virtual COM port, sending BLE command over the port, and listening to the HCI events.<br/>

Example 2
=========

Arduino as BLE central role and via the BLE link, connecting to BLE Mini running Biscuit firmware as peripheral role

Typical connections:<br/>
1. Arduino (A) <-> Serial <-> BLE Mini (A) <----- BLE Link -----> BLE Mini (B) <-> Serial <-> Arduino (B)<br/>
2. Arduino (A) <-> Serial <-> BLE Mini (A) <----- BLE Link -----> BLE Mini (C) <-> USB <-> Raspberry Pi

* Suggest to use Arduino Leonardo or other boards with more than one serial to try this example.
* We use the USB CDC serial for debug/UI and one for connecting to the BLE Mini on Leonardo board.
* Uno has only one serial and we do not use SoftwareSerial because sometimes data recevied incorrectly.<br/>
  -> We used AltSoftSerial, so Uno works now, but the baudrate limited to 57600bps.<br/>
  -> http://www.pjrc.com/teensy/td_libs_AltSoftSerial.html<br/>
* Tested with Uno (use pin 8, 9), Leonardo (use pin 0, 1), Mega 2560 (use TX1, RX1)

Requirements:<br/>
1. BLE HCI library for Arduino<br/>
2. Arduino (A) running HCI library<br/>
3. AltSoftSerial (requred for Arduino Uno)<br/>
4. BLE Mini (A) running HCI firmware (Serial)<br/>
5. BLE Mini (B or C) running Biscuit firmware (Serial or USB)
