# Internal 8KB RAM Expansion
My attempt to create a simple internal RAM upgrade board for the VIC-20.

## Purpose
- Save having to source replacement 2114 chips in case RAM is faulty,
- Upgrade the internal RAM from 5KB to 8KB, filling BLK0,
- Use as a learning experience to understand how the VIC's memory works and using a GAL.

## Design
I used [grok](/Internal_8KB/grok.md) to help with designing the chip select logic for the 6264, and the implementation code for a [GAL](/Internal_8KB/blk0_exp.cupl).<br>

The daughterboard is designed to plug in to the VIC's motherboard where two of the original 2114 chips were located - expectation is that all ten 2114 chips are removed, and two replaced with an IC socket.

The board itself is quite simple, using just the 6264 RAM chip and a GAL chip for the chip select logic.<br>

Some wires need to be connected from the board to a few other places on the VIC's board to pick up required signals.<br>

There is a switch to allow the additional 3KB RAM expansion to be disabled without having to open up the VIC.  This allows the VIC to return to its original "unexpanded VIC" state in case of software issues.<br>

## Status
25-Apr-2025: Initial design done, checking-over before sending to PCBWAY for fabrication
