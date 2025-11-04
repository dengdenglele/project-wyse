# How to fix certain problems with Wyse 3040

## Device stuck on Dell logot at startup

### How we got there
- Booting from Live USB stick with Linux Mint Cinnamon
- Another USB stick with a complete pre-partitioned Home Assistant OS installation
- Used `Terminal` and `dd` to copy over all partitions of Home Assistant OS installation to Wyse 3040
- `sudo dd if=/dev/sdX of=/dev/mmcblk0 bs=4M status=progress && sync`

### Issues
- There are two more small paritions on Wyse 3040 when viewing with `lsblk`, might be essential for boot process?
- Size of internal storage < size of USB stick used
  - `dd` will display a warning that some blocks cannot be written
  - Or does it write from the beginning again or affect the other two small partitions? 
- System is stuck on Dell Logo after reboot

### How to fix
- (Might be unrelated) Open up the case with prying tool and unplug the CMOS battery, wait five minutes
- Start the machine
  - Dell logo shows up and does not display any errors
  - Just wait, will get to BIOS eventually
  - Note: eventually `F2` key needs to be at least hit once (untested)
- In BIOS select `Data Wipe`
- Reboot and wait again until `Data Wipe` tool asks for interaction
- Afterwards system shall boot up normally again and show a message, that no boot device can be found
