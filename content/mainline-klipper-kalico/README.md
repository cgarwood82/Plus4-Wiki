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
