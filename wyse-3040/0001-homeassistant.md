# How to set up homeassistant on Wyse 3040

## Preparation
- Prepare a boot stick with Live ISO (e.g. Ubuntu or Linux Mint)
  - Tested with Linux Mint Cinnamon
  - Not tested but might be better on performance when using Linux Mint Xfce edition
- Download the `Latest` version `haos_generic-x86-64-xxxx.img.xz` from Releases page [here](https://github.com/home-assistant/operating-system/releases/latest)
  - Put the file on a USB device (stick or external SSD, format with FAT32 for compatibility)
  - Note: Do not modify the file, just do a plain copy

## Installation and post setup
- Follow the official instructions [here](https://www.home-assistant.io/installation/generic-x86-64/)
- Use section "Method 1: Installing HAOS via Ubuntu booting from a USB flash drive" where the `Disks` GUI utility is used
