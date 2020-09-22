## Contents
| File | Description |
|------|-------------|
| _Original_: `boot.img` | SM-J320AZ stock boot image. Extracted into `boot_extracted_ramdisk` and `boot_extracted_kernel` |
| _Original_: `recovery.img` |  |
| _Original_: `system.img` | Becomes the system partition. Sparse image format. Contains all the priv-apps and system apps. Older versions of android that don't have a `vendor` partition will put their firmware in a folder in |
| `boot_extracted_ramdisk` | Boot ramdisk contents |
| ` boot_extracted_kernel` | Boot kernel contents |
| `_system.ext4` | Ext4 mountable partition created from `system.img` |

### boot.img
We used imjtool to extract the kernel and the ramdisk as they are contained in the boot image.
```
AP_J320AZTUU1APC4_CL7342465_QB8837709_REV00_user_low_ship $ imjtool boot.img
Boot image detected
Part		Size		Pages	Addr
Kernel:		5445032		2659	0x10008000
Ramdisk:	2733517		1335	0x11000000
Secondary:	0		0	0x10f00000
Tags:       0x10000100
Flash Page Size: 2048 bytes
DT Size: 362496 bytes
Found Samsung DTBH @0x7cd800 with 4 trees
	Tree@0x7ce000 (0x16000 bytes): Chip:0xd93 Platform:0x50a6 subtype:0x217584da hw_rev:0x0-0x0
	Tree@0x7e4000 (0x16000 bytes): Chip:0xd93 Platform:0x50a6 subtype:0x217584da hw_rev:0x1-0x1
	Tree@0x7fa000 (0x16000 bytes): Chip:0xd93 Platform:0x50a6 subtype:0x217584da hw_rev:0x2-0x3
	Tree@0x810000 (0x16000 bytes): Chip:0xd93 Platform:0x50a6 subtype:0x217584da hw_rev:0x4-0xff
Warning: DT ends 0x826000, but filesize is 0x826120 - looking further
Found SEANDROIDENFORCE@0x826000
ID: 50479eca69cd2297a9873674cec263e0b175dc5d000
Name:    SRPOJ19E000KU
CmdLine:
```
Re-run the command with the `extract` argument to extract the kernel and ramdisk. We placed these into the folders `boot_extracted_kernel` and `boot_extracted_ramdisk`. We can examine compiled binaries from the `boot.img` RAMDISK by exploring the contents of `boot_extracted_ramdisk`.
```
$ imjtool boot.img extract
```

### recovery.img
Contains its own RAMDISK and kernel. Used by vendors for updates and recovery mode. Most rootkits start here. These can be extracted with imjtool as well (see above).

### system.img
Not to be confused with the system image contained in `boot.img`. This image is the full android file system (The image we extract from `boot.img` serves as the root file system and it's init.rc dictates the mounting of images to their select partitions, to include this image). These are often packaged in Android's _Sparse Image format_. A tool for making an ext4 mountable system image from `system.img` is available with `apt-get install android-sdk-libsparse-utils` as of September 2020.
```
AP_J320AZTUU1APC4_CL7342465_QB8837709_REV00_user_low_ship $ file system.img
system.img: Android sparse image, version: 1.0, Total of 708608 4096-byte output blocks in 3052 input chunks.
```

Running the command makes a directory after the second argument.
```
AP_J320AZTUU1APC4_CL7342465_QB8837709_REV00_user_low_ship $ simg2img system.img _system.ext4
AP_J320AZTUU1APC4_CL7342465_QB8837709_REV00_user_low_ship $ sudo mkdir /mnt/tmpsysimg
AP_J320AZTUU1APC4_CL7342465_QB8837709_REV00_user_low_ship $ sudo mount -o loop _system.ext4 /mnt/tmpsysimg/
AP_J320AZTUU1APC4_CL7342465_QB8837709_REV00_user_low_ship $ ls /mnt/tmpsysimg/
app  build.prop  container  fonts      kern_sec_info  lib64         lost+found  preloadedmdm  recovery-from-boot.p  tima_measurement_info  vendor
bin  cameradata  etc        framework  lib            lkm_sec_info  media       priv-app      saiv                  usr                    xbin
 ```
Unless you are reverse engineering android applications, there isn't anything terrible exciting in here worth exploring.
