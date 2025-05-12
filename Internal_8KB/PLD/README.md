# PLD Stuff
## Info
PLD used: Atmel F18V8B<br>
Assembler used: [GALasm](https://github.com/daveho/GALasm) on macOS<br>
Programmer used: Wellon VP598 EPROM programmer

## Files
- blk0_exp.pld: The PLD design file
- blk0_exp.jed: The assembled JEDEC file used to program the PLD
- blk0_exp.chp: The pin-out of the PLD
- blk0_exp.fus: The fuse file
- blk0_exp.pin: List of pin numbers, name and type

## Logic
The logic defined in the PLD file is:
```
/RAM1 = SW * VA10 * /VA11 * /VA12 * VA13 * /BLK0
/RAM2 = SW * /VA10 * VA11 * /VA12 * VA13 * /BLK0
/RAM3 = SW * VA10 * VA11 * /VA12 * VA13 * /BLK0
/CS1 = VA13 * /BLK0 
CS2 = VA13 * /BLK0
```

The 6264 RAM chip has an active low /CS1 and active high CS2. The VA13 and /BLK0 signals are used to enable the 74LS138 RAM decoder in the VIC, so we re-use the same signals to enable our RAM.  The 6264's /OE follows the /CS1 and are tied on the 6264 itself.<br>

The RAM data bus (BD0..BD7) in the VIC is connected to the CPU data bus (CD0..CD7) via a 74LS245 transceiver. When /RAM1, /RAM2 or /RAM3 are asserted (via a 74LS133 NAND, output is high) the inputs on 74LS245 transceiver are disabled which isolates the RAM data bus from the CPU data bus.<br>

If we want the additional 3KB RAM expansion to work (when enabled via the switch) then we want to de-assert the /RAM1 to /RAM3 signals to the 74LS133 which, in turn, ensures our RAM data bus remains connected to the CPU data bus.<br>
