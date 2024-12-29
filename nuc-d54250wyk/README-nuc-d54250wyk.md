# Specs Intel NUC
- Core i5-4250U
- up to 16 GB SODIMM DDR3 (2x8)
- mSATA port
- also standard SATA data and power port available
  - but no holes or bay for 2.5 inch SSD installation
  - only available in larger model D54250WYKH

# Advantages
- low power consumption due to ULV notebook CPU
- small form factor

# How to disassemble
- at the bottom loosen 4 screws
- lift up the bottom plate
- remove the black pill shaped audio jack connector cover (front panel)
  - it is held in place from the inside with 3 clips
  - it is necessary for the next step, because without removal there is not enough wiggle room
- unscrew two screws keeping the motherboard in place, loacted near the pack panel
- use a prying tool at the edge of the Ethernet port to lift up the motherboard

# How to apply BIOS update
- the BIOS is currently on a very old state from 2014
- get the BIOS version from 2019
- get the SHA256 here: [BIOS Update [WYLPT10H]](https://www.intel.com/content/www/us/en/download/17536/29075/bios-update-wylpt10h.html)
  - the official intel page leads to a broken link for the BIOS update wy0054.bio
  - SHA256: 8DE4E7E68AD8DB1AFC83458ADD48AB819A34BBE8D5B1E4FB1A5A03E3AA20CE75 
- get the BIOS update here: [Intel D54250WYK NUC Kit BIOS 0054](https://drivers.softpedia.com/get/BIOS/Intel/Intel-D54250WYK-NUC-Kit-BIOS-0054.shtml)
  - download is at the bottom of the page or here: [Intel D54250WYK NUC Kit BIOS 0054 Download Links](https://drivers.softpedia.com/get/BIOS/Intel/Intel-D54250WYK-NUC-Kit-BIOS-0054.shtml#download)
  - download only the WY0054.bio file
  - **VERIFY** with sha256sum: $ sha256sum /path/to/WY0054.bio
- copy the WY0054.bio onto an empty FAT32 formatted USB stick
- restart the PC and enter BIOS Update tool with F7 and follow instructions

# Fix broken BIOS
- if the system does not boot after playing around with BIOS 
  - screen stays black
  - no display output signal
  - fan spins up for a moment, and then remains silent
  - power button is just lighting blue, no SSD activity lights blinking
- unplug from power cord
- get the complete motherboard out of the case
- remove the BIOS security jumper (located in the corner between front audio jack and SODIMM slots)
- unplug the CMOS battery (located next to the CPU heatsink)
- press and hold the naked power button for one minute, make sure to siphon all remaining energy
- plug back in display cable, keyboard and power
- start the system, a warning will appear
  - do not press 1 or 2??? (not sure yet)
- now you should be able to enter BIOS with F2 or perform a BIOS update with F7
  - enter BIOS with F2 and restore default values with F9, and save with F10 motherboard 
  - might still remain in bricked state
  - still no display output?
- try to perform a BIOS update with F7 and USB drive ready
  - trigger the .bio file
  - the system might restart and stay in a state without display output
  - after a few minutes shut it down hard (not sure if it was with holding power button or pulling the cord)
  - reboot the system, system shall show you on the display that BIOS update from 2014 to 2019 will be performed
  - after all steps are done, put the **BIOS security jumper** and **CMOS battery** back in place (not sure if those two parts can be plugged in here or better at an earlier step)
- system shall now restart again, enter BIOS (F2) and restore setttings (F9) and save (F10)

Credits:
- [BIOS Setup Auto-Entry Enabled (D54250WYK)](https://www.reddit.com/r/intelnuc/comments/tg5rwz/comment/l0wgbx2/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)

# Make it quiet
- presets in POWER
  - Intel Dynamic Power Technology "Energy Efficient Performance"
  - Processor Power Efficiency Policy "High Performance"
- settings in COOLING -> CPU Fan Header
  - Control Mode to "Auto"
  - set Minimum Duty Cycle (%) to 0
    - PRO: fan can turn off completely when no/low load
    - CON: can be very annyoing when watching YouTube (fan repeatedly spinning up for a short moment due to heat and turn off afterwards)
    - Recommendation: for simple office work without spikes in CPU usage
  - set Minimum Duty Cycle (%) between 20-30%, try it out, 25% is working fine
    - PRO: fan spins constantly at the same frequency, does not interrupt the atmosphere
    - CON: fan is always spinning at a low RPM, can still spin up during high constant CPU load
    - Recommendation: for mixed usage, office, YouTube, regular spikes in CPU usage

# How to undervolt
- -100 mV Core/Cache and -50 mV GPU --> does not boot Ubuntu, crashed after stress testing
- -90 mV Core/Cache and -50 mV GPU --> does not boot Ubuntu, crashed after stress testing
- -80 mV Core/Cache and -50 mV GPU --> crashed while watching a 1080p60 YouTube Video with hardware acceleration (whole screen froze)
- -70 mV Core/Cache and -50 mV GPU --> testing