# USB-C 3-way-splitter

![picture](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Graphics/Overview.JPG?raw=true)

*Disclaimer* - Build and use this at your own  risk. I am not responsible for anything that arises from use of these files or guide, or for anything that arises from constructing and using this device.

This is a USB-C splitter that splits a 5V 3A-capable USB-C power source to 3 5V 1A  sources. This is for using a single-port USB-C PD charger to charge multiple 5V USB-C devices at once. Files are done in KiCAD 8, and manufacturing files for JLCPCB are provided. An enclosure design is included. 

This design has been prototyped and  tested. 

## Background
With the widespread prevalance of USB-C, I can now travel with a single compact 45W USB-C GaN charger and  cable, and charge all my devices (phone, laptop, camera, flashlight, power bank, headphones, etc.). However, having a single cable and single charger is often limiting when I need to charge multiple devices,especially overnight, and many USB-C devices only need 5V and not many watts. This splitter board is for charging those devices simultaneously with a single charger, without needing a bulkier multi-port charger and multiple cables.

## Design
The splitter only powers on with USB-C inputs capable of supplying 5V 3A. This is done by monitoring the USB-C CC lines and checking that the signal there is greater than 1.25V. Under the USB-PD standard, if the voltage on the CC pin [is greater than 1.31V](https://hackaday.com/2023/01/04/all-about-usb-c-resistors-and-emarkers/), it indicates the source is capable of supplying 5V 3A. Only then are the outputs powered on (as indicated by the green LED). Otherwise, the outputs are turned off. The outputs have D+ and D- shorted to indicate that they can supply 1A of current (per the USB Battery Charging standard). 

The CC line voltage checking is done by a pair of comparators that monitor each of the 2 CC lines (as the USB-C input cable can be plugged in either way). The CC line voltage are compared against a 1.25V reference voltage (provided by an ST TS4061AICT-1.25 shunt reference) - a 1.31V voltage reference would have been more precise, but were not easily available, and 1.25V is above the 1.16V cutoff for a 1.5A source and works fine. The output of the comparators are fed to the ENABLE input on an SiP32509 high-side switch that turns the outputs on and off. The input is over-current protected by a 3A resettable fuse. 

Note that the output cables need 56K pull-up resistors between output CC and 5V. USB-A to USB-C cables are required to include this resistor, so using the USB-C end from a cut-up USB-A to C cable is recommended for the output cables. 

A 3D-printed enclosure design is supplied in the Enclosure folder. The enclosure design is meant to be 3D-printed in two halves; on prototypes this was printed with PETG. The lower enclosure features embedded M3 nuts - the print must be paused at the appropriate layer and M3 nuts need to be inserted before the print resumes. The two halves are screwed together with M3x8 countersunk screws. The enclosure is designed to use [Ikea  SITTBRUNN](https://www.ikea.com/us/en/p/sittbrunn-usb-a-to-usb-c-light-yellow-80539483/) USB-A to USB-C cables (as these are widely available and inexpensive), wrapped in Qualtek Q5-3X-3/16-01-QB48IN-25 heatshrink as strain relief. To dissipate heat from the SiP32509 high-side switch (U2), which is expected to generate about 0.4W at 3A, either the enclosure must be pottetd, or thermal pads must be used between the SiP32509 and the case. Lower-enclosure-potted has a small hole to inject potting compound (or hot glue, or silicone) into the case - use a high viscosity potting compound to avoid it getting in the input USB-C connector. Lower-enclosure-thermal-pad has a small ledge to place a 1.5mm thick thermal pad between U2 and the case. 

# ORDERING GUIDE

## Bill Of Materials

Work in progress 
### Custom Parts
| Description                                                                                                                                                                                                                                           | Quantity  | Notes | 
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | - |
| [PCB](https://github.com/bluepylons/USB-C-3-way-splitter/tree/main/Manufacturing%20files)                                                                                                                                                             | 1         | See "Ordering the PCB" section below  | 
| [Upper enclosure](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Enclosure/Upper-enclosure.3mf)                                                                                                                                         | 1         | 3D-printed  |
| Lower enclosure ([thermal pad](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Enclosure/Lower-enclosure-thermal-pad.3mf) or [potted](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Enclosure/Lower-enclosure-potted.3mf)) | 1         | 3D-printed. Has 4 embedded M3 nuts, which must be installed while 3D printing | 

The 3D-printed parts were FDM 3D-printed in PETG, though other materials probably work fine here. A translucent or semi-translucent material is recommended so that the indicator LEDs can shine through. 


## Off-the-shelf parts

| Description                                                                                                         | Part number                              | Quantity | Notes                                         | 
| ------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- | -------- | --------------------------------------------- |
| [Ikea Sittbrunn USB-A to USB-C cable](https://www.ikea.com/us/en/p/sittbrunn-usb-a-to-usb-c-light-yellow-80539483/) | Ikea 805.394.83                          | 3        |                                               | 
| M3 hex nut, DIN 934, zinc-plated steel                                                                              | McMaster-Carr 90591A250                  | 4        | Generic. Not stainless steel to avoid galling |
| M3x8 flat head screw, DIN 7991 / ISO 10642, hex drive, 18-8 stainless steel                                         | McMaster-Carr 92125A128                  | 4        | Generic.                                      |
| Adhesive-lined heat-shrink, 3/16" / 4.8mm ID, 3:1 shrink ratio                                                      | Qualtek Qualtek Q5-3X-3/16-01-QB48IN-25  | 3x 25mm  |                                               |

If you are using the ther

## Ordering the PCB

The PCB can be ordered from [JLCPCB](https://jlcpcb.com/) in China, and the files are provided in their format. 

1.)  Go to JLCPCB, and press "Order Now". 
![](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Graphics/Ordering%20guide/1-JLCPCB-home.png?raw=true)

2.) Next, you want to upload the [Gerber ZIP file](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/PCB%20manufacturing%20files/V3%20Gerbers.zip) for the PCB. 
![](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Graphics/Ordering%20guide/2-add-gerbers.png?raw=true)

3.) Specify the following options once the Gerber file has uploaded. Non-default settings are highlighted in red. 
![](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Graphics/Ordering%20guide/3-JLCPCB-options.png?raw=true)

For color, specify a color supported by JLCPCB's ["Economic PCB Assembly"](https://jlcpcb.com/capabilities/pcb-assembly-capabilities). As of June 30, 2024, green, black, blue, red, white, and purple are supported. Note that some colors might incur an extra fee.

4.) Under "PCB Assembly", specify the following options:
![](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Graphics/Ordering%20guide/4-JLCPCB-options-2.png?raw=true)

5.) Press "Next":

