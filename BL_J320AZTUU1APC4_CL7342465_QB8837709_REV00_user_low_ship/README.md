## Contents

| File | Descritpion |
|------|-------------|
| sboot.bin | Bootloader image |
| param.bin | Companion posix archive for sboot.bin |
| adv-env | Not sure what this is |

## TODO
1. Get `sboot.bin` to decompile in ghidra properly

### sboot.bin
This is the bootloader. Bootloader should have minimal functionality, but should include a USB and UART stack for download modes and flashing. This image should finds `boot.img` and parses the RAMDISK and Kernel in those images before handing execution to the entry point in `boot.img`s RAMDISK. See 

### param.bin
The contents can be inspected by changing this to a `.tar` archive and extracting it. The following should extract a number of pictures and annother image file.
```
$ mv param.bin param.bin.tar
$ tar -xvf param.bin.tar
```
