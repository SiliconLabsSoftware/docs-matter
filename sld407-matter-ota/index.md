# Matter OTA

The Over The Air (OTA) Software Update functionality is enabled by default for all of the EFR32 and SiWx917 example applications. Its inclusion in an application is controlled by the OTA Requestor component in a Matter Studio project.

- [**Matter OTA Bootloader**](./01-ota-bootloader.md)
- [**Matter OTA Software Update**](./02-ota-software-update.md)
- [**Matter 917 SOC OTA Software Update**](./03-ota-software-update-soc.md)
- [**Matter OTA Project in Simplicity Studio**](./04-build-ota-application-using-studio.md)

Note:The Matter specification requires every certified device to support a secure firmware upgrade mechanism (Section 11.20.4.2 of the Matter Specification, version 1.5). On Silicon Labs platforms, this requirement is satisfied by the [Gecko Bootloader Secure Firmware Upgrade](https://docs.silabs.com/mcu-bootloader/latest/bootloader-user-guide-gsdk-4/09-gecko-bootloader-security-features#secure-firmware-upgrade) feature, and all Silicon Labs Matter products must use this feature to meet Matter certification requirements.