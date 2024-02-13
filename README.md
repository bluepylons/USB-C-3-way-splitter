# USB-C-3-way-splitter
 A splitter board (for making a cable splitter) for turning a 5V 3A USB power source to 3 5V 1A USB sources (with D+ and D- lines shorted). This is for using single-port USB PD chargers to charge multiple 5V devices at once.
 
 This implements proper CC line monitoring using a 1.25V voltage reference, a comparator, and a high-side power switch. The outputs should only be turned on once the CC line voltage is determined to be above 1.25V, meaning that the source can supply 3A. 
