# How to set up Libreelec with Kodi on Wyse 3040

## Prepare USB boot device
- Download the newest generic file [here](https://libreelec.tv/downloads/generic/)
- Use `gunzip` to extract the .img file and `dd` it to the USB thumbdrive

```
gunzip LibreELEC-Generic.x86_64-xxxx.img.gz
sudo dd if=/path/to/LibreELEC-Generic.x86_64-12.2.1.img of=/dev/sdX bs=4M status=progress && sync
```

## Install LibreELEC with Kodi
- Plug in the prepared thumbdrive
- Boot from USB stick, use `F12` to select it
- Follow the instructions, install finished in a few minutes

## Enable front audio port
- Adhere to these [instructions](https://www.reddit.com/r/libreELEC/comments/13u94vd/for_anyone_looking_to_install_libreelec_on_the/)
- SSH into your LibreELEC `ssh root@<IP-address>`
- Use the following command `echo "pactl load-module module-udev-detect" > autostart.sh`
- Use command to `reboot`

## Setup ARD/ZDF livestreams
- Add the "Kodinerds" repository, instructions [here in German](https://www.kodi-tipps.de/kodinerds-repository-herunterladen-installieren/)
- Select and install the `ARDundZDF` Video add-on
