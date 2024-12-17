# New Features

## New Features for v2.5.0-1.4
- Quality-tested Matter 1.4 GA solution for Thread MG24 / MG26, Wi-Fi MG24/WF200 and Wi-Fi MG24/RS9116 (non-sleepy). 
  - For Wi-Fi SiWx917 SoC and NCP platforms, this is an Alpha. Basic functionality works but there are issues with stress testing, for deatils see the Known Issues section of the [Release Notes](https://github.com/SiliconLabs/matter_extension/releases/tag/v2.5.0). If GA quality is desired, use v2.4.0 release until the v2.5.1 patch is available.
- Works with Simplicity SDK v2024.12.0 and WiSeConnect SDK v3.4.0.
- Expands Matter support for Thread. 
  - The xG26 module support is enabled for BRD4350A, BRD4351A, BRD2709A. 
  - SixG301 Alpha support is enabled for BRD1019A. 
  - GA support of the Matter Zigbee CMP (concurrent multi-protocol) Lighting example application. 
    - Some limitations exist, for details see the Known Issues section of the [Release Notes](https://github.com/SiliconLabs/matter_extension/releases/tag/v2.5.0).
- Expands Matter support for Wi-Fi SiWx917.
  - Improved power numbers for the Wi-Fi SiWx917 SoC with the Selective Listening feature.
  - Refrigerator application and Dimmer switch application support has been added for SiWx917.
  - SiWx917 SoC module board support is enabled for BRD4343A, BRD2708A, BRD2911A.
  - SiWx917 NCP board support is enabled for BRD4357A.
  - Matter SiWx917 RCP Linux Host support has been added.
  - The mbedTLS library has been upgraded from 2.x to 3.x for the SiWx917.
- DX Improvement: Added conformance data to Matter XML files and a 'Device Type Features' page in ZAP. Toggling a feature auto-updates the featureMap and aligns attributes, commands, and events to correct conformance plus shows detailed conformance warnings for them if their enabled state conflicts with conformance value.
- Miscellaneous bug fixes and improvements.

## New Features for v2.4.0-1.4

- Quality-tested Matter 1.4 GA solution for Thread MG24 / MG26, Wi-Fi 917 SoC and DevKit (BRD2605A), Wi-Fi MG24/WF200 (non-sleepy), Wi-Fi 917 NCP platforms. Beta support for Wi-Fi 917 SoC BRD4342A module and Alpha support for Wi-Fi MG24/RS9116 platforms.
- LIT-ICD Support and Quiet Reporting Support is provided.
- Sensor App is refactored to be more generic for easier usage and maintenance.
- Fan Control App support is added for SiWx917.
- Works with Simplicity SDK v2024.6.2 and WiSeConnect SDK v3.3.4.
- Miscellaneous bug fixes and improvements.

## New Features for v2.3.2-1.3

- Quality-tested Matter 1.3 GA solution for Thread MG24 / MG26, Wi-Fi SiWx917 SoC and DevKit(BRD2605A), Wi-Fi MG24/WF200, Wi-Fi SiWx917 NCP and Wi-Fi MG24/RS9116 (non-sleepy) platforms. Beta solution for Wi-Fi MG24/RS9116 (sleepy) platforms.
- Works with Simplicity SDK v2024.6.2 and WiSeConnect SDK v3.3.3
- BRD4342A PSRAM board support is enabled for all the Matter Wi-Fi applications - beta quality.
- Miscellaneous bug fixes and improvements.

## New Features for v2.3.1-1.3

- Quality-tested Matter 1.3 GA solution for Thread MG24 / MG26, Wi-Fi 917 SoC, Wi-Fi MG24/WF200, Wi-Fi 917 NCP (non-sleepy) and Wi-Fi MG24/RS9116 (non-sleepy) platforms. Beta solution for Wi-Fi 917 NCP (sleepy) and Wi-Fi MG24/RS9116 (sleepy) platforms.
- Works with Simplicity SDK v2024.6.1 and WiSeConnect SDK v3.3.1.
- WiseConnect 2 SDK is updated to v2.10.0 for RS9116.
- Improved sleepy stability and power numbers with the Wi-Fi 917 SoC.
- BRD2605A board support is enabled for the lighting, lock, and dishwasher Matter Wi-Fi applications - beta quality.
- Introduced the Air Quality Sensor example application. The app also works with SparkFun SGP40 air quality sensor - alpha quality.
- Miscellaneous bug fixes and improvements.

## New Features for v2.3.0-1.3

- Quality-tested Matter 1.3 GA solution for Thread, Wi-Fi MG24/WF200, and Wi-Fi MG24/RS9116 (non-sleepy) platforms. Beta solution for Wi-Fi SiWx917 and Wi-Fi MG24/RS9116 (sleepy) platforms.
- Works with Simplicity SDK v2024.6.0 and WiSeConnect SDK v3.3.0.
- Introduces Matter over Thread support for BRD4116A, BRD4117A, BRD4118A, and BRD2608A boards from the EFR32MG26 family.
- Introduces the Matter Zigbee CMP (concurrent multi-protocol) Lighting example application which demonstrates the usage of the Matter Stack alongside the Silicon Labs Zigbee stack.
- Adds support for Long Idle Time ICDs.
- Adds Provisioning 2.0 Support for EFR32 and SiWx917 SoC.
- Provides Multi-chip OTA functionality support (EFR32-Thread only).
- Adds support for TA based flash storage for storing factory data in SiWx917 SoC with alpha quality.
- Enables Tickless Idle Mode and sleepy stability improvements for SiWx917 SoC.
- Removes support for EFR32 Series 1 MG12 devices: BRD4161A, BRD4162A, BRD4163A, BRD4164A, BRD4170A, and BRD4166A.
- Miscellaneous bug fixes and improvements.

## New Features for v2.2.1-1.2

- Works with Gecko SDK v4.4.2 and WiSeConnect SDK v3.1.4.
- Provides [Matter Solutions](../sld248-matter-overview-guides/matter-solutions.md) functionality for all sample applications. Example-only project generation has been removed to simplify user options.
- Adds support for custom clusters in Matter Studio projects – simply add the cluster XML file through the "Extensions" menu in ZAP.
- Enables LCD and OTA support (M4 image only) for MG24+SiWx917 NCP.
- Miscellaneous bug fixes and improvements.

## New Features for v2.2.0-1.2

- GA support for Intermittently Connected Devices
- Introduction of a third LCD screen to display application information
- Introduction of the Dishwasher Demo Application
- Adds support of Matter 1.2 on all devices
- Adds Matter support on SiWx917 SoC Common flash variants - BRD4338A
- Adds LCD display support on SiWx917 SoC for all the Wi-Fi Matter Apps
- Adds support for Direct Internet Connectivity on the SiWx917 SoC & NCP
- Support for Visual Studio Code integration
- Adds support for certificate provisioning on SiWx917 SOC
- Adds support for Firmware Upgrade on SiWx917 SOC

### Self-Provisioning Mode

Silicon Labs' Matter examples now include a self-provision mode, which enables the application to be used as Generator Firmware with the provisioning script:

- e.g.:`python3 provision.py -c config/silabs.json -gf ../out/light/BRD4187C/matter-silabs-lighting-example.s37`

To enter the self-provisioning mode, factory reset the device pressing buttons BTN0 and BTN1 for six seconds. Using this method, the device application only needs to be flashed once, provisioned multiple times, and be ready for commissioning after each provisioning.

### Support for Intermittently Connected Devices (ICD)

With the official introduction of Matter Short Idle Time (SIT) ICDs, both the door-lock sample app and the light-switch sample app are configured as SIT ICDs by default (with the exception of SiWx917 SoC examples).
The default configurations can be found in their respective `sl_matter_icd_config.h` configuration files.

- Full support for ICD Short Idle Time (SIT) Devices in support of the Matter 1.2 specification
  - In this release, Silicon Labs has provided full support for Short Idle Time intermittently connected devices
  - These are ICDs (formerly called Sleepy End Devices) which must remain responsive to user input such as Door Locks and Window Coverings
- ICD Management cluster server implementation
  - Silicon Labs has provided an implementation of the ICD cluster server and the configuration of the ICD
- ICD Manager and ICD Event Manager has been implemented to manage the Idle and Active mode of the ICD
- NEW DNS advertisement Text Key SAI: indicates the SLEEPY_ACTIVE_INTERVAL (default to 4000 ms when ICD is not enabled)
- NEW Matter ICD configuration defines:
  - **CHIP_CONFIG_ICD_IDLE_MODE_INTERVAL** sets the value for the ICD IdleInterval attribute
  - **CHIP_CONFIG_ICD_ACTIVE_MODE_INTERVAL** sets the value for the ICD ActiveInterval attribute
  - **CHIP_CONFIG_ICD_ACTIVE_MODE_THRESHOLD** sets the value for the ICD ActiveThreshold attribute
  - **CHIP_CONFIG_ICD_CLIENTS_SUPPORTED_PER_FABRIC** sets the value for the ICD ClientsSupportedPerFabric attribute
    - All of these defines can be configured within `sl_matter_icd_config.h` inside the config directory (default values listed here):

```cpp
    #define SL_IDLE_MODE_INTERVAL = 600      // 10min Idle Mode Interval
    #define SL_ACTIVE_MODE_INTERVAL = 1000   // 1s Active Mode Interval
    #define SL_ACTIVE_MODE_THRESHOLD = 500   // 500ms Active Mode Threshold
    #define SL_ICD_SUPPORTED_CLIENTS_PER_FABRIC = 2  // 2 registration slots per fabric
    
    // The OpenThread polling rates used in either ICD mode
    #define SL_OT_IDLE_INTERVAL = 15000     // 15s Idle Intervals
    #define SL_OT_ACTIVE_INTERVAL = 200     // 200ms Active Intervals
```

- CHANGES:
  - Optimized the subscription reports by synchronizing all client’s subscriptions with the ICD idle mode interval. This ensures the minimal amount of wake ups possible due to subscription reports. This component is introduced as `matter_subscription_synchronization`.
  - The previous `matter_sed` components has been replaced by `matter_icd_management`. This is in line with previous sleepy end device behavior being deprecated and replaced by the ICD behavior.
  - Silicon Labs' Light Switch and Door Lock apps support the ICD implementation and have the ICD cluster enabled.
