# Internal 8KB RAM Expansion
My attempt to create a simple internal RAM upgrade board for the VIC-20.

## Purpose
- Save having to source replacement 2114 chips in case RAM is faulty,
- Upgrade the internal RAM from 5KB to 8KB, filling BLK0,
- Use as a learning experience to understand how the VIC's memory works and using a GAL.

## YouTube Video
[Simple KiCad For Simple Vintage Computer Hobbyists: Part 5 (VIC-20 RAM Expansion)](https://youtu.be/WQpgBGNAkP0)

## Design
This is the layout of the VIC's BLK0 (first 8KB chunk of memory):
```
1KB LOW (Zero Page)
0000-03FF   0000 0000 0000 0000 A10-A12 = 0
            0000 0011 1111 1111

3KB EXPANSION CARTRIDGE
0400-07FF   0000 0100 0000 0000 !RAM1  (A10)
            0000 0111 1111 1111
0800-0BFF   0000 1000 0000 0000 !RAM2  (A11)
            0000 1011 1111 1111
0C00-0FFF   0000 1100 0000 0000 !RAM3  (A10+A11)
            0000 1111 1111 1111

4KB MAIN
1000-1FFF   0001 0000 0000 0000 A12
            0001 0011 1111 1111 
            0001 0100 0000 0000 A10+A12
            0001 0111 1111 1111
            0001 1000 0000 0000 A11+A12
            0001 1011 1111 1111
            0001 1100 0000 0000 A10+A11+A12
            0001 1111 1111 1111
```

As per the existing VIC RAM design, we only want the RAM chip select to be active for these conditions:
- VA13 = high (when low the character ROM is selected), and
- BLK0 = low

All other combinations we want RAM chip select to be inactive.

Additionally, we want to be able to disable the full 8KB and return the VIC to its original "unexpanded VIC" state to avoid possible software compatibility issues.  The original 5KB of RAM is accessed when:
- A12 = high, or
- A10, A11, A12 = low

In its unexpanded state we should ignore all other combinations of A10 to A12.

I used [grok](/Internal_8KB/grok.md) to help with designing the chip select logic for the 6264, and the implementation code for a [GAL](/Internal_8KB/GAL/blk0_exp.pld).<br>

The daughterboard is designed to plug in to the VIC's motherboard where two of the original 2114 chips were located - expectation is that all ten 2114 chips are removed, and two replaced with an IC socket.

The board itself is quite simple, using just the 6264 RAM chip and a GAL chip for the chip select logic.<br>

Some wires need to be connected from the board to a [few other places](/Internal_8KB/Images/VIC-20_internal_RAM_layout.png) on the VIC's board to pick up required signals:<br>
- VA10 from UC4 (74LS138) pin 1
- VA11 from UC4 (74LS138) pin 2
- VA12 from UC4 (74LS138) pin 3
- VA13 from UC4 (74LS138) pin 6
- BLK0 from UC4 (74LS138) pin 4
- Φ2 (Phi2) from UC3 (74S02) pin 3

## Status
25-Apr-2025: Initial design done, checking-over before sending to PCBWAY for fabrication<br>
10-May-2025: Test PCB built & being tested
