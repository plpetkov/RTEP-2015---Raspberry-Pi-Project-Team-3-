# RTEP-2015---Raspberry-Pi-Project-Team-3-
This repository holds the files created and used for the Real Time Embedded Programming Mini Project using a Raspberry Pi and force sensing resistor


Test / demo program for the AD7705
==================================

This program switches on the clock from the RPI, 
triggers a calibration of the AD, 
reads data from channel 1 and 
prints it on the screen.

Note: this program uses DRDY connected to Port 22
Make sure you use the new PCB layout from:
http://web.eng.gla.ac.uk/rpi/


Making it work
--------------

To build:

    make

Run it with the command:

    sudo ./ad7705_test


Associated website:
http://web.eng.gla.ac.uk/rpi/
