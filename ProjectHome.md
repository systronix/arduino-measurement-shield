# Arduino Measurement Shield #

'<img src='http://arduino-measurement-shield.googlecode.com/files/shield.jpg' alt='Shield' />'


## Summary: ##

The Arduino Measurement Shield is a low cost, 20-bit precision, full measurement solution for Arduino. Many sensing applications require precise voltage measurement, or measurement of voltages on the scale of a few millivolts (i.e. a Wheatstone bridge or thermocouple). Most commercially available measurement solutions are expensive and difficult to interface, which can be prohibitive to those operating on a small budget or limited time frame. The Arduino Measurement Shield is designed so students, hobbyists, and  rofessionals alike can implement precision measuring systems as easily as
possible.

## Applications of the Shield: ##
  * Weigh scales
  * Thermocouples
  * Load cells
  * Pressure transducers
  * Strain gauges
  * Resistance Temperature Detectors
  * ...and more!

## Features: ##

  * 20-bit bipolar sigma-delta ADC
  * Input signal conditioning and filtering performed on the shield
  * Software programmable gain from 1 to 128
  * Up to 470Hz output rate
  * Separate low-noise supply available for powering sensors
  * Internal or external voltage reference
  * Selectable current sources for resistance sensor measurement
  * Compatible with 2,3, or 4-wire resistance sensors
  * Interchangeable front-end input modules for future expansion
  * Multiple Measurement Shields can be used at once, and in combination with other Arduino shields.
  * Hardware and software is open source.
  * Arduino library and LabVIEW VI's available for easy use.


### Example Arduino Sketch: ###
```
#include "AD7785.h"
#include <SPI.h>

/* Construct AD7785 Class */
AD7785 AD7785(5);

void setup(){
  /* Initialize ADC */
  if ( !AD7785.Init() ) {
    // Error, AD7785 not detected  
  } else {  
    /* Configure ADC */
    AD7785.Config(AD7785_CLK_INT, 
                  AD7785_RATE_470, 
                  AD7785_GAIN_128, 
                  AD7785_VBIAS_DISABL, 
                  AD7785_REFSEL_INT, 
                  0, 
                  AD7785_EN_IXCEN_DISABL);
  
    /* Set Continuous Conversion Mode */
    AD7785.SetMode(AD7785_MODE_CONT);  
  }    
}

void loop(){
  unsigned long conv;
  
  /* Wait for available conversion, print to serial port, loop */
  conv = AD7785.GetConversion();
  Serial.print(conv);
}
```