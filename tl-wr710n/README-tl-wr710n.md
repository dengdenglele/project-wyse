# Install OpenWrt TP-LINK TL-WR710N

## Defaults
- "150Mbps Wireless N Mini Pocket Router"
- USB port, Reset hole, LAN/WAN port, LAN port
- Device version is 1.2 (EU)
- Default access
  - Vanilla SSID: TP-LINK_4BADD8
  - Web Interface: `http://tplinklogin.net`
  - Username: admin
  - Password: admin

## Install OpenWrt
[Official instructions](https://openwrt.org/toh/tp-link/tl-wr710n) are expanded below with correct links

1. Switch on the TL-WR710N and wait 2 minutes.
1. Depress and hold the recessed Reset button for 5 seconds. Release the button when the LED starts flashing.
1. Connect a computer to the LAN port and point a web browser to the TPlink web UI at `192.168.0.254`.
1. Enter `admin` for both username and password.
1. Navigate to `System Tools > Firmware Upgrade`
1. Choose the LEDE 17.01.6 squashfs-**factory**.bin image file.
   1. Download `lede-17.01.6-ar71xx-generic-tl-wr710n-v1-squashfs-factory.bin` image from [here](http://archive.openwrt.org/releases/17.01.6/targets/ar71xx/generic/lede-17.01.6-ar71xx-generic-tl-wr710n-v1-squashfs-factory.bin)
   1. [Image archive](http://archive.openwrt.org/releases/17.01.6/targets/ar71xx/generic/) for `lede-17.01.6-ar71xx-generic-xxx-yyy.bin`
1. Click `Upgrade` button.
1. After about 3 minutes, point web browser to `192.168.1.1` to bring up LuCI.
   1. What is LuCI: [Documentation](https://openwrt.github.io/luci/)
1. Log in. No password required.
1. Navigate to `System > Backup /Flash firmware` menu.
1. Under `Flash new image` section, select the OpenWrt squashfs-**sysupgrade**.bin image file (Do NOT use the squashfs-factory.bin file). Uncheck `Keep Settings`, and proceed to upgrade to OpenWRT 18 or later.
   1. Download image `openwrt-22.03.7-ath79-generic-tplink_tl-wr710n-v1-squashfs-sysupgrade.bin` from [here](https://downloads.openwrt.org/releases/22.03.7/targets/ath79/generic/openwrt-22.03.7-ath79-generic-tplink_tl-wr710n-v1-squashfs-sysupgrade.bin)

## OpenWrt post install steps
- Default access
  - Vanilla SSID: OpenWrt
  - Host IP (LAN): `192.168.1.1`
  - Username: root
  - Password: \<empty\>
- Note: Router password == Root password
- Root password max length: 100 characters
- When rooot password characters is 101 <=length
  - Login in GUI works
  - Login via `ssh root@<IP-Address>` **fails**
- Disable root login with password via ssh!
- Use public key instead
