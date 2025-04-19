# Mainline Klipper and Katapult for Qidi Plus 4

This guide provides instructions for flashing the Qidi Plus 4 printer with Katapult bootloader and mainline Klipper firmware.

## Overview

The Qidi Plus 4 printer has two distinct MCU boards that need to be flashed:

1. **System MCU**: The main control board
2. **Toolhead MCU**: The board controlling the extruder and hotend

Each MCU requires a two-stage flashing process:
- First with Katapult (bootloader)
- Then with Klipper firmware

## Prerequisites

- SSH access to your Qidi Plus 4 printer
- Basic understanding of Linux command line
- Backups of your existing configurations
- stlink v2 programmer for toolhead

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

## Configuration

Information about setting up and configuring Klipper for the Qidi Plus 4 after firmware installation.

## Troubleshooting

Common issues and their solutions when flashing and running Klipper on Qidi Plus 4.

## Resources

- [Klipper Documentation](https://www.klipper3d.org/Overview.html)
- [Katapult Documentation](https://github.com/klipper-framework/katapult)

---

*Note: This guide is a community effort and not affiliated with Qidi Technology.*
