# Mainline Klipper and Katapult for Qidi Plus 4

This guide provides instructions for flashing the Qidi Plus 4 printer with Katapult bootloader and mainline Klipper firmware.

> [!WARNING]
> ## ⚠️ PROCEED AT YOUR OWN RISK ⚠️
> 
> The procedures described in this guide involve modifying your printer's firmware and hardware.
> These modifications:
> 
> - **Can permanently damage or brick your printer**
> - **Will void your manufacturer warranty**
> - **Could cause fire or safety hazards if done incorrectly**
> 
> While you can seek help from the community or in online in general, please understand that:
> - **No official support will be provided**
> - **Contributors to this guide are not responsible for any damages**
> - **You assume all risks associated with these modifications**
> 
> **Always back up your original firmware and configurations before proceeding!**

## Overview

The Qidi Plus 4 printer has two distinct MCU boards that need to be flashed:

1. **System MCU**: The main control board
2. **Toolhead MCU**: The board controlling the extruder and hotend

Each MCU requires a two-stage flashing process:
- First with Katapult (bootloader)
- Then with Klipper firmware

For detailed information on specific topics, please refer to these guides:
- [Hardware Information](hardware.md) - Details about the Qidi Plus 4 hardware
- [Klipper Information](klipper.md) - Klipper-specific configuration and usage
- [Kalico Information](kalico.md) - Kalico-specific features and setup

## Prerequisites

- SSH access to your Qidi Plus 4 printer
- Basic understanding of Linux command line
- Backups of your existing configurations
- stlink v2 programmer for toolhead
- an eMMC adapter
- an extra eMMC card (optional)

## Backup
Backup your `printer_data` directory before you proceed. The following will backup everything except your gcode files. Adjust the command to include/exclude other directories you may want to save or discard.

```
cd ~/printer_data
tar --exclude='./gcodes' -zcvf config/plus4-backup.tgz .
```

After the command completes, you can easily download it to your computer from the Fluidd interface by going to the Configuration section and downloading the `plus4-backup.tgz` file.

Another option is to use a new eMMC and store the stock eMMC in a safe place.

## Flashing the host with a new Armbian image

1. Power down your printer and remove the eMMC card from the printer motherboard. It is held down with 2 screws.
2. Download one of the following images:
   - [An older Q1 Pro image with KIAUH and Klipper preinstalled](https://github.com/frap129/armbian_qidi-q1-pro/releases).
   - [A newer image with nothing preinstalled](https://github.com/redrathnure/armbian-mkspi/releases/download/mkspi%2F1.0.2-25.2.1/Armbian-unofficial_25.2.1_Mkspi_bookworm_current_6.12.12.img.xz)

   **Please Note: Many people have had problems getting the newer version to boot. This issue is being investigated. If your version doesn't boot, please try the Q1 Pro image.**
   
3. Write the image to your eMMC card via your preferred method (Balena Etcher, dd, etc)
    **If you need wireless networking**
    1. After writing the image to your eMMC card, open your file manager and open the `armbi_boot` drive.
    2. Rename the file `armbian_first_run.txt.template` to `armbian_first_run.txt`
    3. Open the file in a text editor, and add the SSID and Password for your wifi network. Find the line for enabling wifi and change 0 to 1.
        * `FR_net_change_defaults=1`
        * `FR_net_wifi_enabled=1`
        * `FR_net_wifi_ssid='MySSID'`
        * `FR_net_wifi_key='MyWiFiKEY'`
4. Unmount the eMMC card and re-install it into your printer and power on. If everything worked, you should now be able to access your printer via SSH.
5. SSH into your printer.
* If you're using the Q1 Image, the default username/password is `mks`. You will be asked to change your password on first login.
* If you're using the clean image, the default username is `root` and the password is `1234`
6. Install system updates and other necessary software
    ```
    sudo apt update && sudo apt upgrade
    sudo apt install git -y
    ```

### Disable debug console (if using the newer image)
By default, the Plus4 uses `/dev/ttyS2` to communicate with the toolhead. The fresh armbian image you just flashed uses `/dev/ttyS2` as a
kernel debug console, so we need to disable that:
```
echo 'console=none' > sudo tee -a /boot/armbianEnv.txt

# Grant user permissions and prevent getty from taking over the port
echo 'KERNEL=="ttyS2",MODE="0660"' > /etc/udev/rules.d/99-ttyS2.rules
systemctl mask serial-getty@ttyS2.service
```
For more information on these changes, see here: https://github.com/frap129/armbian_qidi-q1-pro#disable-debug-console-uart2--or-freeup-uart1-interface

## Installing klipper/kalico, moonraker, fluidd/mainsail and friends
[!TIP]
IF YOU INSTALLED THE Q1 PRO IMAGE FROM ABOVE, YOU CAN SKIP THESE STEPS AS KLIPPER AND FRIENDS ARE ALREADY INSTALLED. CONTINUE ON TO SYSTEM MCU FLASHING. 

### Installing KIAUH
KIAUH is a helper script to install klipper/kalico, mainsail, fluidd, crowsnest, moonraker, and many other things you may need or want.
The following steps will get KIAUH installed:
```
  cd ~
  git clone https://github.com/dw-0/kiauh.git
  ./kiauh/kiauh.sh
```
You will now be entered into the KIAUH main menu where you can install the software needed. At a minium, install the following:
* Klipper (or Kalico)
* moonraker
* fluidd (or mainsail)

KIAUH should automatically install all the required modules and start the services for you.

After everything is installed, we can move your backed up configurations over to the new setup:
Copy your `printer.cfg` and `gcode_macros` to `~/printer_data/config`


## Flashing the System MCU

### 1. Flashing Katapult
Detailed instructions for flashing Katapult to the system MCU will be provided here.

### 2. Flashing Klipper
Steps for installing Klipper firmware on the system MCU after Katapult is installed.

## Flashing the Toolhead MCU

### 1. Flashing Katapult
Process for installing Katapult on the toolhead MCU.

### 2. Flashing Klipper
Instructions for flashing Klipper firmware to the toolhead MCU.

## Troubleshooting

Common issues and their solutions when flashing firmware on Qidi Plus 4.

## Resources

- [Klipper Documentation](https://www.klipper3d.org/Overview.html)
- [Katapult Documentation](https://github.com/klipper-framework/katapult)

---

*Note: This guide is a community effort and not affiliated with Qidi Technology.*
