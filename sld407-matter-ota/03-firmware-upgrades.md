# Firmware Upgrades with Matter applications

The Over The Air (OTA) Software Update functionality provides WiFi firmware upgrades within the matter environment.

## Hardware Requirements

- To run matter ota on Silicon Labs Platform, refer [Hardware Requirements](/matter/{build-docspace-version}/matter-prerequisites/hardware-requirements).

## Software Requirements

- To run matter ota on Silicon Labs Platform, refer [Software Requirements](/matter/{build-docspace-version}/matter-prerequisites/software-requirements).

## Setting up OTA Environment

- To run OTA on Matter over Wi-Fi, Need to build two different application below:
  - **OTA-A** is a normal application with default or older software version. It acts as **ota-requestor** where it needs to update latest software version.
  - **OTA-B is** a normal application with updated software version.
  - **Chip-tool** is a controller for sending commands to ota-requestor to update the software version and receving commands from device.
  - **OTA-Provider** is the server who has the latest software version and from which ota-requestor will download the updated software.

### Setting up Chip-tool Controller

If you have not downloaded or cloned this repository, you can run the following
commands on a Linux terminal running on either Linux machine, WSL or Virtual
Machine to clone the repository and run bootstrap to prepare to build the sample
application images.

1. To download the [SiliconLabs Matter codebase](https://github.com/project-chip/connectedhomeip.git) run the following commands.

    ```shell
     $ git clone https://github.com/project-chip/connectedhomeip.git
    ```

2. Bootstrapping:

    ```shell
    $ cd matter
    $ ./scripts/checkout_submodules.py --shallow --recursive --platform efr32
    $ . scripts/bootstrap.sh
    # Create a directory where binaries will be updated/compiled called `out`
    $ mkdir out
    ```

    To control the Wi-Fi Matter Accessory Device you will have to compile and run the chip-tool on either a Linux, Mac or Raspberry Pi. The chip-tool builds faster on the Mac and Linux machines so that is recommended, but if you have access to a Raspberry Pi that will work as well.

3. Build the chip-tool

    ```shell
    $ ./scripts/examples/gn_build_example.sh examples/chip-tool out/standalone
    ```

This will build chip-tool in `out/standalone`.

### Setting up OTA-Provider

- To Build OTA-Provider app in Linux Platform, Run below command in matter repository.

```shell
    scripts/examples/gn_build_example.sh examples/ota-provider-app/linux out/debug chip_config_network_layer_ble=false
```

### Building OTA Images Using Simplicity Studio

- To create and build matter OTA using Simplicity studio, refer following link [build OTA application using studio](./05-build-ota-application-using-studio.md).

## Executing OTA Scenario

### Generating the OTA image

1. Locate Simplicity Commander Path via **Command Prompt Terminal**.
2. Create a bootable image file by running below command in commander terminal(using the Lighting application image as an
example):

    ```shell
        commander gbl create chip-efr32-lighting-example.gbl --compress lzma --app chip-efr32-lighting-example.s37
    ```

    **Note**: Using LZMA compression when building the .gbl file ( passing `--compress lzma` parameter to the `commander gbl create` command) further reduces the downloaded image size.

3. Create the Matter OTA file by running below command in **${WORKSPCAE_DIR}/matter** path:

```shell
    ./src/app/ota_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 2 -vs "2.0" -da sha256 chip-efr32-lighting-example.gbl chip-efr32-lighting-example.ota
```

**Note**: Modify **-vn** to **CHIP_DEVICE_CONFIG_DEVICE_SOFTWARE_VERSION** and **-vs** to **CHIP_DEVICE_CONFIG_DEVICE_SOFTWARE_VERSION** as per OTA-B application Building Step 10 in [Build OTA Images](./05-build-ota-application-using-studio.md).

### Running OTA Provider

- Locate **ota-provider** terminal start the Provider app passing to it the path to the Matter OTA file created in the previous step:

```shell
    rm -r /tmp/chip_*
    ./out/debug/chip-ota-provider-app -f chip-efr32-lighting-example.ota
```

### Setting up OTA-Requestor

- Before running **ota-requestor** app flash the bootloader binary images for Silicon Labs Devices.

#### Flash Bootloader Images

- Bootloader binaries will be flashed using Simplicity Commander only. It will support EFR32 NCP Boards only.
- Silicon Labs Devices will supports below Bootloader variants for EFR32 Boards.
  - Internal Storage Bootloader
  - External Storage Bootloader
- To Flash the Bootloader Binary along with the application for Silicon Labs Device, refer [Flashing Binaries](/matter/{build-docspace-version}/matter-wifi-run-demo/flashing-using-commander.md).

### Running OTA-Requestor

1. In a separate terminal, locate the chip-tool and ota-requestor and run the chip-tool commands to provision the Provider:

    ```shell
        ./out/chip-tool pairing onnetwork 1 20202021
        ./out/chip-tool accesscontrol write acl '[{"fabricIndex": 1, "privilege": 5, "authMode": 2, "subjects": [112233], "targets": null}, {"fabricIndex": 1, "privilege": 3, "authMode": 2, "subjects": null, "targets": null}]' 1 0
    ```

2. If the application device had been previously commissioned hold Button 0 for six seconds to factory-reset the device.

3. In the chip-tool terminal, commission the Device by passing below command:

    ```shell
        ./out/chip-tool pairing ble-wifi "node_id" "SSID" "PSK" 20202021 3840
    ```

    where SSID and PSK are AP username and password.

4. Once the commissioning process completes in the same terminal, run below requestor command to start downloading the image:

```shell
    ./out/chip-tool otasoftwareupdaterequestor announce-ota-provider 1 0 0 0 2 0
```

- The application device will connect to the Provider and start the image download. Once the image is downloaded the device will reboot into the downloaded image.
