# Getting Started with Matter SiW917 RCP Linux Host

This guide describes how to get started developing a Matter Linux application with a Linux host device and a SiWx917 running in RCP mode. The application and connectivity stack run on the Linux host (Raspberry Pi), while the Wi-Fi and BLE link layers run on the SiWx917 RCP.

## Check Prerequisites

To run this Matter over Wi-Fi example, check for the following prerequisites:

### Hardware Requirements

The following hardware devices are required for this example:

- SiWx917 WiFi 6 and Bluetooth LE Co-processor Radio Board
  - BRD4346A
- Adapter board for co-processor
  - BRD8045B
- Raspberrypi Board with Ubuntu version 24.04 LTS (64-bit) and above

### Firmware Images

- Download the application and configuration files from [Matter Artifacts page](/matter/{build-docspace-version}/matter-prerequisites/matter-artifacts).

## Building and running the Matter Linux with RCP App

1. Get the relevant code and binaries

    ```shell
    $ git clone https://github.com/SiliconLabs/si91x-rcp-driver.git
    ```

2. Install the dependencies

    ```shell
    $ sudo apt install -fy \
          linux-headers-$(uname -r) \
          wireless-tools \
          net-tools \
          iw \
          rfkill \
          isc-dhcp-client \
          device-tree-compiler \
          bluez \
          build-essential
    ```

3. Boot Configuration Changes

    - Generate the dtbo file from the dts
      ```shell
      $ dtc -@ -I dts -O dtb -o wfx-sdio-overlay.dtbo wfx-sdio-overlay.dts
      ```
    - Copy the generated dtbo file to /boot/firmware/overlay folder
      ```shell
      $ sudo cp wfx-sdio-overlay.dtbo /boot/firmware/overlays/
      ```
    - Add the following text in the config.txt file present in /boot/firmware folder
      ```shell
      $ sudo nano /boot/firmware/config.txt
      ```

      ```shell
      #############################################
      # Following lines were added by Silabs team #
      ############################################# 
      # Disable core_freq change because it impacts SPI bus speed
      # For details see https://github.com/raspberrypi/linux/issues/2094
      # 250MHz was chosen to have a bus frequency of 41.6MHz
      core_freq=250
      core_freq_min=250
 
      # Allow EEPROM access
      dtparam=i2c_vc=on
 
      # Disable UART, Broadcom integrated Bluetooth and Wi-Fi
      dtoverlay=disable-uart
      # The below two lines to be uncommented once the RCP driver
      # is upgraded with the latest Kernel to resolve the BLE issue
      # dtoverlay=disable-bt
      # dtoverlay=disable-bt-pi5
      dtoverlay=disable-wifi
      dtoverlay=disable-wifi-pi5
 
      # Enable Silabs Wi-Fi (only one bus may be enabled at a time)
      # Notes:
      #   -SDIO frequency is limited to 25MHz to ensure compatiblity with all
      #    Raspberry Pi versions
      #   -If using a Raspberry Pi 4B with SPI, please limit frequency to 25000000
      #   -For more information, please contact Silabs support
      dtoverlay=wfx-sdio-overlay,sdio_overclock=25
      ```

    - Reboot the pi.

4. Update the startup script to bypass network credential prompts, as it will connect through the Matter network.
      ```shell
      $ cd si91x-rcp-driver/release
      $ nano start_SiWT917.sh
      ```
    Comment from line number [379 to 432 and 436, 437](https://github.com/SiliconLabs/si91x-rcp-driver/blob/master/release/start_SiWT917.sh#L379-L432,L436-L437)
 
5. Compilation steps for the RCP driver
    
    - Run the below commands in root
      ```shell
      $ sudo su
      ```
    - Go to the release directory in si91x-rcp-driver
      ```shell
      $ cd release
      $ ./start_SiWT917.sh <mode>

      For example,
      $ ./start_SiWT917.sh STA
      ```
      Note: mode to be selected STA or STA_BLE
    
      For now, STA to be used due to BLE issue which will be resolved in the upcoming 917 RCP release.
    - Now the remaining steps can be run without root privileges.

6. Check if there is a wlan0 interface is created via
    ```shell
    $ ifconfig -a
    ```

7. Running the matter app

    - Copy the firmware i.e., chip-all-cluster-app from the artifacts provided above to the raspberrypi.
    - To build the Matter project, please refer to the [BUILDING.md guide](https://github.com/project-chip/connectedhomeip/blob/master/docs/guides/BUILDING.md). For building other Linux Matter applications, follow the README of the applications, for example, [lighting-app/linux directory](https://github.com/project-chip/connectedhomeip/tree/master/examples/lighting-app/linux.).
    - Add a default ipv6 address to the wlan0 interface using the below commands
      ```shell
      $ ip -6 addr show
      $ sudo ip -6 addr add <ipv6_address>/64 dev wlan0
 
      For example,
      $ sudo ip -6 addr add fd12:3456:789a:1::1/64 dev wlan0
      ```
    - Run the matter application using the following command
      ```shell
      $ ./chip-all-cluster-app --wifi --ble-device 0
      ```
    - Now the application is running on the Raspberry Pi with the SiWx917 RCP connected. With the help of another Pi/Linux setup (Matter Hub/Controller) running chip-tool, the commissioning can be performed
      ```shell
      $ ./chip-tool pairing ble-wifi <node-id> <ssid> <psk> 20202021 3840
      $ ./chip-tool onoff on <node-id> 1
      ```

For more information about the RCP documentation, refer to the [RCP driver documentation]( https://docs.silabs.com/wifi91xrcp/2.10.1/wifi91xrcp-getting-started/).
