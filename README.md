# USB-C-3-way-splitter

Build and use this at your own  risk.

This is a USB-C splitter that turns a 5V 3A-capable USB-C power source to 3 5V 1A USB sources. This is for using a single-port USB PD charger to charge multiple 5V USB-C devices at once. Files are done in KiCAD 8, and manufacturing files for JLCPCB are provided. An enclosure design is included.

This is a work in progress. As of May 30th, 2024, The second revision has been prototyped, and the splitter functionality works. It needs some thermal verifiaction to ensure that temperatures on the SiP32509 high-side switch are acceptable when the full 3A are being drawn. A 3rd PCB revision with ESD protection(in the V3 folder) has its design done, but has not yet been prototyped. 

With the widespread prevalance of USB-C, I can now travel with a single compact 45W USB-C GaN charger and  cable, and charge all my devices (phone, laptop, camera, flashlight, power bank, headphones, etc.). However, having a single cable and single charger is often limiting when I need to charge multiple devices (especially overnight), and many USB-C devices only need 5V and not many watts. This splitter board is for charging those devices simultaneously with a single charger, without needing a bulkier multi-port charger and multiple cables.

The splitter only powers on with USB-C inputs capable of supplying 5V 3A. This is done by monitoring the USB-C CC lines and checking that the signal there is greater than 1.25V. Under the USB-PD standard, if the voltage on the CC pin [is greater than 1.31V](https://hackaday.com/2023/01/04/all-about-usb-c-resistors-and-emarkers/), it indicates the source is capable of supplying 5V 3A. Only then are the outputs powered on (as indicated by the green LED) turning on. Otherwise, the outputs are turned off. The outputs have D+ and D- shorted to indicate that they can supply 1A of current (per the USB Battery Charging standard). 

The CC line voltage checking is done by a pair of comparators that monitor each of the 2 CC lines (as the USB-C input cable can be plugged in either way). The CC line voltage are compared against a 1.25V reference voltage (provided by an ST TS4061AICT-1.25 shunt reference). The output of the comparators are fed to the ENABLE input on an SiP32509 high-side switch that turns the outputs on and off. The inputs are over-current protected by a 3A resettable fuse. There is currently no ESD protection on the inputs. 

Note that the output cables need 56K pull-up resistors between CC and 5V. USB-A to USB-C cables are required to include this resistor, so using the USB-C end from a cut-up USB-A to C cable is recommended for the output cables. 

A 3D-printed enclosure design is supplied in the Enclosure folder. The enclosure design is meant to be 3D-printed in two halves. The lower enclosure features embedded M3 nuts - the print must be paused at the appropriate layer and M3 nuts need to be inserted before the print resumes. The two halves are screwed together with M3x8 countersunk screws. The enclosure is designed to use [Ikea  SITTBRUNN](https://www.ikea.com/us/en/p/sittbrunn-usb-a-to-usb-c-light-yellow-80539483/) USB-A to USB-C cables (as these are widely available and inexpensive), wrapped in Qualtek Q5-3X-3/16-01-QB48IN-25 heatshrink as strain relief. To dissipate heat from the SiP32509 high-side switch (which is expected to generate about 0.4W at 3A), either the enclosure must be pottetd, or thermal pads must be used between the SiP32509 and the case. Lower-enclosure-potted has a small hole to inject potting compound (or hot glue, or silicone) into the case - use a high viscosity potting compound to avoid it getting in the input USB-C connector. Lower-enclosure-thermal-pad has a small ledge to place a 1.5mm thick thermal pad.

![thermal pad location](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Graphics/thermal-pad-location.PNG?raw=true)



