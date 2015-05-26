# RTEP-2015---Raspberry-Pi-Project-Team-3-
This repository holds the files created and used for the Real Time Embedded Programming Mini Project using a Raspberry Pi and force sensing resistor
Pressure Sensor Code

The AD7705 communicates to the Raspberry Pi via SPI. This is
implemented through the device file /dev/spidev0.0.  As the ADC is a 16-bit variant the values are
sent to the Raspberry Pi as two 8-bit bytes and reconstructed through the readData()
function in adcreader.cpp on the Pi into the correct digital value. This format
is required as the maximum transaction period for SPI is 8 bits.

A key obstacle was overcome in receiving the ADC values and
then plotting them accordingly. The ADC sample rate is set to 100Hz whereas the
refresh rate of the QT program is 25Hz. As a result as the values are received
from the ADC they must be buffered before being used by the QT program. To
facilitate this is a circular buffer was implemented in adcreader.cpp. A
circular buffer is a software queue based on the First In First Out (FIFO)
principle [5]. This allows the quickly sampled ADC values to be stored until
the much slower QT program is ready to extract them for plotting purposes. The
reason the QT program does not sample them at a higher rate is because of the
accuracy of the QT timers. These are deemed as unreliable above 10-30Hz.

As part of the software implementation the following files
were used:   

main.c - The main program
initialises the different QT modules that are used and starts the data capture
procedure.

window.cpp - The "body” of the
final product. It creates the QT plot, knob and text fields. It takes in the
ADC values at a certain time and performs calculations if required.

window.h - Describes the different
functions and variables used within window.cpp.

adcreader.cpp - A program used to
communicate to the ADC via SPI and store the data in a buffer, which is later
used by window.cpp.

adcreader.h - A descriptor to the
adcreader program, detailing functions and variables used.

PressurePlot.pro - Creates the
make file called "Makefile”. When the makefile is run it creates the executable
called "PressurePlot”. Running "PressurePlot” starts the plotting application. 

The final product has three main different modes of
operation. The default is displaying the raw values taken in from the ADC, this
is set when the knob is set to 0. In this mode the values being received are
directly placed on the plot. The second mode is the Newton force mode in which
the knob set to 1. In this mode the values being received from the ADC are
converted using a formula. The current maximum force achieved is also monitored
and displayed on the screen as a text box on the left of the screen. The third
mode of operation using the threshold mode is when the knob set to 2. If the
raw value from the ADC is greater than 10,000, the threshold has been passed
and the value of 1 is plotted on the screen, if not 0 is displayed. The purpose
in this mode is to provide a simple visual indication of whether a pressure
threshold has been passed. This threshold is designed to be set to a pressure
value that is deemed to be too high for playing guitar, indicating that the
player is gripping the neck far too tightly.

As the values read in from the ADC represented pressure
values as a voltage level, a conversion to Newton's was required to allow a
unit of measurement to be plotted. The FSR402 force sensing resistor is a
widely used component and as a result has been used in hobby electronics to
measure pressure previously. Using a manufacturers guide provided by the
electronics manufacturer Adafruit [6] a conversion process was found. More
details can be found at FSR
Adafruit.
