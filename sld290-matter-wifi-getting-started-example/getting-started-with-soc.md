# Getting Started with SoC Mode

This guide describes how to get started developing an application for the SiWx91x in System-on-chip (SoC) mode, where both the application and the networking stack run on the SiWx917 chipset.

## Check Prerequisites

To run Matter over Wi-Fi, check for the following prerequisites:

### Hardware Requirements

The following hardware devices are required for executing Matter over Wi-Fi:

- Silicon Labs Wireless starter/development kit (WSTK)
- SiWx917 SoC development kit
- Wi-Fi Dev Kit
  - SiWx917
    - SoC mode:
      - BRD4388A (B0 2.0 common flash)
             SiWx917
- Windows/Linux/MacOS computer with a USB port
- USB cable for connecting WSTK Board to Computer
- Raspberry Pi with a >32 GB SD Card
- Access Point with Internet Access

### Software Requirements

Below are the software tools, packages, and images required for executing Matter over Wi-Fi:

### Software Tools Requirements

- Simplicity Commander for flashing firmware/binary
- Tera Term
- Simplicity Studio
- PuTTY for controlling EFR32 hardware using chip-tool controller
- JLink RTT for logging only

### Software Packages

- Simplicity SDK v2024.x
- WiSeConnect SDK v3.x

### Firmware Images

- Download the firmware images from [Matter Artifacts page](/matter/{build-docspace-version}/matter-prerequisites/matter-artifacts#siwx917-firmware-for-siwn917-ncp-and-siwg917-soc).

- For flashing the firmware images, refer to [Flashing Firmware Images](/matter/{build-docspace-version}/matter-wifi-run-demo/loading-firmware-for-ncp-and-soc-boards).

## Installation of the Wi-Fi Software Tools and Packages

Refer to the [Wi-Fi Software Installation page](./software-installation).

## Connect SiWx917 SoC to Computer

1. Mount the SiWx917 radio board onto the SiWx917 WSTK board.

    ![SiWx917 WSTK](images/mount-soc.png)

2. Connect your SiWx917 Wireless Starter Kit (WSTK) board to your computer using a USB cable.
3. Simplicity Studio will detect and display your radio board.

## Troubleshooting a Board Detection Failure

If Simplicity Studio does not detect the SiWx917 SoC board, try the following:

- In the Debug Adapters panel, click **Refresh** (the icon of two looping arrows).
- Press the **RESET** button on the SiWx917 SoC radio board.
- Power-cycle the SiWx917 SoC radio board by disconnecting and reconnecting the USB cable.

## Building the 917 SoC Matter Accessory Devices Using Simplicity Studio

In Simplicity Studio 5, create the Light Matter Accessory Devices (MAD):

1. [Download](https://www.silabs.com/developers/simplicity-studio) and Install Simplicity Studio 5.
2. To install the software packages for Simplicity Studio, refer to the [Software Package Installation Section](/matter/{build-docspace-version}/matter-wifi-getting-started-example/software-installation#installation-of-software-packages).

3. Switch to the Launcher view (if not already in it).

    ![SoC Launcher tab](./images/siwx917-soc-launcher-tab.png)

4. Go to **All Products** in the Launcher tab, and select one compatible board from the following list of supported SiWx917 SOC dev boards.

   - BRD4338A (Common Flash)

   ![SoC board selection](images/siwx917-soc-boardselection.png)

5. Once the board shows up in the Debug Adapters view, select it.

    ![SoC debug adapter](images/siwx917-soc-debugadapter.png)

6. Open the Example Projects and Demos tab, select the **Matter** filter, and enter *Wi-Fi* in **Filter on keywords**. Click **CREATE**.

    ![Create project](images/siwx917-soc-create-wifiprojects.png)

7. Optionally rename the project, and click **Finish**.

    ![Project wizard](images/siwx917-soc-projectwizard.png)

8. Once the project is created, right-click the project and select **Build Project** in the Project Explorer tab.

    ![Build project](images/siwx917-soc-build-wifiproject.png)

9. To flash the application, connect the compatible dev board to the PC if not yet done.
10. Once the project is compiled successfully, go to the Project Explorer view and select the binary to be flashed.

    ![binary selection](images/siwx917-soc-isp-binaryselection.png)

11. Right-click the selected *_isp.bin* binary and click **Flash to Device**.

    ![Flash to device](images/siwx917-soc-flashtodevice.png)

12. The Flash programmer window opens. Click **Program** to start flashing.

    ![Flash program window](images/siwx917-soc-flashprogram.png)

    **Note:** Output of the SiWX917 SoC application will be displayed on the J-Link RTT Viewer.

13. In order to debug your Matter application, right-click the selected **Matter Project** and click **Debug As**.

    ![Debug](images/siwx917-socdebug.png)
