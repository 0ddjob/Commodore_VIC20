# Commodore VIC-20 Hardware Projects
Hardware &amp; information for the VIC-20.<br>

## [MFJ-1258 Capacitance Meter](/MFJ-1258/)
By MFJ Enterprises<br>

## [HAMSOFT Cartridge](/HAMSOFT/)
By Kantronics<br>

## [VIKTRAK+ Software & AUTOTRAK Cartridge](/VIKTRAK/)
By K7NH/Neil Hill<br>

## [6560/6561 A/V Breakout Board](/VIC_6560/) - UNTESTED
The VIC's default video output is pretty bad.  I've long wanted to "go back to basics" and see how the output can be improved by, for example, wiring it up as per its original datasheet example circuit.<br>

The first step is to create this breakout board to isolate the A/V signals from the video output stage on the VIC's motherboard.<br>

![3D view of breakout board](/VIC_6560/VIC_AV_Breakout_3D.png)

I hope that it will allow me to see what signals the 6560 outputs natively, then start to build on that.<br>

BTW, yes I know there are boards out there that already do this.  I've not had much luck with the free or paid-for boards, so I want to ... TRY TO ... understand it myself.  Let's see ...

## [Internal 8KB RAM Expansion](/Internal_8KB/) - TESTED
My attempt to replace the VIC's built in 5KB of RAM (ten 2114 chips) with a single 8KB chip, with an extra 3KB RAM as a free bonus.

![3D view of RAM upgrade board](/Internal_8KB/Images/VIC-20_BLK0_RAM_Expansion.png)
![3D view of 74LS138 board](/Internal_8KB/Images/VIC-20_BLK0_RAM_Expansion_74LS138.png)

## [Internal 32KB RAM Expansion](/Internal_32KB/) - DESIGNED
Based on the working 8KB internal RAM expansion, adds also BLK1/2/3 expansion that can be switched on/off from outside the case.

![3D view of RAM upgrade board](/Internal_32KB/Images/VIC-20_Internal_32KB.png)

## [6502 to W65C02S Daughterboard](/6502-to-65C02/) - UNTESTED
Unlike the 6522 VIAs that can be directly swapped for modern CMOS 65C22s from WDC, the W65C02S can't be directly swapped - a daughterboard is required to buffer the data bus signals and also handle some other signals/pins that differ.

![3D view of 65C02S daughterboard](/6502-to-65C02/Images/6502-to-65C02S_3D.png)
