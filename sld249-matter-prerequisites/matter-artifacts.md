# Matter Software Artifacts

This page provides links to pre-built software image "artifacts" that can be used to set up the Matter Demo for the Thread and Wi-Fi use cases.

Images for the items listed below are available under the "Assets" section at the bottom of this page:

https://github.com/SiliconLabs/matter_extension/releases/tag/v2.5.2

## Matter Hub Raspberry Pi Image

The Matter Hub image is intended to be flashed onto an SD card for a Raspberry Pi. The Matter Hub image provides both an Open Thread Border Router and the Matter chip-tool. Note the image is ~7GB in size so depending on your internet connection this download may take some time. Start the Matter Hub Raspberry Pi image download here:

https://www.silabs.com/documents/public/software/SilabsMatterPi_2.5.0-1.4-extension.zip

## Radio Co-Processor (RCP) Images

The Radio Co-Processor firmware is used to turn an EFR into an RCP that can be used with a Raspberry Pi to allow the Raspberry Pi's Open Thread Border Router to access the Thread network. Radio Co-Processor (RCP) images are available in the Assets section of this page:

https://github.com/SiliconLabs/matter_extension/releases/download/v2.5.2/ot-rcp-binaries-2.5.2-1.4.zip

## Matter Accessory Device Images

The Matter Accessory Device Images are used to turn an EFR into a Matter device. These are pre-built binary images for the Matter Demo. Matter Accessory Device Images are located in the Assets section of this page:

https://github.com/SiliconLabs/matter_extension/releases/download/v2.5.2/matter-accessory-device-images_2.5.2-1.4.zip

## Matter Bootloader Binaries

All Silicon Labs board supporting Matter require that a bootloader binary is flashed to the device along with the application image. Bootloader binaries for all of the Matter supported devices are available here:

https://github.com/SiliconLabs/matter_extension/releases/download/v2.5.2/bootloader_binaries_matter_extension_v2.5.2-1.4.zip

## RS9116 Firmware

The RS9116 firmware (`rs9116_firmware_files_with_rev.zip`) is used to update the RS9116 which can be found in the Assets section of this page:

https://github.com/SiliconLabs/matter_extension/releases/download/v2.5.2/rs9116_firmware_files_with_rev_2.5.2-1.4.zip

**Note**:
RS9116 chip/module needs to be flashed with proper firmware as mentioned below:

- `RS916.x.x.x.x.x.rps - This firmware image is valid for RS9116 1.5 revision chip/module`
- `RS9116.x.x.x.x.x.rps - This firmware image is valid for RS9116 1.4/1.3 revision chip/module`

## SiWx917 Firmware for SiWN917 NCP and SiWG917 SOC

The SiWx917 firmware(SiWx917_firmware_files.zip) is used to update the SiWN917 NCP and SiWG917 SOC which can be found in the Assets section of this page:

https://github.com/SiliconLabs/matter_extension/releases/download/v2.5.2/SiWx917_firmware_files_2.5.2-1.4.zip

**Note**:

SiWN917 NCP board need to be flashed with proper firmware as mentioned below:

- `SiWG917-B.2.x.X.X.X.rps - This firmware image is valid for BRD8045A (B0 Expansion v2.0) board`

SiWG917 SoC boards need to be flashed with proper firmware as mentioned below:

- `SiWG917-B.2.x.X.X.X.rps - This firmware image is valid for BRD4338A(B0 common flash v2.0) board`

## Matter SiWx917 RCP Linux app and Configuration file

The SiWx917 RCP folder (siwx917_rcp_files.zip) contains the Matter Linux all-cluster-app, which can be run on a Raspberry Pi, and the wfx-sdio-overlay.dts file, a Device Tree Source file used to configure the SDIO interface on the Raspberry Pi to detect and communicate with the SiWx917 RCP.

https://github.com/SiliconLabs/matter_extension/releases/download/v2.5.2/siwx917_rcp_files.zip

## SiWx917 SoC Configuration Files For JLink RTT Logging

To check device logs on JLink RTT for the Matter Application on the SiWx917 SoC, the **JLink RTT** must be configured for the SiWx917 SoC device by following the instructions on the [JLink RTT SOC Support](/matter/{build-docspace-version}/matter-wifi-enabling-features/jlink-soc-setup) for SiWx917 SoC.

The [JLinkDevices.xml](https://github.com/SiliconLabs/matter_extension/releases/download/v2.5.2/JLinkDevices.xml.zip) and [RS9117_SF_4MB_42bsp.elf](https://github.com/SiliconLabs/matter_extension/releases/download/v2.5.2/RS9117_SF_4MB_42bsp.elf.zip) files referenced in the instructions may be found in the Assets section of this page.

**Note**:- For EFR32MG2x devices, JLink RTT Logging support is already enabled.
