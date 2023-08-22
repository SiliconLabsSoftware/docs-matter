# Quick-Start Guides for Matter over Thread and Matter over Wi-Fi

## Overview

The procedures here describe how to make a simple network of a light, a switch, and a Matter hub, and to use the switch to control the light. First, set up your hardware and software as described below. Then you will follow a step by step procedure to:

- Create a Matter hub on a Raspberry Pi.
- Compile and load a light and a switch example application onto two Silicon Labs development boards to make light and switch Matter Accessory Devices (MADs).
- Create a Matter network with the MADs and the Matter hub.
- Test the light through the Matter hub.
- Bind the switch MAD to the light MAD, so that the switch can control the light.

## Initial Setup

Both the Matter over Wi-Fi and Matter over Thread demos require that you have set up a simple development environment with Simplicity Studio,
two EFR32MG24-based development boards, and a Raspberry Pi used as a Matter hub. The following requirements are common to both demos. The Thread demo also requires a radio co-processor (RCP) as part of the Matter Hub. The requirements for this are provided in the [introduction to the Thread demo](/matter/<docspace-docleaf-version>/matter-thread-getting-started).

### Hardware Requirements

- Matter hub

  - 1 Raspberry Pi 4B
  - 1x high speed, 64 GB SD card

- Matter devices

  - 2 EFR32xG24 kits from these recommended parts:

    - [EFR32xG24-PK6009A EFR32xG24 Pro Kit (+10 dBm)](https://www.silabs.com/development-tools/wireless/efr32xg24-pro-kit-10-dbm?tab=overview) [BRD4186C]
    - [EFR32xG24-PK6009A EFR32xG24 Pro Kit (+20 dBm)](https://www.silabs.com/development-tools/wireless/efr32xg24-pro-kit-20-dbm) [BRD4187C]

- (Wi-Fi only) Dual-Band Access Point

### Software Requirements

**Simplicity Studio 5**: Download and install Simplicity Studio 5 for your operating system from the [silabs.com Simplicity Studio page](https://www.silabs.com/developers/simplicity-studio). While the installation process is easy to follow, instructions are provided in the Simplicity Studio v5 [Getting Started section](https://docs.silabs.com/simplicity-studio-5-users-guide/latest/ss-5-users-guide-getting-started/install-ss-5-and-software). 

**Silicon Labs Matter GSDK Extension**: Once Simplicity Studio 5 is installed you will be prompted to install the Gecko SDK Suite (GSDK). Here you should also install the Matter Enablement Package by making sure the extension is checked, as shown.

![Installing the Matter Extension](./resources/install-package-advanced-device.png)

**Matter Hub Raspberry Pi Image**: A copy of the pre-built image from the Silicon Labs web services can be downloaded in this [zipfile](https://www.silabs.com/documents/public/software/SilabsMatterPi_2.0.0-1.1.zip). **Note** this is a large file and will take some time to download. 

>**Note:** The Matter hub for Matter over Thread requires an additional device, a radio co-processor. See [the introduction to the Matter over Thread demo](/matter/<docspace-docleaf-version>/matter-thread-getting-started) for more information. 

**Matter Hub Bootloader Image**: The EFR32MG24 devices must be programmed with a bootloader. Obtain those here: [Silicon Labs Matter Artifacts](/matter/<docspace-docleaf-version>/matter-prerequisites/matter-artifacts). 

**SSH Client**: Managing the Matter hub often requires connecting to it remotely. An SSH client is needed to follow the step-by-step example in this document (PuTTY is used). Install software such as [PuTTY](https://www.putty.org/), Terminal or a similar application for access to the Raspberry Pi-based Matter hub. 

**SD Card-Flashing Software**: Many different applications can be used to prepare an SD card for the Raspberry Pi, such as the [Raspberry Pi Imager](https://www.raspberrypi.com/software/), [balenaEtcher](https://www.balena.io/etcher) and [Rufus](https://silabsiot.slack.com/archives/C018366PBH8/p1654113932884999). The step-by-step example in this document uses the Raspberry Pi Imager.

## Next Steps

Now that you have your environment you can create a [Matter over Thread network](/matter/<docspace-docleaf-version>/matter-thread-getting-started) or a [Matter over Wi-Fi network](/matter/<docspace-docleaf-version>/matter-wifi-getting-started). 