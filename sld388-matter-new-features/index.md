# New Features

## New Features for v2.2.1-1.2

- Full [Matter Solutions](../sld248-matter-overview-guides/matter-solutions.md) functionality for all sample applications. Example only project generation has been deprecated.
- Adds support for custom clusters Matter Studio projects – simply add the cluster XML file through the "Extensions" menu in ZAP
- Enabled LCD and OTA support for MG24+917 NCP
- Miscellaneous bug fixes and improvements

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
