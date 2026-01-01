# How to update BIOS on M910q

## Preparation and tutorials
- Complicated, hint found on [reddit](https://www.reddit.com/r/homelab/comments/hjed0s/m93p_and_m910q_bios_updates/)
- Similar YouTube tutorial [video](https://www.youtube.com/watch?v=SN4OxQHP_KY)
- ?Enable CSM in BIOS temporarily? (might not be necessary!)
- Get a FreeDOS USB stick with Windows
  - Created with Rufus on Windows 10 (defaults)
  - Download the latest BIOS Version [here](https://support.lenovo.com/de/en/downloads/ds120436-flash-bios-update-thinkcentre-m910t-m910s-m910q-m910x-m710q-thinkstation-p320-tiny)
  - The .zip file at the bottom of the list is needed
  - Unzip the content of the .zip file
  - Place it into the root or an extra directory (e.g. call it update-thinkcentre) on the FreeDOS USB stick

## Update Process
- Plug in the FreeDOS USB stick and boot up M910q
  - Load FreeDOS from F12 menu
  - Choose appropriate keyboard layout
  - `DIR` lists current directory, `CD` switches directory
  - In the right directory type `AUTOEXEC.BAT` into prompt and run BIOS Update
- During BIOS Update
  - "Would you like to update the Serial Number?" -> N
  - "Would you like to update the Machine Type and Model?" -> N
- After Reboot check in BIOS `F1` if everything is alright, load defaults `F9`
 
## BIOS versions
- BIOS version current: M1AKT5AA (2025)
- BIOS version initial: M1AKT51A (very old version)
- WIFI deactivated
- Uncheck all unnecessary entries in boot sequence
