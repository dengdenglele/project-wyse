# Tinkering with small devices

- Dell Wyse 3040 (`F1` retry boot, `F2` setup utility (BIOS), `F5` onboard diagnostics, `F12` Boot menu)
- HP t640
- Intel NUC NUC7I5BNB (`F2` BIOS, `F7` BIOS update, `F10` Boot menu)
- Intel NUC D54250WYB (`F2` BIOS, `F7` BIOS update, `F10` Boot menu)


# BIOS update for Dell laptops without battery
Tested with Dell Precision 5530

- Download respective `*.exe` file from Dell pages
- Copy the `*.exe` file to root of a FAT32 formatted thumbdrive
- Restart laptop into `F12` boot menu, select `BIOS Flash Update`
- Select `*.exe` file
- In options field type `/forceit`
- Start BIOS update

## Source
- [reddit: Update BIOS without battery?](https://www.reddit.com/r/Dell/comments/wvbnzd/update_bios_without_battery/)
