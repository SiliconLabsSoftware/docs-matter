# **Developing the Silicon Labs Matter Platform**
Refer [Release Notes](https://github.com/SiliconLabs/matter_extension/releases/tag/v2.1.1) to know more about the latest releases from Silicon Labs

## **Setting up Wi-Fi Matter Development Environment**
This document gives information about setting up host machine for development and testing matter platform.

### Setting up Matter Accessory Devices
- Refer [Getting started with NCP devices](./getting-started-efx32-ncp) for setting up environment for NCP devices.
- Refer [Gettign staretd with SoC devices](./getting-started-with-soc) for setting up environment for SoC devices.

### Setting up of Chip-tool controller
To control the Matter Accessory Device, a controller to be setup which is referred as chip-tool.
Chip-tool can be setup in two ways:

   - **Setting up of Chip-tool controller in Raspberry PI**
     - Refer [Setting up of chip-tool in Raspberry PI](./build-pi-env) for setting up chip-tool controller in Raspberry PI.

   - **Setting up of Chip-tool controller in Linux**
     - Refer [Setting up of chip-tool in Linux](./build-chip-env) for setting up chip-tool controller in Linux.

### Exeuction of Usecase
To run the Matter Demo over Wi-Fi , refer [Running the Matter Demo over Wi-Fi](./run-matter-demo)