![](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Graphics/Ordering%20guide/5-JLCPCB-next.png?raw=true)

6.) Upload the [BOM](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/PCB%20manufacturing%20files/JLCPCB-BOM.xls) and [CPL](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/PCB%20manufacturing%20files/JLCPCB-CPL.xls) files:
![](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Graphics/Ordering%20guide/6-BOM-CPL.PNG?raw=true)

7.) Confirm  the components in the next page. If any components are listed as "Shortfall", JLCPCB does not have enough of them in stock and will not install them on any PCBs. You will have to purchase them from and solder them on yourself. Alternatively, you can wait for JLCPCB to restock the part.
![](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Graphics/Ordering%20guide/7-COMPONENTS.PNG?raw=true)

8.) Next is the component placement confirmation page. You should not have to change anything here:
![](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Graphics/Ordering%20guide/8-COMPONENT-PLACEMENT.PNG?raw=true)

9.) You will need to describe the item in the next page for customs purposes. As of June 30th, 2024, I could not find an option most suitable for this, so select "Office Appliances and Accessories > Others" in the options, and type in "USB cable splitter PCB".
![](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Graphics/Ordering%20guide/9-customs-description.png?raw=true)
![](https://github.com/bluepylons/USB-C-3-way-splitter/blob/main/Graphics/Ordering%20guide/10-customs-description-2.png?raw=true)

# BUILD GUIDE

## Tools needed 
| Tool           | Purpose                                                                                                                                                     |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | 
| Flush cutters  | Stripping wires, trimming leads                                                                                                                             |
| Soldering iron | Soldering the USB-C output cables to the PCB                                                                                                                |
| Solder         | You need it to solder
| Flux           | Makes tinning the output cables easier
| Heat gun       | For the heat-shrink strain relief
| Wire strippers | For stripping wire 

If you are using the thermal pad option for the lower case, you will need scissors. If you are using the potted option 
## Build process 
1.) Test the PCB with a 5V 3A-capable USB-C source. When plugged in, both the white and green LEDs should light up. Next, test it with a non-5V 3A capable source (e.g. use a USB-A cable). When plugged in, only the white LED should light up. 

2.) Unplug the PCB.

3.) Take the 
Work in progresss
