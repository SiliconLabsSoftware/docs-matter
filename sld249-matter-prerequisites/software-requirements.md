# Matter Over Wi-Fi Development Software Requirements

This page provides information on the required softwares tools, packages and firmware for developing Silicon Labs Matter over Wi-Fi devices.

## Softwares Tools Required

Below are the generic software tools required for both NCP and SoC mode:

1. [Silicon Labs Simplicity Studio](https://www.silabs.com/developers/simplicity-studio)

   Simplicity Studio is the main IDE and development platform provided by Silicon Labs. 
2. [Ozone - The J-Link Debugger for Windows](https://www.segger.com/products/development-tools/ozone-j-link-debugger/)

   Ozone is a full-featured graphical debugger for embedded applications. With Ozone it is possible to debug any embedded application on C/C++ source and assembly level.
3. [Simplicity Commander](https://www.silabs.com/documents/public/software/SimplicityCommander-Windows.zip)

   Simplicity Commander is a utility that provides GUI and command line access to the debug features of an EFM32 device. It allows you to flash firmware, update the kit firmware, and lock, or unlock debug access.

4. [Tera Term](https://osdn.net/projects/ttssh2/releases/)

   Tera Term is the terminal emulator for Microsoft Windows that supports serial port, telnet and SSH connections.

5. SSH Client ([PuTTY](https://www.putty.org/), Terminal, or similar):

   SSH client is used to communicate with the Raspberry Pi over a secure shell.

6. [Raspberry Pi Disk Imager](https://www.raspberrypi.com/software/)

   Raspberry Pi Disk Imager is used to flash the SD Card that contains the operating system for the Raspberry Pi.

## Softwares Packages Required for EFR32 NCP Devices

1. [GeckoSDK package](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example/software-installation#installation-of-gecko-sdk-extension), which can be installed as part of the Simplicity Studio tool installation.
 
2. [WiseConnect SDK v2.x for RS9116 NCP](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example/software-installation#installation-of-wiseconnect-sdk-v2x-or-v3x-extension), which can be installed as part of the Simplicity Studio tool installation.

3. [Wiseconnect SDK v3.x for SiWx917 NCP](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example/software-installation#installation-of-wiseconnect-sdk-v2x-or-v3x-extension), which can be installed as part of the Simplicity Studio tool installation.

4. [Firmware for RS9116 NCP](./matter-artifacts.md#rs9116-firmware)

5. [Firmware for SiWx917 NCP](./matter-artifacts.md#siwx917-firmware-for-siwx917-ncp)


## Softwares Required for SiWx917 SoC devices

1. [GeckoSDK package](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example/software-installation#installation-of-gecko-sdk-extension), which can be installed as part of the Simplicity Studio tool installation.
   
2. [WiSeConnect SDK v3.x](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example/software-installation#installation-of-wiseconnect-sdk-v2x-or-v3x-extension), which can be installed as part of the Simplicity Studio tool installation.

3. [Firmware for SoC](./matter-artifacts.md#siwx917-firmware-for-siwx917-soc)