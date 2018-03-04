Erbse V01 (alternative Firmware for MI Branches)

Manual 
======
* Erbse (Euclid Random Branched SEquences)
* Erbse contains braches firmware with some add-ons.
* Original consists of two identical sections called Bernoulli gates with toggle and latch mode for each channel.

Add-on:
=======

Toggle v2:
-----------
 Original toggle was implemented as XOR from previouse outcome and current outcome. 
 Toggle v2 also works when previouse outcome and current outcome are low ( will toggle to high ) 

   
Pattern mode per channel:
-------------------------
 Hardware-in signal triggers an internal 16 step sequencer per channel.
 Original Bernouille random mode gets deactivated. Knob/CV controls pattern (1-32).
 Some patterns work as simple clock divider, some are derived from good old Shruthi.

Euclid sequencer mode:
-----------------------
 Hardware-in signal triggers internal 16 step euclid sequencer (one for both channels).
 Knob/CV channel 1 controls hits (0-32).
 Knob/CV channel 2 controls length (0-32).

Link mode:
----------
 Generated output from each channel overrides the Hardware-in signal from the other channel.
 Note:
 Option 1: Channel 1 is master, channel 2 is linked to channel 1.
 Option 2: Channel 2 is master, channel 1 is linked to channel 2.
 Both set as master is not possible! (due to physical limitation)

Priority:
----------
 Euclid pattern overrules random mode and pattern mode (knobs shared for both channels)
 Pattern mode per channel overrides random mode (per Channel)
 Random mode is automatically activeted if no pattern mode was selected.
 Link mode, Toggle, Toggle v2 and Latch can be combined. 

Leds indicate modes and selections:
-----------------------------------
 If a mode is actived Led lights for a sec.
 If a mode is turned off, Led blinks for a sec. 
 The led lights kind of dimmed while pressing the switch and 
 change the color to know what mode gets selected when releasing the switch.

Led light table: Single button handling:
* short press				Toggle mode		ON   GREEN				
* short press				Toggle mode		OFF  BLINK GREEN		
* long press				Latch mode		ON   RED				
* long press				Latch mode		OFF  BLINK RED			
* very long press			Toggle V2		ON   GREEN/RED			
* very long press			Toggle V2		OFF  BLINK GREEN/RED 
* very very long press	Pattern Mode 	ON   GREEN/RED		
* very very long press	Pattern Mode 	OFF  BLINK GREEN/RED

Double press handling:
* short press				Euclid pattern 	ON   GREEN			(both channels)
* short press				Euclid pattern	OFF  BLINK GREEN	(both channels) 
* long press				Euclid pattern 	ON   RED			(both channels*)
* long press				Euclid pattern	OFF  BLINK RED		(both channels*) 
* very long press			Reset		 	HOLD BLINK RED		(both channels) blinks alwayse since all is off 

(*)When pressing both buttons at same time, the first which gets release is the linked channel. The button wich gets released last defines the master channel.


Limitations/Notes:
__________________
A decision was made to implement only 16 step patterns. Deriving new grooves with toggle and latch come more handy as 32 step sequences.
As I use the original hardware and it misses an extra knob to control the pattern position, the firmware tries to force always first beat.
Switching link mode on/off only happens on first beat.
Internal clock and reset detection are still active in random mode. Change from pattern-mode to random-mode and back keeps the pattern tracking in sync.
Reset detection was done by a fixed given time no input change ( has pros and cons ), with the advantage of no repatching the hardware.

Have fun 
Widy
