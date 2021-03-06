# genesis_flash_cart_8mbit
simple genesis / md re-writable flash cart - 8 mbit (1 MByte)

![carts](https://github.com/ole00/genesis_flash_cart_8mbit/raw/master/img/carts.jpg "carts")

This is a PCB design of a simple Genesis flash cartridge based on the schematic and design
published by Raphaël Assénat here: https://www.raphnet.net/electronique/genesis_cart/genesis_cart_en.php

For schematics and tools please refer to the link above.

Gerber files ready for manfuacturing are located in the gerbers directory of this repository.

The PCB design can be opedned and edited in the free geda-pcb tool: http://pcb.geda-project.org/

The goal of this redesign was to fit the size of the cartridge within 100x100mm in order to save on costs of manufacturing. The zipped gerbers are ready to be droped-in to most of the popular PCB manufacturing sites without modifications.

PCB manufacturing parameters:
-----------------------------
- dual layer board
- dimensions: 87x95mm
- board thickness: 1.6mm
- no castellated holes
- only 1 design in the file
- rest of the parameters (color, surface finish, etc.) can be changed at will, the default
  options set by the manufacturers will work just fine

Additional info:
----------------
- This PCB was successfully tested with AT49F040-90PI flash chip, and also with SST39SF040-70PHE.
  It was not tested with slower chips (120ns and more) so they may not work properly in this board.
- Both flash chips must be installed. The top flash chip (marked by letter H on the PCB) holds the High bits
  and the bottom flash chip (marked by letter L) holds the Low bits of the ROM. 
- Through hole or SMD passives can be used for caps, resistor and the LED.
- Installation of LED and the resistor is optional. 
- Installation of 74LS90 is also optional. You have several options:
  * Single ROM: use the PCB only for single rom image (smaller than 8 mbit is fine as well). In this case install
  a jumper in J1 connector and shorten the 2 pins marked as 8M (even if you intend to use smaller ROM).
  The 74LS90 holes can stay unpopulated. J2 is not required either. 
  * Two ROMS - manual switch: use the PCB for 2 ROM images, each up to 4Mbit (but may be smaller). Switching
  between the ROMS is manual  by changing jumpers/switches. The device must be TURNED OFF.  Install a pin
  header (or small switch) on J1 to be able to switch between two 4M ROMS and single 8M ROM. Install a pin header 
  (or small switch) on J2 to be able to switch between ROM-1 and ROM-2 (works only when J1 is set to 2x4M mode).
  Ensure the top and bottom pins of the J2 header (or switch) are shortened to the adjecent pin on the PCB
  as indicated by the lines on the silk screen.
  * Two ROMS - auto switch: use the PCB for 2 ROM images, each up to 4Mbit (but may be smaller). Switching
  between the ROMS is automatic by pressing the Reset button on the console. The J1 and 74LS90 must be installed.
- To create 2x4M ROM image setup:
  * ensure both ROMs are in binary format and are exactly of 4 MBit size (pad them with zeros if any of 
  the image is smaller)
  * concatenate both images together to get a single 8Mbit image. Use 'copy /B img1.bin + img2.bin out.bin' on Win OS,
  or 'cat img1.bin img2.bin > out.bin' on Linux
  * use 'bin2hilo' tool (see Raphaël's site linked above) to split the out.bin to H and L part. Programm
  the H and L files into appropriate flash chips.
  
  
  
