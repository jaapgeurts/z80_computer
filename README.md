# Sea80 1648 : Z80 Homebrew computer

This project contains the following subprojects

1. Hardware Schematic and PCB design
2. Retro8 compiler - compiler for z80
3. Firmware, rom monitor, gal files, general test utilities


System clock: 7,372,800 Hz

Notes to self:
My z80 and peripheral chips have been relabeled(sanded and repainted) by Chinese sellers. The SIO in my system is a SIO/0

# Hardware

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
F4B0 - FEFF = System variables
FF00 -      = Keyboard buffer
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

The screen is a graphics screen and supports one mode. Characters drawn are blitted from rom to the screen and is backed by a character array.
Resolution: 480x320
Text output resolution: 60x20 characters

## GPIO

There are four GPIO groups divided over three GPIO headers.
Each group is mapped to a port.

Group A & B are mapped to port A and port B of the Z84C2004
Group C & D are mapped to port A and port B of the AY-3-8910

### PSG

Since port A and port B have on-board devices connected, the direction should be programmed as indicated below:

|GPIO|PSG Port|I/O        |
|----|--------|-----------|
|PC2 | A2     | Input only|
|PC3 | A3     | Input only|
|PC4 | A4     | Input only|
|PC5 | A5     | Input only|
|PC6 | A6     | Input only|
|PC7 | A7     | Input only|
|----|--------|-----------|
|PD4 | B4     |Output only|
|PD5 | B5     |Output only|
|PD6 | B6     |Output only|
|PD7 | B7     |Output only|

Port D outputs are open collector and buffered throught a ULN2008. Sinking is limited to max 500ma for all pins together. So 500ma is shared between all outputs; i.e. two pins can sink 250ma each etc..


### Z84C2004

|GPIO   |Z84C2004 Port|I/O  |
|-------|-------------|-----|
|PA0    | A0          | I/O |
|PA1    | A1          | I/O |
|PA2    | A2          | I/O |
|PA3    | A3          | I/O |
|PA4    | A4          | I/O |
|PA5    | A5          | I/O |
|PA6    | A6          | I/O |
|PA7    | A7          | I/O |
|PARDY  | ARDY        | I/O |
|/PASTB | ASTB        | I/O |
|-------|-------------|-----|
|PB0    | B0          | I/O |
|PB1    | B1          | I/O |
|PB2    | B2          | I/O |
|PB3    | B3          | I/O |
|PB4    | B4          | I/O |
|PB5    | B5          | I/O |
|PB6    | B6          | I/O |
|PB7    | B7          | I/O |
|PBRDY  | BRDY        | I/O |
|/PBSTB | BSTB        | I/O |


Port A can source 1.6ma, Port B can source 5ma per pin.
Port A & B can both sink max per pin 15ma.

Note: This device does not have a RESET line and must be reset in software.

### Buzzer

The buzzer is connected to PSG port B0

### Leds

The three leds are active HIGH and connected to PSG port B.
Led 1 = Pin B1
Led 2 = Pin B2
Led 3 = Pin B3

### Buttons

All buttons are active LOW.

The two user buttons are connected to the PSG port A.

BTN 1 = Pin A0
BTN 2 = Pin A1

NMI is connected directly to the NMI interrupt of the CPU

RESET is connected directly connected to reset line of board

## Timer

System clock = 7,372,800 Hz
Baudrate clock on CLK/TRG0 = 3,686,400 Hz

Period = 1/ClockFreq * Prescaler * TimeConstant

Or rewritten:

Tc = (C * I) / P
where Tc = TimeConstant
      C = Clock in Hz
      I = Interval in s (largest interval is 0.008888...s or 112.5 Hz)
      P = PreScaler = 256 or 16

The minimum and maximum interval range of the timer is: ~2.17us - ~0.009s or 460,800Hz - 112.5Hz

### Timer/Counter header

## RS232


## PSG - AY-3-8910

Input frequency: 1,843,200 Hz

Standard TTL level.
Default 9600, 8N1

## PS/2 Keyboard

## POST indicators

Explain led errors
01 001
02 010
03 011
04 100
05 101
06 110
07 111

## Soft power

Not working. Design error

## Errata

Bodge wires

# Software

## Available functions
## RST vectors
## Interrupts




