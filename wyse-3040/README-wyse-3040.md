# project-wyse
Getting started with Dell Wyse 3040 thin client as a Raspberry Pi 4 alternative

## initial ideas
- install Debian as a minimal installation
- install Arch
- run it as a disk nuking machine (4 USB Ports are available)
- run Pi-hole
- run RetroPie
- run various Distros from USB Stick (Debian with GNOME, Kali Linux with XFCE)
- try out Remote Desktop Protocol (RDP)
- try out pre-installed ThinOS

## Default BIOS Password
- Fireport


### Testing Debian 12 Bookworm
- Enable USB Boot from BIOS
- Intro sites:
  - [Installing Debian on Dell Wyse 3040](https://binarypatrick.dev/posts/linux-on-dell-wyse-3040/)
    - How to fix system not shutting down or not rebooting
    - How to fix system not booting
  - [InstallingDebianOnDellWyse 3040](https://wiki.debian.org/InstallingDebianOn/Dell/Wyse%203040)

### WiFi / Expandable Storage
- The WiFi Card Slot is an E Keyed M.2 Port.
- *However* even though conventional WiFi Cards will fit in this port, they will not work
- The Atom CPU only has one PCI-Lane, that is used by the Ethernet Controller
- The WiFi Card uses the SDIO protocol (Yes, SD as in SD-Card)
- -> For WiFi, you can buy SDIO WiFi Cards. Expandable storage may also be an option, but I did not find the correct adapter

### Philipp, Marcel and Valentin will document the dell out of these Thin clients!
