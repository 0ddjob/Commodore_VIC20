# 6502-to-W65C02S Daughterboard
My attempt to create a daughterboard to allow the repalcement of the original NMOS 6502 in the Commodore VIC-20 with a modern CMOS W65C02S from WDC.

## YouTube Video
[Simple KiCad For Simple Vintage Computer Hobbyists: Part 6 (VIC-20 6502 Replacement)](https://youtu.be/deTViI5Wltk)

## Purpose
- Save having to source replacement 6502 chip in case CPU is faulty,
- Reduce power consumption & waste heat generation by using a CMOS variant,
- Use as a learning experience using KiCad.

## Design
The [W65C02S](https://www.westerndesigncenter.com/wdc/AN-002_W65C02S_Replacements.php) can't be directly used in the Commodore VIC-20 for a few reasons:
- The purpose of some pins has changed over the years,
- This includes the RDY pin which no longer has an internal pull-up resistor,
- The data bus needs a [bus transceiver](/6502-to-65C02/Doc/grok.md) (i.e. 74HCT245) to convert between TTL and CMOS level.


## Status
27-Apr-2025: Initial design done, checking-over before sending to PCBWAY for fabrication
