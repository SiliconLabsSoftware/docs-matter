# Running the Matter Demo over Wi-Fi

Follow the procedure below to run the Matter demo over Wi-Fi.

## Flashing the Bootloader Binary

   **Note**: Flashing the bootloader binaries is only required for NCP devices (MG24), it is not applicable to the SiWx917 SoC.

- The bootloader binary is supported on EFR32 boards only and it can be flashed using the Simplicity Commander software or Simplicity Studio.
- To Flash the Bootloader Binary for EFR32 Board, refer to the following guide: [Flashing Bootloader Binaries on EFR32 Devices](./flashing-using-commander#flashing-the-bootloader-binaries-for-efx32-board-using-simplicity-commander).

## Flashing the Connectivity Firmware

- To flash the connectivity firmware on an NCP device, refer to the following guide: [Upgrading Connectivity Firmware for NCP Devices](./loading-firmware-for-ncp-and-soc-boards#upgrading-the-connectivity-firmware-on-ncp-devices).
- To flash the connectivity firmware on a SiWx917 SoC, refer to the following guide [Upgrading Connectivity Firmware for SoC Devices](./loading-firmware-for-ncp-and-soc-boards#upgrading-the-connectivity-firmware-on-soc-devices).

## Building and Flashing the Matter Application using Simplicity Studio

- To build and flash an application for the EFR32, refer to [EFR32 Building and Flashing Application](./build-efx32-application-using-studio).
- To build and flash an application for SiWx917 SoC, refer to [SiWx917 SOC Building and Flashing Application](./build-soc-application-using-studio).

## Flashing the Matter Pre-Built Binaries Using Simplicity Commander

- To flash the application for EFR32 Board using Simplicity Commander, refer to [Flash EFR32 Binaries using Simplicity Commander](./flashing-using-commander#flashing-the-efr32-using-simplicity-commander).

   **Note**: For EFR32, you must use the **.s37** format file only.
- To flash the application for the SiWx917 SoC Board using Simplicity Commander, refer to [Flash SiWx917 SoC Matter Pre-Built Binaries](./flashing-using-commander#flashing-the-siwx917-soc-matter-pre-built-binary-using-simplicity-commander).
  
   **Note**: For SiWx917 SoC, use the **.rps** format file only.

## Setting up the Raspberry Pi

To set up the Raspberry Pi, refer to [Setting up the chip-tool on Raspberry PI](./build-pi-env).

## Next Steps

- [**Running the Demo**](./use-case-execution)
- [**Debugging the Application**](./application-debug)
