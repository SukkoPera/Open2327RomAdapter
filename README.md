# Open2327RomAdapter
Open2327RomAdapter is an Open Hardware adapter PCB that allows the use of a 27xxx EPROM in place of a 2364 PROM. This is mainly useful for replacing the KERNAL and other ROMs in Commodore 64 home computers and 1541 drives.

![Board](https://raw.githubusercontent.com/SukkoPera/Open2327RomAdapter/master/doc/render-top.png)

### Summary
The KERNAL ROM in a Commodore 64 is a 2364 model (8 KB), which comes in a 24-pin package. In some cases it is necessary to replace it, but 24-pin EEPROMs are not easily available. Besides, in some cases you want to have multiple KERNAL ROMs that you can select with a switch (think about [JiffyDOS](http://www.go4retro.com/products/jiffydos/)).

Open2327RomAdapter comes as an adapter PCB that sits inbetween the original socket and the new chip and solves both those problems. It also features solder pads where switched can be wired to allow the selection of a particular ROM.

### Installation
Open2327RomAdapter has been designed with a Winbond W27C512 (or W27E512, I don't understand what differences they have) EEPROM in mind. This is a 64 KB chip (thus it can hold up to 8 ROM images, more than enough for most needs), which is widely available, cheap and electrically erasable, which avoids the need for a clunky UV-eraser. **This is the only part that was thoroughly tested**.

Three 0805 SMD resistors must be soldered to the bottom side of the board, according to the following table:

| (E)EPROM | Size  | # of images |  R1  |  R2  |  R3  | Switchable pads |
|----------|-------|-------------|------|------|------|-----------------|
| 2764     | 8 KB  | 1           | 0    | 0    | 0    | -               |
| 27128    | 16 KB | 2           | 10k  | 0    | 0    | A13             |
| 27256    | 32 KB | 4           | 10k  | 10k  | 0    | A13, A14        |
| 27512*   | 64 KB | 8           | 10k  | 10k  | 10k  | A13, A14, A15   |

\* This is the only configuration that has been tested. **USE OTHER CONFIGURATIONS AT YOUR RISK!**

Note that where the recommended value is 10k, probably any value between 5k and 50k will do.

When flashing the (E)EPROM, make sure that every file is exactly 8192 bytes long and just concatenate them. You don't need to use all of the available space, but keep in mind that the unused address lines are pulled high. This means that if you use a 27512 EPROM with a single image and no switches, for instance, the image must be flashed at $E000 (i.e.: as if it was the last of 8 concatenated images).

The adapter has been carefully sized to fit both inside a C64 (tested on a 250425 board) and a 1541 drive. It can usually be installed in the original ROM socket, with no need to desolder it.

To switch between ROMs, you will need one or more switches. Every switch must connect one of the A13-A15 pads to ground when enabled. A ground pad is available on the board, but any ground spot on the C64 board can be used. Since having more than switch can be cumbersome, a rotary switch can be used as well.

**IMPORTANT: ALWAYS TURN YOUR C64 OFF BEFORE MOVING THE ROM SELECTION SWITCH(ES).**

### License
Open2327RomAdapter is Open Hardware.

### Thanks
- https://ist.uwaterloo.ca/~schepers/roms.html
- https://ist.uwaterloo.ca/~schepers/sockets.html
- http://smisioto.no-ip.org/elettronica/kicad/kicad.htm
