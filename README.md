# Sea80 1648 : Z80 Homebrew computer

This project contains the following subprojects

1. Hardware Schematic and PCB design
2. Retro8 compiler - compiler for z80
3. Firmware, rom monitor, gal files, general test utilities

Notes to self:
My z80 and peripheral chips have been relabeled(sanded and repainted) by Chinese sellers. The SIO in my system is a SIO/0

##  Memory map

Memory is divided into 8K block

0000-1FFF = ROM chip U6
2000-3FFF = ROM chip U7
4000-5FFF = RAM chip U8
6000-7FFF = RAM chip U9
8000-9FFF \
A000-BFFF } RAM chip U10
C000-DFFF |
E000-FFFF /

0000-3FFF = (16k) ROM
4000-EFFF = (45k) USER RAM
F000-FFFF = (4k)  SYSTEM RAM

### System ram
F000 - F4AF = Character Screen Ram
F4B0 - FF7F = Sytem variables
FF80 - FFFF - System stack (128 bytes)

## IO memory map

Memory IO is divided into 8 blocks of 32 bytes each
0x00 - Z84-3000, Timer/Counter
0x20 - RTC27421, Realtime Clock
0x40 - Z84-4000, Serial IO
0x60 - Z84-2000, Parallel IO
0x80 - AY-8910, Sound
0xA0 - ILI9488, LCD Display,
0xC0 - CF, Compact Fash, IDE interface
0xE0 - Free

## Screen

The screen is a graphics screen and supports one mode. Characters are drawn are blitted from rom to the screen and is backed by a charachter array.
Resolution: 480x320
Text output size: 60x20 characters

## GPIO

List GPIO max milliamps
GPIO 

### Leds

### Buttons

## RS232

Standard TTL level.
Default 9600, 8N1

## PS/2 Keyboard

## Soft power

Not working. design error

## Errata

Bodge wires


