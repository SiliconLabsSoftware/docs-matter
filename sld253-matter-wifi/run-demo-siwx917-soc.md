# Running the Matter Demo over Wi-Fi for SiWx917 SoC

**Note:** 
SiWx917 SoC device support is available in the latest Simplicity Studio and Simplicity Commander(version 1v15p3)

## Flashing Images/Binaries on the SiWx917 SoC platform using Simplicity Studio

1. SiWx917 SoC boards supported:
    - `BRD4325B - Dual Flash Boards`
    - `BRD4325C & BRD4325G - common flash boards`

2. Plug the WSTK with SiWx917 SoC into the laptop.
![SiWx917 soc Device](./images/siwx917-radio-wstk.png)

3. For updating SiWx917 SoC Firmware, Refer [Firmware Update](./siwx917-soc-fwupdate.md).
   
4. To Build and flash Matter application on SiWx917 SoC using simplicity studio [Building and Flashing MATTER Application through Studio](./build-soc-application-using-studio.md)
   
5. Go to *Demo Execution - Commissioning a SiWx917 SoC Device using chip-tool for Linux* section, to run the demo with SiWx917 SoC


## Alternate flashing methods for SiWx917 SoC without Simplicity Studio

1. Flashing the Matter application using commander tool  

   - Download the Pre-built images for SiWx917 SoC Matter Application (_isp.bin/.rps file) from [Matter Artifacts page]( /matter/<docspace-docleaf-version>/matter-prerequisites/matter-artifacts).

    - Refer [Flashing MATTER Application Using Commander]( /matter/<docspace-docleaf-version>/matter-references)
  
    - Go to *Demo Execution - Commissioning a SiWx917 SoC Device using chip-tool for Linux* section, to run the demo with SiWx917 SoC

2. Flashing the Matter application using Ozone Debugger

   - Download the Pre-built images for SiWx917 SoC Matter Application (.out file) from [Matter Artifacts page]( /matter/<docspace-docleaf-version>/matter-prerequisites/matter-artifacts) or [Build Matter Application using Simplicity Studio](./build-soc-application-using-studio.md).

    - Refer [Flashing MATTER Application Using Ozone debugger](./siwx917-enablement-for-ozone.md)
  
    - Go to *Demo Execution - Commissioning a SiWx917 SoC Device using chip-tool for Linux* section, to run the demo with SiWx917 SoC
   
**Note**:
1. SiWx917 SoC Common flash boards are not supported by Ozone.
2. To enable RTT logs, download **JlinkDevices.xml** file from the [Matter Artifacts page]( /matter/<docspace-docleaf-version>/matter-prerequisites/matter-artifacts) and install in the Jlink installation path.



## Demo Execution - Commissioning a SiWx917 SoC Device using chip-tool for Linux

**Note**: Commissioning can be done using chip-tool running either on Linux or Raspberry Pi.

1. Get the SSID and PSK of the Wi-Fi network (WPA2 - Security) you are connected to.

2. Run the following:

    ```shell
    $ cd $MATTER_WORKDIR/matter
    ```

    ### Commissioning Command:

    ```shell
    $ out/standalone/chip-tool pairing ble-wifi 1122 $SSID $PSK 20202021 3840
    ```

**Note:**
The Node ID used here is `1122`. This will be used in future commands. The below given steps (3, 4, 5) are for Lighting-app, use app specific commands if you are using any other application.
 
1. To turn **on** the LED on the SiWx917:
    ```shell
    $ out/standalone/chip-tool onoff on 1122 1
    ```
 
2. To turn **off** the LED on the SiWx917:
    ```shell
    $ out/standalone/chip-tool onoff off 1122 1
    ```

3. The updated **on/off** state may be verified with the following command:
    ```shell
    $ out/standalone/chip-tool onoff read on-off 1122 1
    ```
 
If you are having difficulty getting the chip-tool to commission the device
successfully, refer to the troubleshooting information on the 
[Running the Matter Demos over Wi-Fi on EFR32 hosts page](./run-demo.md).

As the device remembers the Access Point credentials given for commissioning, if
you want to run the demo multiple times, do a [Factory Reset](./siwx917-soc-factory-reset.md).

The commissioning command mentioned above does the following:

- chip-tool scans BLE and locates the Silicon Labs device that uses the specified discriminator
- Sends the Wi-Fi SSID and Passkey
- The Silicon Labs device will join the Wi-Fi network and get an IP address.
It then starts providing mDNS records on IPv4 and IPv6
- chip-tool then locates the device over Wi-Fi and establishes operational certificates
- Future communications (tests) will then happen over Wi-Fi
 
