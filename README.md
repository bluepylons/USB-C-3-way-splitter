# USB-C-3-way-splitter
Work in progress. This design has been prototyped and needs another round of prototyping as it does not currently work. 

This is a splitter board (for making a cable splitter) for turning a 5V 3A USB-C power source to 3 5V 1A USB sources. This is for using a single-port USB PD charger to charge multiple 5V USB-C devices at once. I often travel with a single 45W USB-C charger and cable for all my devices (phone, laptop, camera, flashlight, power bank, etc.), but having just one cable is often limiting when I need to charge everything overnight, and many of my devices only charge off 5V and don't need that many watts. This splitter board and cable is for charging those devices simultaneously, without needing a bulkier multi-port charger and multiple cabls.
 
This implements proper CC line monitoring using a 1.25V voltage reference, a comparator, and a high-side power switch. The outputs should only be turned on once the CC line voltage is determined to be above 1.25V, indicating that the source can safely supply 3A per the USB-PD standard. Otherwise, the outputs are off. The outputs have D+ and D- shorted to indicate that they can supply 1A of current (per the USB Battery Charging standard). 

