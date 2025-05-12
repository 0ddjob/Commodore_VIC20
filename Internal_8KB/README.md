# Internal 8KB RAM Expansion
My attempt to create a simple internal RAM upgrade board for the original VIC-20 (two-prong power, not the CR).  And, I'm not touching the single 2114 used for the colour RAM.<br>

NOTE: This is currently ... 12-May-2025 ... still a work-in-progress.  The design works, but I'm still tweaking it!

## Purpose
- Save having to source replacement 2114 chips in case RAM is faulty;
- Upgrade the internal RAM from 5KB to 8KB, filling BLK0, but make it switchable ON/OFF from outside the case;
- Reduce power consumption/waste heat generation (reduced by just over 200mA, almost 20%);
- Use as a learning experience to understand how the VIC's memory works and using a PLD;
- 100% reversible, no cutting of tracks required.

## YouTube Videos
- [Simple KiCad For Simple Vintage Computer Hobbyists: Part 5 (VIC-20 RAM Expansion)](https://youtu.be/WQpgBGNAkP0)
- [Commodore VIC-20 Internal RAM Replacement: Part 1](https://youtu.be/0KduuzFBmz8)

## Important Note
This information is provided to you completely free - use at your own risk.<br>
It is assumed that you kind-of know what you're doing - it is tricky removing chips from the VIC-20 motherboard as the top-layer tracks can lift up if there is still solder attached, so pleae be very careful.  I've been using the Japanese-made ENGINEER SS-03 solder sucker a lot lately and highly recommend it.<br>

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

The daughterboard is designed to plug in to the VIC's motherboard where two of the original 2114 chips were located - expectation is that all ten 2114 chips are removed, and two replaced with an IC socket.

The board itself is quite simple, using just the 6264 RAM chip and a PLD chip for the chip select logic.<br>

In order for the additional 3KB expansion to work we need to remove the 74LS138 RAM decoder (UC4 on my board) - its logic will be replaced by that in the PLD.<br>

Some wires need to be connected from the RAM board to where the [RAM decoder](/Internal_8KB/Images/VIC-20_internal_RAM_layout.png) was to pick up required signals:<br>
- VA10 from UC4 pin 1
- VA11 from UC4 pin 2
- VA12 from UC4 pin 3
- VA13 from UC4 pin 6
- /BLK0 from UC4 pin 4
- /RAM1 to UC4 pin 12
- /RAM2 to UC4 pin 13
- /RAM3 to UC4 pin 14

## BOM
- 6264 SRAM
- GAL16V8 (i.e. Atmel F16V8B)
- 10KΩ pull-up resistor
- 2 x 100nF decoupling capacitor
- 2 x 18-pin DIP sockets (for UD4 & UE4 RAM locations)
- 4 x 9-pin SIL two-way pin headers (to plug into DIP sockets)
- 2 x 8-way pin header (for extra required signals)
- 2-way pin header (for 3KB expansion disable/enable)
- 1 x 16-pin DIP socket (for UC4 RAM decoder location)
- 8-way Dupont connector wiring

## Status
25-Apr-2025: Initial design done, checking-over before sending to PCBWAY for fabrication<br>
10-May-2025: Test PCB built & being tested<br>
11-May-2025: IT WORKS!  But, some small revisions to the board are required ...<br>
12-May-2025: Revisions to board made, new 74LS138 daughterboard created, might still tweak the design a little<br>
