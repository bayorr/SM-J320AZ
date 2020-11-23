## Scope
Find binaries for analysis. Initially look to see if any of these binaries are not stripped.

## Method
The trivial method for retrieving files was to simply rightclick and select 'mount'. The sub-images included in the *tar.md5 packages are then easily copy/paste out of the directory. Should probably look into the proper way to do this on the command line, though. Maybe I just got lucky. The files in the table below are in their respective directories.

| File | Description |
|------|-------------|
|AP_J320AZTUU1APC4_CL7342465_QB8837709_REV00_user_low_ship.tar.md5 | Contains `boot.img`, `recovery.img`, and `system.img`. See definitions in directory readme file  |
|BL_J320AZTUU1APC4_CL7342465_QB8837709_REV00_user_low_ship.tar.md5 | Contains `param.bin' and `sboot.bin`. See definitions in directory readme file |
|CP_J320AZTUU1APC4_CL7342465_QB8837709_REV00_user_low_ship.tar.md5 | Contains `modem.bin`. See definitions in directory readme file |
|CSC_AIO_J320AZAIO1APC4_CL7342465_QB8837709_REV00_user_low_ship.tar.md5 | Contains `J3XLTE_USA_AIO.pit` and `cache.img`. See definitions in directory readme file |
