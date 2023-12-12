# Matter OTA Software Update with Silicon Labs Example Applications 

This page outlines the steps for a scenario that demonstrates the The Over
The Air (OTA) Software Update functionality in Matter.

The Over The Air (OTA) Software Update functionality is enabled by default for
all Silicon Labs example applications. Its inclusion in an application is
controlled by the OTA Requestor component in a Matter Studio project.

## Overview

The OTA Software Update scenario requires the following binaries:

- **OTA-A**, the running image: a regular application built with the default/older software version value. This application will be updated to the one with a higher software version. In the OTA Software Update process it acts as the OTA Requestor.
- **OTA-B**, the update image: a regular application built with a higher software version value.
- **Chip-tool**: the controller that announces the OTA-Provider's address to the application thus triggering the OTA Software Update.
- **OTA-Provider**: the server that carries the update image and from which the OTA Requestor will download the updated software.
- **Bootloader**: Silicon Labs Gecko Bootloader image that supports OTA; supports the external (SPI-flash) or the internal storage option.
  
## Setting up the OTA Environment

### Setting up chip-tool

The chip-tool binary is a part of the Silicon Labs' Matter Hub Raspberry Pi Image available as a part of the Release Artifacts page. If you are planning to run chip-tool on the Matter Hub you may skip the rest of this section.

If you have not downloaded or cloned this repository, you can run the following
commands on a Linux terminal running on a Mac, Linux, WSL or Virtual
Machine to clone the repository and run bootstrap to prepare to build the sample
application images.

