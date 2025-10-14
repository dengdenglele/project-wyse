# How to set up Debian 13 on Wyse 3040

## Setup steps

### Download Debian and prepare installation media

- Go [here](https://www.debian.org/) and download the Debian netinst ISO
- Prepare your drive with `dd`
  
  ```
  sudo dd if=/path/to/iso/file of=/dev/device-name bs=4M status=progress oflag=sync
  ```
  
### Boot into installer

- Boot from USB device via `F12` menu at boot
- Ensure that `UEFI` mode is visible in Debian installer menu
- Select `Install`

#### Installtion without encryption

- As disc space is limited on Dell Wyse 3040, use `Manual partitioning` instead of `Guided partitioning`
- Without encryption, no separate `/boot` partition is needed, as already included in `/`
- `Manual partitioning` allows installtion without `swap partition`, skip the warning later
- Instead of `swap partition`, it is possible to use a `swap file` instead later
- As `ESP`, also known as `/boot/efi`, typically requires only ~9 MB, the `ESP` can be reduced from ~650 MB to 9 MB

| partition | guided  | manual   |
|-----------|---------|----------|
| ESP (efi) | ~650 MB | ~50 MB   |
| / (root)  | ~6.4 GB | residual |
| swap      | ~790MB  | --       |

<!-- 32MB with EFI is not allowed by installer, error message-->

### Software selection

- Uncheck GNOME, as it is way too big for Wyse 3040
- For remote usage select both `SSH server` and `standard system utilites`
- Otherwise, uncheck all checkboxes and install everything manually for even smaller installation

### Post installation

- Increase font size of TTY

```bash
sudo dpkg-reconfigure console-setup
# choose "UTF-8", "Latin1 and Latin5 - western Europe and Turkic languages", "Terminus", "16x32 (framebuffer only)"
```
