# Open2327RomAdapter
Open2327RomAdapter is an Open Hardware adapter PCB that allows the use of a 27xxx EPROM in place of a 2364 PROM. This is mainly useful for replacing the KERNAL and other ROMs in VIC-20 and Commodore 64 home computers and 1541 drives.

![Board](https://raw.githubusercontent.com/SukkoPera/Open2327RomAdapter/master/doc/render-top.png)

### Summary
The KERNAL ROM in a Commodore 64 is a 2364 model (8 KB), which comes in a 24-pin package. In some cases it is necessary to replace it, but 24-pin EPROMs are not easily available. Besides, in some cases you want to have multiple KERNAL ROMs that you can select with a switch (think about [JiffyDOS](http://www.go4retro.com/products/jiffydos/)).

Open2327RomAdapter comes as an adapter PCB that sits inbetween the original socket and the new chip and solves both those problems, by allowing the use of 28-pin EPROMs, which are cheaper and much more common. It also allows the use of EPROMs bigger than the original ROM, with solder pads where switches can be wired to allow the selection of a particular ROM.

### Assembly
1. Solder the 0805 SMD resistors first. My suggested technique is as follows: put a small blob of solder on one of the pads, then grab a resistor with tweezers, reheat the solder and slide the resistor into it, keeping it flat on the board. Hold it in place with your tweezers and take the iron away. If you didn't place it straight, reheat and correct with the tweezers. Finally solder the other end. It's not that hard, you just need to practice a few times.
1. Put the pin headers into a solderless breadboard and lay the board on them, with the 0805 resistors facing down (i.e.: you should not see them). Make sure to use the two shortest hole series. Solder into place.
1. Remove the board from the solderless breadboard. Using flush cutters, cut the top two pins on the right (on the soldering side) so that they are as flush to the board as possible. Repeat with the bottom two pins. Take the socket and do a test fit, it should sit flush to the board.
1. Turn the board over and solder down the socket. Again, make sure it sits as flush as possible.
1. You are done! Try to fit the adapter in the socket on your board or solder it down, if you prefer. In both cases, you can trim the pins shorter if you need.

### Installation
Open2327RomAdapter has been designed with a Winbond W27C512 EEPROM in mind (and W27*E*512 should work just as well). This is a 64 KB chip (thus it can hold up to 8 ROM images, more than enough for most needs), which is widely available, cheap and electrically erasable, which avoids the need for a clunky UV-eraser. **This is the only part that was thoroughly tested**.

Three 0805 SMD resistors must be soldered to the bottom side of the board, according to the following table:

| (E)EPROM | Size  | # of images |  R1  |  R2  |  R3  | Switchable pads |
|----------|-------|-------------|------|------|------|-----------------|
| 2764     | 8 KB  | 1           | 0R   | 0R   | 0R   | -               |
| 27128    | 16 KB | 2           | 10k  | 0R   | 0R   | A13             |
| 27256    | 32 KB | 4           | 10k  | 10k  | 0R   | A13, A14        |
| 27512*   | 64 KB | 8           | 10k  | 10k  | 10k  | A13, A14, A15   |

\* This is the only configuration that has been tested. **USE OTHER CONFIGURATIONS AT YOUR RISK!**

Note that `0R` means that you have to install a 0-ohm resistor. Alternatively you can bridge the pads with a solder blob, but don't leave the spot empty. Where the recommended value is `10k`, instead, you have some flexibility: probably any value between 5k and 100k will do.

When flashing the (E)EPROM, make sure that every file is exactly 8192 bytes long and just concatenate them. You don't need to use all of the available space, but keep in mind that the unused address lines are pulled high. This means that if you use a 27512 EPROM with a single image and no switches, for instance, the image must be flashed at $E000 (i.e.: as if it was the last of 8 concatenated images).

The adapter has been carefully sized to fit both inside a VIC-20 (tested on the KERNAL and BASIC ROMs on an Assy #250403 board) C64 (tested on the KERNAL of an Assy #250425 board) and a 1541 drive. It can usually be installed in the original ROM socket, with no need to desolder it.

To switch between ROMs, you will need one or more switches. Every switch must connect one of the A13-A15 pads to ground when enabled. A ground pad is available on the board, but any ground spot on the C64 board can be used as well, if easier to reach. Since having more than switch can be cumbersome, a rotary switch can be used as well.

**IMPORTANT: ALWAYS TURN YOUR C64 OFF BEFORE MOVING THE ROM SELECTION SWITCH(ES).**

### License
The Open2327RomAdapter documentation, including the design itself, is copyright &copy; SukkoPera 2017-2019.

Open2327RomAdapter is Open Hardware licensed under the [CERN OHL v. 1.2](http://ohwr.org/cernohl).

You may redistribute and modify this documentation under the terms of the CERN OHL v.1.2. This documentation is distributed *as is* and WITHOUT ANY EXPRESS OR IMPLIED WARRANTIES whatsoever with respect to its functionality, operability or use, including, without limitation, any implied warranties OF MERCHANTABILITY, SATISFACTORY QUALITY, FITNESS FOR A PARTICULAR PURPOSE or infringement. We expressly disclaim any liability whatsoever for any direct, indirect, consequential, incidental or special damages, including, without limitation, lost revenues, lost profits, losses resulting from business interruption or loss of data, regardless of the form of action or legal theory under which the liability may be asserted, even if advised of the possibility or likelihood of such damages.

A copy of the full license is included in file [LICENSE.pdf](LICENSE.pdf), please refer to it for applicable conditions. In order to properly deal with its terms, please see file [LICENSE_HOWTO.pdf](LICENSE_HOWTO.pdf).

The contact points for information about manufactured Products (see section 4.2) are listed in file [PRODUCT.md](PRODUCT.md).

Any modifications made by Licensees (see section 3.4.b) shall be recorded in file [CHANGES.md](CHANGES.md).

The Documentation Location of the original project is https://github.com/SukkoPera/Open2327RomAdapter/.

### Support the Project
Since the project is open you are free to get the PCBs made by your preferred manufacturer, however in case you want to support the development, you can order them from PCBWay through this link:

[![PCB from PCBWay](https://www.pcbway.com/project/img/images/frompcbway.png)](https://www.pcbway.com/project/shareproject/Open2327RomAdapter_V2.html)

You get cheap, professionally-made and good quality PCBs, I get some credit that will help with this and [other projects](https://www.pcbway.com/project/member/shareproject/?bmbid=41100). You won't even have to worry about the various PCB options, it's all pre-configured for you!

Also, if you still have to register to that site, [you can use this link](https://www.pcbway.com/setinvite.aspx?inviteid=41100) to get some bonus initial credit (and yield me some more).

Again, if you want to use another manufacturer, feel free to, don't feel obligated :). But then you can buy me a coffee if you want:

<a href='https://ko-fi.com/L3L0U18L' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://az743702.vo.msecnd.net/cdn/kofi2.png?v=2' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>

### Get Support
If you need help or have questions, you can join [the official Telegram group](https://t.me/joinchat/HUHdWBC9J9JnYIrvTYfZmg).

### Thanks
The following links were useful during the development of this project:
- https://ist.uwaterloo.ca/~schepers/roms.html
- https://ist.uwaterloo.ca/~schepers/sockets.html
- http://smisioto.no-ip.org/elettronica/kicad/kicad.htm