1. To download the [SiliconLabs Matter codebase](https://github.com/SiliconLabs/matter.git), run the following commands.

    ```shell
     $ git clone https://github.com/SiliconLabs/matter.git
    ```

2. Bootstrapping:

    ```shell
    $ cd matter
    $ ./scripts/checkout_submodules.py --shallow --recursive --platform efr32
    $ . scripts/bootstrap.sh
    # Create a directory where binaries will be updated/compiled called `out`
    $ mkdir out
    ```

    To control the  Matter application you will have to compile and run the chip-tool on either a Linux, Mac, or Raspberry Pi. The chip-tool builds faster on the Mac and Linux machines so that is recommended, but if you have access to a Raspberry Pi that will work as well.

3. Build the chip-tool

    ```shell
    $ scripts/examples/gn_build_example.sh examples/chip-tool out/
    ```

### Setting up OTA-Provider

The chip-ota-provider-app binary for a Raspberry Pi is a part of the Artifacts package available with the Matter Extension release. If you are planning to run the OTA-Provider on a Raspberry Pi there is no need to build it. 

- To build the OTA-Provider app in Linux, run the following command in a Matter repository:

    ```shell
    $ scripts/examples/gn_build_example.sh examples/ota-provider-app/linux out chip_config_network_layer_ble=false
    ```

### Building Application Images Using Simplicity Studio

- The running image and the update image are regular Matter application images and are built using the standard procedure. The only additional configuration required is the use of a higher software version in the update image. See the following document for detailed steps: [build OTA application using studio](./05-build-ota-application-using-studio.md).

### Obtaining the Bootloader binary

- Build or download the Gecko Bootloader binary which can be obtained in one of the following ways:
  - Follow the instructions in [Creating the Bootloader for Use in Matter OTA](01-ota-bootloader.md)
  - Pre-built binaries (only valid for the external SPI-flash storage OTA update) are available on the
      [Matter Artifacts page](/matter/<docspace-docleaf-version>/matter-prerequisites/matter-artifacts).
  - Bootloader (only valid for the external SPI-flash storage OTA update) project can be built as a part of any Matter Solution in Studio 

- Using the commander tool or Simplicity Studio, upload the bootloader to the device running the
    application.

## Running the OTA Download Scenario

- Create a bootable image file (using the Lighting application image as an
    example):

    ```shell
    $ commander gbl create chip-efr32-lighting-example.gbl --app chip-efr32-lighting-example.s37
    ```

- Create the Matter OTA file from the bootable image file:

    ```shell
    $ commander ota create --type matter --input chip-efr32-lighting-example.gbl --vendorid 0xFFF1 --productid 0x8005 --swstring "2.0" --swversion 2 --digest sha256 -o chip-efr32-lighting-example.ota
    ```

- In a terminal start the Provider app and pass to it the path to the Matter
    OTA file created in the previous step:

    ```shell
    $ rm -r /tmp/chip_kvs_provider
    ```

    ```shell
    ./out/chip-ota-provider-app  --KVS /tmp/chip_kvs_provider -f chip-efr32-lighting-example.ota
    ```

- In a separate terminal run the chip-tool commands to provision the Provider:

    ```shell
    $ ./out/chip-tool pairing onnetwork 1 20202021
    ```

    ```shell
    $ ./out/chip-tool accesscontrol write acl '[{"fabricIndex": 1, "privilege": 5, "authMode": 2, "subjects": [112233], "targets": null}, {"fabricIndex": 1, "privilege": 3, "authMode": 2, "subjects": null, "targets": null}]' 1 0
    ```
- For Matter over OpenThread, bring up the OpenThread Border Router and get its operational
    dataset, for Matter over WiFi bring up the AP. 
    
- If the application device had been previously commissioned, hold Button 0
    for six seconds to factory-reset the device.

- Commission the device. 
  For Matter over OpenThread:
   
    ```shell
    $ ./out/chip-tool pairing ble-thread 2 hex:<operationalDataset> 20202021 3840
    ```
    where operationalDataset is obtained from the OpenThread Border Router.

    For Matter over WiFi:
    ```shell
      ./out/chip-tool pairing ble-wifi "node_id" "SSID" "PSK" 20202021 3840
    ```
    

- Once the commissioning process completes enter:

    ```shell
    $ ./out/chip-tool otasoftwareupdaterequestor announce-otaprovider 1 0 0 0 2 0
    ```

- The application device will connect to the Provider and start the image
    download. Once the image is downloaded the device will reboot into the
    downloaded image.

## Internal Storage Bootloader

Internal storage bootloader for Matter OTA software update is supported on MG24
boards only. In this use case both the running image and the downloadable update
image must fit on the internal flash at the same time. This in turn requires
that both images are built with a reduced feature set, such as disabled logging
and Matter shell. See [Creating the Bootloader for Use in Matter OTA](01-ota-bootloader.md)
for more details.

Installing the Lower Power Mode component in the project's Software Components tool in Studio will uninstall the following optional components and reduce the image size:

```shell
    Matter QR Code Display, 
    Matter Display, 
    Matter Shell, 
    OpenThread CLI.
```

Disabling logging in the configuration of the Matter Core Components component also helps to reduce the image size.

Using LZMA compression when building the .gbl file ( passing `--compress lzma`
parameter to the `commander gbl create` command) further reduces the downloaded
image size.

When building an internal storage bootloader the two key configuration
parameters are the Slot Start Address and Slot Size in the Bootloader Storage
Slot component. The storage slot must not overlap with the running image and the
NVM section of the flash. In other words, the slot start address must be greater
than the end of the running image address and the sum of the start address and
the slot size must be less than the address of the NVM section. The simplest way
to get the relevant addresses for the running image and NVM is by using the
Silicon Labs `Simplicity Commander` (Device Info->Main Flash->Flash Map).

The pre-built bootloader binaries are configured with slot start address of
0x080EC000 and slot size of 548864

## Managing the Software Version

In order for the Provider to successfully serve the image to a device during the
OTA Software Update process the Software Version parameter that the .ota file
was built with must be greater than the
CHIP_DEVICE_CONFIG_DEVICE_SOFTWARE_VERSION parameter set in the application's
`sl_matter_config.h` file which is a config file for the Matter Core Components component in the Matter Studio project. The Software Version parameter is set by the `-vn`
parameter passed to the `commander ota create` command. For example, if the
application's running image was built with
CHIP_DEVICE_CONFIG_DEVICE_SOFTWARE_VERSION set to 1 and if the `.ota` file is
built with `-vn 2` then the Provider will serve the update image when requested.

In order for the OTA Software Update subsystem to consider an update to be
successful and for the NotifyUpdateApplied command to be transmitted the
CHIP_DEVICE_CONFIG_DEVICE_SOFTWARE_VERSION in the updated image must exceed the
software version of the running image (continuing the above example, the image
for the update must be built with CHIP_DEVICE_CONFIG_DEVICE_SOFTWARE_VERSION set
to 2).

## Managing the Vendor and Product ID

Starting the ota-provider-app with the --otaImageList command line option allows
the user to supply a JSON file specifying the Software Version, Vendor and
Product ID that identify the image served by the Provider, see the ota-provider-app for Linux in examples directory.

Example provider configuration file:

```cpp
        { "foo": 1, // ignored by parser
          "deviceSoftwareVersionModel":
          [
           { 
            "vendorId": 65521, "productId": 32773, "softwareVersion": 1, "softwareVersionString": "1.0.0", "cDVersionNumber": 18, "softwareVersionValid": true, "minApplicableSoftwareVersion": 0, "maxApplicableSoftwareVersion": 100, "otaURL": "chip-efr32-lighting-example.ota" 
            }
          ]
        }
```

## Additional Info

Developers can find more resources on
[Silicon Labs Matter Community Page](https://community.silabs.com/s/article/connected-home-over-ip-chip-faq?language=en_US).
