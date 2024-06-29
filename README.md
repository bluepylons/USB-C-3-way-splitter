# USB-C-3-way-splitter

![picture](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Graphics/DSC_1433.JPG?raw=true)

Build and use this at your own  risk.

This is a USB-C splitter that turns a 5V 3A-capable USB-C power source to 3 5V 1A USB sources. This is for using a single-port USB-C PD charger to charge multiple 5V USB-C devices at once. Files are done in KiCAD 8, and manufacturing files for JLCPCB are provided. An enclosure design is included. 

This design has been prototyped and  tested. 

## Background
With the widespread prevalance of USB-C, I can now travel with a single compact 45W USB-C GaN charger and  cable, and charge all my devices (phone, laptop, camera, flashlight, power bank, headphones, etc.). However, having a single cable and single charger is often limiting when I need to charge multiple devices (especially overnight), and many USB-C devices only need 5V and not many watts. This splitter board is for charging those devices simultaneously with a single charger, without needing a bulkier multi-port charger and multiple cables.

## Design
The splitter only powers on with USB-C inputs capable of supplying 5V 3A. This is done by monitoring the USB-C CC lines and checking that the signal there is greater than 1.25V. Under the USB-PD standard, if the voltage on the CC pin [is greater than 1.31V](https://hackaday.com/2023/01/04/all-about-usb-c-resistors-and-emarkers/), it indicates the source is capable of supplying 5V 3A. Only then are the outputs powered on (as indicated by the green LED). Otherwise, the outputs are turned off. The outputs have D+ and D- shorted to indicate that they can supply 1A of current (per the USB Battery Charging standard). 

The CC line voltage checking is done by a pair of comparators that monitor each of the 2 CC lines (as the USB-C input cable can be plugged in either way). The CC line voltage are compared against a 1.25V reference voltage (provided by an ST TS4061AICT-1.25 shunt reference). The output of the comparators are fed to the ENABLE input on an SiP32509 high-side switch that turns the outputs on and off. The input is over-current protected by a 3A resettable fuse. 

Note that the output cables need 56K pull-up resistors between output CC and 5V. USB-A to USB-C cables are required to include this resistor, so using the USB-C end from a cut-up USB-A to C cable is recommended for the output cables. 

A 3D-printed enclosure design is supplied in the Enclosure folder. The enclosure design is meant to be 3D-printed in two halves; on prototypes this was printed with PETG. The lower enclosure features embedded M3 nuts - the print must be paused at the appropriate layer and M3 nuts need to be inserted before the print resumes. The two halves are screwed together with M3x8 countersunk screws. The enclosure is designed to use [Ikea  SITTBRUNN](https://www.ikea.com/us/en/p/sittbrunn-usb-a-to-usb-c-light-yellow-80539483/) USB-A to USB-C cables (as these are widely available and inexpensive), wrapped in Qualtek Q5-3X-3/16-01-QB48IN-25 heatshrink as strain relief. To dissipate heat from the SiP32509 high-side switch (U2), which is expected to generate about 0.4W at 3A, either the enclosure must be pottetd, or thermal pads must be used between the SiP32509 and the case. Lower-enclosure-potted has a small hole to inject potting compound (or hot glue, or silicone) into the case - use a high viscosity potting compound to avoid it getting in the input USB-C connector. Lower-enclosure-thermal-pad has a small ledge to place a 1.5mm thick thermal pad between U2 and the case. 

# ORDERING GUIDE

## Bill Of Materials

Work in progress 
**Custom Parts**
| Description                                                                                                                                                                                                                                           | Quantity  | Notes | 
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | - |
| [PCB](https://github.com/bluepylons/USB-C-3-way-splitter/tree/main/Manufacturing%20files)                                                                                                                                                             | 1         |   | 
| [Upper enclosure](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Enclosure/Upper-enclosure.3mf)                                                                                                                                         | 1         |   |
| Lower enclosure ([thermal pad](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Enclosure/Lower-enclosure-thermal-pad.3mf) or [potted](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Enclosure/Lower-enclosure-potted.3mf) | 1         | Has 4 embedded M3 nuts, which must be installed while 3D printing | 

The PCB can be ordered from JLCPCB.

[JLCPCB ordering guide]


**Off-the-shelf parts**

| Description                                                                                                         | Part number -----------------------------| Quantity | Notes                                         | 
| ------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- | -------- | --------------------------------------------- |
| [Ikea Sittbrunn USB-A to USB-C cable](https://www.ikea.com/us/en/p/sittbrunn-usb-a-to-usb-c-light-yellow-80539483/) | Ikea 805.394.83                          | 3        |                                               | 
| M3 hex nut, DIN 934, zinc-plated steel                                                                              | McMaster-Carr 90591A250                  | 4        | Generic. Not stainless steel to avoid galling |
| M3x8 flat head screw, DIN 7991 / ISO 10642, hex drive, 18-8 stainless steel                                         | McMaster-Carr 92125A128                  | 4        | Generic.                                      |
| Adhesive-lined heat-shrink, 3/16" / 4.8mm ID, 3:1 shrink ratio                                                      | Qualtek Qualtek Q5-3X-3/16-01-QB48IN-25  | 3x 25mm  |                                               |

# BUILD GUIDE

Work in progresss
