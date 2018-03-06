Release Histroy 
===============
* Erbse V01 (alternative Firmware for MI Branches) 
  - inital release 4 Match 2018
* Erbse V02 - (current in test stage) 
  - Improved reset detection (planed weekend 10 Match 2018)

Manual 
======
Erbse (Euclid Random Branched SEquences) contains braches firmware with some add-ons.
Original consists of two identical sections called Bernoulli gates with toggle and latch mode for each channel.

Toggle v2:
-----------
Original toggle was implemented as XOR from previouse outcome and current outcome. 
Toggle v2 also works when previouse outcome and current outcome are low ( will toggle to high ) 

E.g. in random mode toggle has no effect when knos are counterclockwise CCW, since the random generator alwyse generates low in out 1 per channel. If toggle v2 is active the out 1 and out 2 will alternate 50%. 

  
Pattern mode per channel:
-------------------------
Hardware-in signal triggers an internal 16 step sequencer per channel. Original Bernouille random mode gets deactivated. Knob/CV controls pattern (1-32). Some patterns work as simple clock divider, some are derived from good old Shruthi.

Control:
* Each Knob/CV swith pattern number from fixed given patterns 

Note:With latch active there could be nice nice clock singnales derived.
Also the Sruthi patterns generates some nicce grooves for some bread and butter sequences.

Euclid sequencer mode:
-----------------------
Hardware-in signal triggers internal 16 step euclid sequencer. The generated sequence is shared on both channels. Both channels could have individual clock in and get tracked indenpendend. 

Control:
* Knob/CV channel 1 controls hits (0-32).
* Knob/CV channel 2 controls length (0-32).

Note:
Because of the limited hardware there is no rotate button of the generated sequences. The algorithm tries alwyse to force first beat.
(Switching between length and rotate was not handy and was leading to an additnal mode selection which was confusing).
By linking channel together and combine toggle and latch new patterns could be derived for each channel.

Link mode:
----------
 Generated output from each channel overrides the Hardware-in signal from the other channel.
 
 Options:
 * Channel 1 is master, channel 2 is linked to channel 1.
 * Channel 2 is master, channel 1 is linked to channel 2.
 Both set as master is not possible! (due to physical limitation)
 
 Note:If both channels get linked to each other, the previouse link gets disabled.

Priority:
----------
Exclusive modes:
* Euclid pattern overrules random mode and pattern mode (knobs shared for both channels)
* Pattern mode per channel overrides random mode (per Channel)
* Random mode is automatically activeted if no pattern mode was selected.

Combined modes:
* Link mode, Toggle, Toggle v2 and Latch can be combined with all other modes. 

Leds
----
Leds indicate modes and selections:
* If a mode is actived Led lights for a sec.
* If a mode is turned off, Led blinks for a sec. 
* The led lights kind of dimmed while pressing the switch and change the color to know what mode gets selected when releasing the switch.

Led light table for Single button handling:

| Action | Mode | Led state |
| --- | --- | --- |
| short press		|		Toggle mode		ON  | GREEN		|
| short press		|		Toggle mode		OFF | BLINK GREEN		|
| long press			|	Latch mode		ON  | RED			|
| long press			|	Latch mode		OFF | BLINK RED			|
| very long press |	Toggle V2		ON  | GREEN/RED		|	
| very long press	|	Toggle V2		OFF | BLINK GREEN/RED |
| very very long press |	Pattern Mode 	ON  | GREEN/RED	(faster)	|
| very very long press	| Pattern Mode 	OFF | BLINK GREEN/RED (faster)|

Led light table for Single button handling:

| Action | Mode | Led state |
| --- | --- | --- |
| short press	 |			Euclid pattern 	ON |  GREEN			(both channels) |
| short press		|		Euclid pattern OFF | BLINK GREEN	(both channels) |
| long press			|	Link Channels 	ON  | RED (*see notes below, the order of button release define the master) |
| long press			|	Link Channels OFF |  BLINK RED (*see note below, the order of button release define the master) |
|very long press	|		Manual Reset		| 	start BLINK RED on hold (both channels) blinks alwayse since all is off |

Note:
(*)When pressing both buttons at same time, the first which gets release is the linked channel. The button wich gets released last defines the master channel. if both channels get linked to each other the last active link mode gets automaticly disabled. 

When holding a button down, the the led becomes light up a bit dimmed (flashes fast) to singal what mode gets next on releasing the button.
E.g. pessing the button, after a short time is passed ( for latch ) the led light up dimmed red and when releasing in dimed red the led light up full red if latch was selected or blink red if latch was deselected.

Reset handling
------------------
Auto detected reset vs Manual reset:
* When no signal gets detected for a given time the internal sequencer gets reseted to the first beat. 
This will also be signaled by a short flashing RED / GREEN for each channel. Would be the same as a reset signal as known from other sequencers. 

 * Pressing both buttons very long will force a *manual reset*. This only resets the configuration and modes.
It doesn't reset the internal clock and sequencer possitions. This will help reset all modes to random ( orginal behaviour )
during a jam by not losing the seuquencer tracking.

Limitations/Notes:
------------------
* A decision was made to implement only 16 step patterns. Deriving new grooves with toggle and latch come more handy as 32 step sequences.
* Internal clock and reset detection are still active in random mode. Change from pattern-mode to random-mode and back keeps the pattern tracking in sync.
* Reset detection was done by a fixed given time no input change ( has pros and cons ), with the advantage of no repatching the hardware.

Known problems:
* To short trigger could be missed.	Especial in euclid sequencer mode. Generating new sequences costs cpu and the clock in only read naive 
  in a loop, rather than implement interrupts. (Have to be fixed fix). There are no problem by driving erbse with normal clock diverders witch produce gates. I discoverd problems so far only if i drive erbse with grids, that sometimes triggers are not detected. 
* Link mode enable disable could lose tracking ( beat shifts ) when used in combination with latch mode, since latch influce edge detection. 
  
Have fun 
Widy
