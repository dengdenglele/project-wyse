# Install OpenWrt TP-LINK TL-WR710N

## Defaults
- "150Mbps Wireless N Mini Pocket Router"
- USB port, Reset hole, LAN/WAN port, LAN port
- Device version is 1.2 (EU)
- Default Access
  - Vanilla SSID: TP-LINK_4BADD8
  - [Web Interface](http://tplinklogin.net)
  - Username: admin
  - Password: admin

## Install OpenWrt
- [Official instructions](https://openwrt.org/toh/tp-link/tl-wr710n)
- Step 6 hint:
  - [Image archive](http://archive.openwrt.org/releases/17.01.6/targets/ar71xx/generic/) for lede-17.01.6-ar71xx-generic-xyz.bin
  - Download LEDE 17.01.6 squashfs-factory.bin image from [here](http://archive.openwrt.org/releases/17.01.6/targets/ar71xx/generic/lede-17.01.6-ar71xx-generic-tl-wr710n-v1-squashfs-factory.bin)
- Step 11 hint:
  - Uncheck `Keep Settings`

## OpenWrt post install steps
- Default access
  - Vanilla SSID: OpenWrt
  - [Web Interface](192.168.1.1)
  - Username: root
  - Password: <empty>
