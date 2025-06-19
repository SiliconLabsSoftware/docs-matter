# Getting Started with Matter over Wi-Fi

To get started with Matter over Wi-Fi, download the latest version of Simplicity Studio as described in [Software Installation](.\software-installation) and select one of the getting started guides in this section:

- **System-on-chip (SoC) mode**: Both the application and connectivity stack runs on the SiWx91x™ chipset. Refer to [Getting Started with SoC Mode](./getting-started-with-soc).
- **Network Co-Processor (NCP) mode**: The application runs on an external micro-controller unit (MCU) host and the connectivity stack runs on the Silicon Labs Wi-Fi Processor. Refer to [Getting Started with EFR32 in NCP Mode](./getting-started-efx32-ncp).
- **Linux Host with Radio Co-Processor (RCP) mode**: The connectivity stack and application run on the Linux host, while the Wi-Fi and BLE link layers run on the Silabs RCP device. Refer to [Getting Started with Matter SiW917 RCP Linux Host](./getting-started-siwx917-rcp.md)

## Setting up the Matter over Wi-Fi Development Environment

Refer to the [Release Notes](https://github.com/SiliconLabs/matter_extension/releases/tag/v2.6.0) to know more about the latest releases from Silicon Labs.

To control the Matter Accessory Device, a controller is required which is termed as **chip-tool**. The chip-tool can be set up in two ways:

- **On the Raspberry PI**: See [Setting up chip-tool on Raspberry Pi](./build-chip-tool#build-environment-using-raspberry-pi-4).
- **On Linux**: See [Setting up chip-tool on Linux](./build-chip-tool#build-environment-for-linux).

## Running the Matter over Wi-Fi Demo

To run the Matter Demo over Wi-Fi, refer to [Running the Matter Demo over Wi-Fi](/matter/{build-docspace-version}/matter-wifi-run-demo).
