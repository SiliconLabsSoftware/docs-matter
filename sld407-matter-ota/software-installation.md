# Installation of Matter Over Wi-Fi Development Software Requirements
This document provides information and procedure to install the required softwares tools and packages for Silicon Labs Matter over Wi-Fi devices development.

## Installation of Software Tools
Installation of generic software tools required for both NCP and SoC devices:

1. [Silicon Labs Simplicity Studio](https://www.silabs.com/developers/simplicity-studio)

    Simplicity Studio is the main IDE and development platform provided by Silicon Labs. 
2. [Ozone - The J-Link Debugger for Windows](https://www.segger.com/products/development-tools/ozone-j-link-debugger/)
   
   Ozone is a full-featured graphical debugger for embedded applications. With Ozone it is possible to debug any embedded application on C/C++ source and assembly level.
3. [Simplicity Commander](https://www.silabs.com/documents/public/software/SimplicityCommander-Windows.zip)
   
   Simplicity Commander is a utility that provides GUI and command line access to the debug features of an EFM32 device. It allows you to flash firmware, update the kit firmware, and lock, or unlock debug access.

4. [Tera Term](https://osdn.net/projects/ttssh2/releases/)
   
   Tera Term is the terminal emulator for Microsoft Windows, that supports serial port, telnet and SSH connections.

5. [PuTTY](https://www.putty.org/) (SSH Client ,Terminal, or similar)
    
    SSH client is used to communicate with the Raspberry Pi over a secure
    shell.

6. [Raspberry Pi Disk Imager](https://www.raspberrypi.com/software/)
    
    Raspberry Pi Disk Imager is used to flash the SD Card that contains the
    operating system for the Raspberry Pi.

## Installation of Software Packages
Below packages to be installed during the installation of studio:

### Installation of Gecko SDK Extension

If you already selected the Gecko SDK extension while installing Studio, you may skip this section.
You may install Gecko SDK by following below steps:
  - Installation Manager (recommended)
  - Manage SDKs Window

**Note:** Version numbers mentioned in the screenshot might be outdated. Install the latest packages available with the studio.

#### Install Gecko SDK v4.3.x through the Installation Manager
1. Log in to Simplicity Studio if not already done.

2. In the Simplicity Studio home page, select Install > Manage installed packages.
![Silicon Labs - design](./images/install-gecko-sdk-step-1.png)

3. Select the SDKs tab.

4. Next to the Gecko SDK version click on three dots button.
![Silicon Labs - design](./images/install-gecko-sdk-step-2.png)

5. Select change Version and select New Version from drop-down list to install and click finish.
![Silicon Labs - design](./images/install-gecko-sdk-step-3.png)

#### Install Gecko SDK through Manage SDK Window
1. Download the Gecko SDK v4.x source code from the following URL after substituting 4.x.x with the desired release version:

   https://github.com/SiliconLabs/gecko_sdk.git
   
   If you don't know the release version, go to the github releases page and select the version to download.

2. Unzip the downloaded Gecko SDK-4.x.x.zip file.

3. Launch Simplicity Studio and log in.

4. In the Debug Adapters panel, select the radio board.

5. In the General Information section, click Manage SDKs.
![Silicon Labs - design](./images/click-manage-sdks-efx-board.png)

6. The Preferences window will be opened in the SDKs section.

7. Select Add SDK.
![Silicon Labs - design](./images/Add-sdk.png)

8. In the Add SDK Extensions window, click Browse.
![Silicon Labs - design](./images/click-browse.png)

9. Locate and select the Gecko SDK sub-folder extracted in step 2 above which contains the source code.

10. Studio will detect the Gecko SDK extension.

11. Select the detected extension and click OK.
![Silicon Labs - design](./images/Add-sdk-path.png)

12. If a Verify SDK Extension popup is displayed, click Trust.
![Silicon Labs - design](./images/install-wiseconnect-3-ext-manage-sdks-trust-popup.png)

13.  The selected WiSeConnect 3 extension will be displayed.
![Silicon Labs - design](./images/selected-gsdk.png)

14.  Click Apply and Close.


### Installation of WiSeConnect SDK v2.x or v3.x Extension
If you already selected the WiSeConnect extension while installing Studio, you may skip this section.

Before installing the WiSeConnect SDK v2.x or v3.x extension, upgrade to a compatible GSDK version if not already done by following above steps.

You may install WiSeConnect SDK v2.x or v3.x through one of the following alternative paths:

  - Installation Manager (recommended)
  - Manage SDKs Window

#### Install WiSeConnect SDK v2.x or v3.x through the Installation Manager

1. Log in to Simplicity Studio if not already done.

2. In the Simplicity Studio home page, select Install > Manage installed packages.
![Silicon Labs - design](./images/install-wiseconnect-sdk-step-1.png)

3. Select the SDKs tab.

4. Next to the WiSeConnect SDK v2.x or v3.x extension, click Install.
![Silicon Labs - design](./images/install-wiseconnect-sdk-step-2.png)


#### Install WiSeConnect SDK v2.x or v3.x through the Manage SDKs Window

1. Download the WiSeConnect v3.x source code from the following URL after substituting 3.x.x with the desired release version:

   https://github.com/SiliconLabs/wiseconnect/archive/refs/tags/v3.x.x.zip
   
   If you don't know the release version, go to the github releases page and select the version to download.

2. Unzip the downloaded wiseconnect-3.x.x.zip file.

3. Launch Simplicity Studio and log in.

4. In the Debug Adapters pane, select your radio board.

5. In the General Information section, click Manage SDKs.
![Silicon Labs - design](./images/click-manage-sdks-efx-board.png)

6. The Preferences window will be opened in the SDKs section.

7. Select Gecko SDK Suite vx.x.x and click Add Extension.
![Silicon Labs - design](./images/click-add-extensions.png)

8. In the Add SDK Extensions window, click Browse.
![Silicon Labs - design](./images/click-browse.png)

9. Locate and select the WiSeConnect SDK v2.x or v3.x sub-folder extracted in step 2 above which contains the source code.

10. Studio will detect the WiSeConnect 3 SDK extension.

11. Select the detected extension and click OK.
![Silicon Labs - design](./images/install-wc3-ext-add-sdk-extensions-window.png)

12. If a Verify SDK Extension popup is displayed, click Trust.
![Silicon Labs - design](./images/install-wiseconnect-3-ext-manage-sdks-trust-popup.png)

13. The selected WiSeConnect SDK v2.x or v3.x extension will be displayed.
![Silicon Labs - design](./images/selected-sdk.png)

14. Click Apply and Close.
