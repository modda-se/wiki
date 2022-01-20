# Freepad - Flash CC2531 with Raspberry Pi
You can flash a CC2531 chip without having a specific programmer. Use a Raspberry Pi instead! This is a simplified guide on how to do just that. 

Credut and orignal source here: 

https://github.com/diyruz/freepad
                
https://modkam.ru/2019/11/13/pult-zigbee-v2-prosto-otlomi-lishnee/#more-1264


## Preparation

This guide will asume that you already have your Rpi setup and SSH enabled. 

* First, make sure `wiringPi` are installed: 

        sudo apt-get install wiringpi

* Also git:

        sudo apt install git

* Download `flash_CC2531`: 

        git clone https://github.com/jmichault/flash_cc2531.git

 * Go inside the folder:

        cd flash_cc2531

* and finally download the `DIYRuZ_FreePad.hex` firmware: 

        curl "https://github.com/diyruz/freepad/releases/download/2.0.7/DIYRuZ_FreePad.hex" > freepad.hex


## Installation

* Connect the following pins from the Raspberry Pi to the PCB:

        Rpi PIN 1 (3.3V)     -->   PCB PIN 1 (VCC)
        Rpi PIN 35 (GPIO19)  -->   PCB PIN 2 (RST)
        Rpi PIN 38 (GPIO20)  -->   PCB PIN 3 (DD)
        Rpi PIN 36 (GPIO16)  -->   PCB PIN 4 (DC)          
        Rpi PIN 39 (GND)     -->   PCB PIN 5 (GND)   
   
## Programming

Test by running: 

        ./cc_chipid

it should return something like:

          ID = b524.

If you see 0000 or ffff, something is wrong and you should probably check your wiring.

Erase and flash the CC2531:

        ./cc_erase
        ./cc_write freepad.hex

Wait for it to finish and then your done! 


