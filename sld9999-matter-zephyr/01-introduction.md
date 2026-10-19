# Introduction

Matter applications can run on Silicon Labs hardware with the Zephyr RTOS. This guide uses the Simplicity SDK for Zephyr and the Silicon Labs Matter SDK.

Development uses West, CMake, Kconfig, and devicetree rather than the SLC project workflow. The Zephyr implementation also uses Zephyr storage services, such as NVS, instead of Silicon Labs NVM3.

Start with [Set Up the Zephyr Workspace](02-setup-zephyr.md), then build the [All-Devices Application](03-all-devices-app.md).

## Supported Hardware

The following board targets have configurations in the Silicon Labs All-Devices application. Use the exact target name with `west build -b`.

### SiWx917

SiWx917 provides Matter over Wi-Fi. Install the matching network processor (NWP) firmware as described in the [Simplicity SDK for Zephyr Getting Started Guide](https://docs.silabs.com/zephyr/latest/zephyr-getting-started/getting-started-guide).

| Board Target | Radio Board |
| --- | --- |
| `siwx917_rb4338a` | BRD4338A |
| `siwx917_rb4342a` | BRD4342A |

### EFR32xG24 and MGM240

These boards provide Matter over Thread. Except for `xg24_ek2703a`, the application uses external MX25 flash for the secondary OTA image slot.

| Board Target | Board | Notes |
| --- | --- | --- |
| `xg24_dk2601b` | BRD2601B | External OTA image slot. |
| `xg24_ek2703a` | BRD2703A | No external flash. The example configuration does not support OTA or MCUboot; build without `--sysbuild`. |
| `xg24_rb4186c` | BRD4186C | External OTA image slot. |
| `xg24_rb4187c` | BRD4187C | External OTA image slot. |
| `xg24_rb4188a` | BRD4188A | External OTA image slot. |
| `xgm240_rb4316a` | BRD4316A | External OTA image slot. |
| `xgm240_rb4317a` | BRD4317A | External OTA image slot. |
| `xgm240_rb4318a` | BRD4318A | External OTA image slot. |

### EFR32xG26 and MGM260

These boards provide Matter over Thread. The application stores both image slots in internal flash.

| Board Target | Board |
| --- | --- |
| `mgm260p_ek2713a` | BRD2713A |
| `mgm260p_rb4350a` | BRD4350A |
| `mgm260p_rb4351a` | BRD4351A |
| `xg26_dk2608a` | BRD2608A |
| `xg26_ek2709a` | BRD2709A |
| `xg26_rb4118a` | BRD4118A |
| `xg26_rb4120a` | BRD4120A |
| `xg26_rb4121a` | BRD4121A |