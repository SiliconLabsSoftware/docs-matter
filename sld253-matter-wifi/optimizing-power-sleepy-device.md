# Optimizing Power Consumption for Sleepy End Devices
This document provides information on optimizing power consumption for Sleepy End Devices.

## Minimal Power Consumption

Simply enabling Sleepy functionality does not give the application the best power consumption.
By default, several features that increase power consumption are enabled in the example applications.

To achieve the most power-efficient build, the following components need to be disabled.

- Matter Shell (`matter_shell`)
- LCD (`matter_lcd`) and Qr Code (`matter_qr_code`)

> **Note:**
> `matter_shell` is not enabled by default in project file.
>
> - Add `matter_shell` component in project file to enable the matter shell feature (for Wi-Fi non-sleepy apps)
> - Remove `matter_shell` while enabling sleepy apps


### Achieving power optimization when LCD is enabled

- For this need to use sleepy end device with LCD component(ex: matter_sed_wf200_lcd) instead of using the direct sed component(matter_sed_wifi)
The sed with LCD component enables the sleepy along with the LCD configurations

## Flow of The Matter Wi-Fi App with LCD configuration:

- On Start of App Task we are starting a timer, if there is NO activity after defaultTimeoutMs the the callback will be triggered, and the LCD will go to Sleep.

- In between if User presses BTN1 the LED1 will toggle as usual and LCD screen will be enabled. After timeoutMs  it will trigger the callback and disables the LCD.

- If the User presses the BTN0 the system will check if the device is already commissioned, if it is not commissioned the display will be enable, it will toggle the QR Code and the call back function will be triggered after QRtimeoutMs.

## Start of Commissioning :

- On start of commissioning initially the display will remain enabled and on pressing the BTN0 user will able to see the QR code to commission for a period of QRtimeoutMs.

- Once the commissioning process starts, the LCD screen will be disabled.

## After Commissioning :

- LCD display is off during in-active transmissions.
- LCD display active , if there is any BTN press or data transfer
- On pressing the BTNs it will work the same way before.
- On initiating Data Transfer, once the action is initiated the LCD display will be enabled and disabled back after specified time.
- On triggering Factory Reset the LCD will be enabled for QRtimeoutMs then it will be disabled.
- Below diagram gives end-to-end flow for optimizing power consumption
  ![Silicon Labs - design](./images/optimize-lcd-sleepy.png)

### Power Save Methods

 - Refer, [Power Save Methods](./wifi-sleepy-end-device.md#power-save-methods)

### Enabling Power Optimization using LCD Configuration

To enable power optimization using LCD Configuration, the following component need to be added in the **.slcp** project file.

- For WF200 - `matter_sed_wf200_lcd`