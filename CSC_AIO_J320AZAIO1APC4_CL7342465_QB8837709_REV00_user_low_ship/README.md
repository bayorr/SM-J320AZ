## Contents 

|File | Description |
|-----|-------------|
| `J3XLTE_USA_AIO.pit`  | Samsung file used to instruct flashing tool where to flash images |
| `cache.img ` | Cache image |

### J3XLTE_USA_AIO.pit
Use the `file` utility to see the instructions. This file should only be tampered with if you are sure what you are doing. Tampering with this is a good way to brick your device.
```
CSC_AIO_J320AZAIO1APC4_CL7342465_QB8837709_REV00_user_low_ship $ file J3XLTE_USA_AIO.pit 
J3XLTE_USA_AIO.pit: Partition Information Table for Samsung smartphone, 24 entries; 
#1 BOOTLOADER+RW (0x50) "sboot.bin"; #2 PIT (0x46) "-"; 
#3 MD5HDR (0x47) "md5.img"; 
#4 BOTA0 (0x1) "-"; 
#5 BOTA1 (0x2) "-"; 
#6 EFS (0x3) "efs.img"; 
#7 CPEFS (0x4) "cpefs.img"; 
#8 m9kefs1 (0x5) "m9kefs1.bin"; 
#9 m9kefs2 (0x6) "m9kefs2.bin"; 
#10 m9kefs3 (0x7) "m9kefs3.bin"; 
#11 PARAM (0x8) "param.bin"; 
#12 BOOT (0x9) "boot.img"; 
#13 RECOVERY (0xa) "recovery.img"; 
#14 OTA (0xb) "-"; 
#15 CDMA-RADIO (0xc) "modem_cdma.bin"; 
#16 RADIO (0xd) "modem.bin"; 
#17 TOMBSTONES (0xe) "tombstones.img"; 
#18 TDATA (0xf) "tdata.img"
```

### cache.img
This is packaged in Android's _Sparse Image format_. A tool for making an ext4 mountable system image from cache.img is available with `apt-get install android-sdk-libsparse-utils` as of September 2020.
