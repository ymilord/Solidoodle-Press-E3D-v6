# E3D v6 Ready Firmware & Parts for the Soildoodle Press

This repo will have two versions. One Bowden and one direct drive. The in Firmware folder I've place a dump of the stock (shipping) firmware for the Press & a E3D Prepped verison. 

Notice : This is for the folks that are experienced in uploading arduino sketches/hex files to AVR's. If any of this sounds foreign or complicated- Not not attempt. <b>I will not provide support. Any damages/issues that you cause will be at your own risk.</b> (Sorry, got to say it.)

Installation:

This was done with a USBTinyISP connected to a RPI B+. (If you are using OctoPi and have a USBTinyISP this is by far the easiest method.) Of course there are other methods to do this. Use what ever workflow works best for you. This is a document of what I've done.

On the Press' controller, The right header is for the ATTINY2313 (Pin 1 is right) the left header is for the AT90USB1286 (Pin 1 is left). The ATTINY2313 can be pulled directly (no jumpers) but the AT90USB1286 needs a jumper in JP1 in order for you to read/write the firmware via the ICSP header.

If you want to make your own backup of the stock firmware, On the RPi create a folder where you'd like to store the backup. If you are using OctoPi I'd suggested creating a folder tree ~/pi/Press_Firmware/Stock/ & ~/pi/Press_Firmware/Modded/. 'Stock' to store the backup and 'Modded' to store the firmware provided here. 

To create your own backup run:

cd ~/pi/Press_Firmware/Stock/

avrdude -c avrisp -b 250000 -i 10 -p AT90USB1286 -P /dev/ttyACM0 -F -U flash:r:factory_press_AT90USB1286.hex:i

This will read the firmware on the Press and dump that data to a HEX file called 'factory_press_AT90USB1286.hex' in that folder.

To flash the modified firmware to the Press navigate to the folder where you placed the modded firmware. (i.e. ~/pi/Press_Firmware/Modded')

And run: 

avrdude -c avrisp -b 250000 -i 10 -p AT90USB1286 -P /dev/ttyACM0 -F -U flash:w:Solidoodle_Press_Modified_Firmware.cpp.hex:i
