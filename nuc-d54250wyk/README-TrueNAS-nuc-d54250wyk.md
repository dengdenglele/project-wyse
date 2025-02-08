# TrueNAS on Intel NUC d54250WYK

## Prerequisites

- Up to 4 HDD/SSD SATA to USB enclosures: [BENFEI External Hard Drive Enclosure](https://www.amazon.de/BENFEI-Festplattengeh%C3%A4use-Externes-Optimiert-unterst%C3%BCtzt/dp/B0C73VYQCW)
    - Note: Simple USB SATA adapters may not be recognized as different devices if they have the same serial number.
- Follow the official TrueNAS installation guide: [Installing TrueNAS SCALE](https://www.truenas.com/docs/scale/gettingstarted/install/installingscale/)
- Create a bootable USB stick with TrueNAS SCALE (Linux variant preferred over BSD):
    
    ```bash
    sudo dd if=~/Downloads/TrueNAS-SCALE-24.10.1.iso of=/dev/sda bs=4M status=progress oflag=sync
    ```
    

## Installation

1. Boot from the USB stick and run the setup.
2. Set up a password for the web UI.
3. Follow the installation steps from the TrueNAS SCALE website: [Download TrueNAS SCALE](https://www.truenas.com/download-truenas-scale/)
4. After installation, log in with your specified credentials and access the dashboard.

## Setup Pool

1. Click on `Create Pool` to open the pool creation wizard.
2. Choose a name and optional encryption for the pool.
3. Select RAID layout and disks.
4. Configure additional options if needed, or proceed to the last step and create the pool.

## Setup NFS Share

1. Navigate to the `Shares` tab and click `Add` under `UNIX (NFS) Shares`.
2. Specify the path for the NFS share and define your network (`192.168.X.0/24`).
3. Set authorized hosts and IP addresses for the devices that will connect.
4. In advanced options:
    - Set `Maproot User` to `root`.
    - Set `Maproot Group` to `wheel` for an easier permission setup.
5. Click `Add` and start the NFS service within TrueNAS.
6. On the client machines, mount the NFS share:
    
    ```bash
    sudo mount -t nfs 192.168.2.46:/mnt/poolName/ localDirectory/
    ```
    
