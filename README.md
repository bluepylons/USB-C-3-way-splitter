# USB-C-3-way-splitter

Work in progress. As of May 4th, 2024, The second revision has been prototyped, and the splitter functionality works. It needs some thermal verifiaction to ensure that temperatures on the SiP32509 high-side switch are acceptable when the full 3A are being drawn. A 3rd revision with ESD protection is being prototyped.

This is a splitter board (for making a cable splitter) for turning a 5V 3A-cabale USB-C power source to 3 5V 1A USB sources. This is for using a single-port USB PD charger to charge multiple 5V USB-C devices at once. Files are done in KiCAD 8, and manufacturing files for JLCPCB are provided. 

With the widespread prevalance of USB-C, I can now travel with a single compact 45W USB-C charger and  cable, and charge all my devices (phone, laptop, camera, flashlight, power bank, headphones, etc.). However, having a single cable and single charger is often limiting when I need to charge multiple devices (especially overnight), and many only need 5V and not many watts. THis splitter board is for charging those devices simultaneously with a single charger, without needing a bulkier multi-port charger and multiple cables.

The splitter only powers on with USB-C inputs capable of supplying 5V 3A. This is done by monitoring the USB-C CC lines and checking that the signal there is greater than 1.25V, which under the USB-PD standard indicates the source is capable of supplying 5V 3A. Only then are the outputs powered on (as indicated by the green LED) turning on. Otherwise, the outputs are turned off. The outputs have D+ and D- shorted to indicate that they can supply 1A of current (per the USB Battery Charging standard). 

The CC line voltage checking is done by a pair of comparators that monitor each of the 2 CC lines (as the USB-C input cable can be plugged in either way). The CC line voltage are compared against a 1.25V reference voltage (provided by an ST TS4061AICT-1.25 shunt reference). The output of the comparators are fed to the ENABLE input on an SiP32509 high-side switch that turns the outputs on and off. The inputs are over-current protected by a 3A resettable fuse. There is currently no ESD protection on the inputs. 

Note that the output cables need 56K resistors between CC . USB-A to USB-C cables are required to include this resistor, so using the USB-C end from a cut-up USB-A to C cable is recommended for the output cables. 

A 3D-printed enclosure design is supplied in the Enclosure folder. As of May 4th, 2024, this has been printed and assembled but not yet tested. The enclosure design is meant to be 3D-printed in two halves. The lower enclosure features embedded M3 nuts - the print must be paused at the appropriate layer and M3 nuts need to be inserted before the print resumes. The two halves are screwed together with M3x8 countersunk screws. The enclosure is designed to use [Ikea  SITTBRUNN](https://www.ikea.com/us/en/p/sittbrunn-usb-a-to-usb-c-light-yellow-80539483/) USB-A to USB-C cables (as these are widely available and inexpensive), wrapped in Qualtek Q5-3X-3/16-01-QB48IN-25 heatshrink as strain relief. The small hole on the lower enclosure is for potting the circuit board (either with potting compound, hot glue, or epoxy) to improve the heat dissipation from the SIP32509 switch. 

Build and use this at your own  risk.

