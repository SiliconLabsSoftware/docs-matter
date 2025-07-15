# Matter OTA For SiWx917 SoC

The scope of this page describes the Matter OTA upgrade on SiWx917 SoC mode for combined image(TA+M4), application(M4) alone, and Wi-Fi(TA) alone image upgrade.

## Hardware Requirements

- To run Matter OTA on Silicon Labs Platform, refer to [Hardware Requirements](/matter/{build-docspace-version}/matter-prerequisites/hardware-requirements).

## Software Requirements

- To run Matter OTA on Silicon Labs Platform, refer to [Software Requirements](/matter/{build-docspace-version}/matter-prerequisites/software-requirements).

## Setting up OTA Environment

To run OTA on Matter over Wi-Fi, you need to build two different applications below:

- **OTA-A** is a normal application(M4) with default or older software version. It acts as **ota-requestor** where it needs to update latest software version.
- **OTA-B** is a normal application with updated software version. Here OTA-B is application(M4) image
- **Chip-tool** is a controller for sending commands to ota-requestor to update the software version and receiving commands from device.
- **OTA-Provider** is the server who has the latest software version and from which ota-requestor will download the updated software.

## High Level Steps

- Building OTA Application
- Creating Images
  - Combined Image(TA+M4) Creation
  - Matter OTA Image Creation
    - **Combined image (TA+M4)**: Updates both the application(M4) and Wi-Fi(TA) together.
    - **M4-only**: Updates only the application(M4).
    - **TA-only**: Updates only the Wi-Fi(TA).
- Running OTA-Provider
- Running OTA-Requestor

### Building OTA Application

To create and build Matter OTA using Simplicity Studio For SiWx917 SoC, refer to [build OTA application using Simplicity Studio](./05-build-ota-application-using-studio.md).

### Creating Images

Once **OTA_B** application(**M4**) image is created in the above step, it will be used to create a Matter OTA file in case of combined image upgrade and application(**M4**) alone image upgrade.

#### Combined Image(TA+M4) Creation

For a combined image upgrade, the first step is to create a single image that contains both the TA and M4 images. Follow these steps:

1. **Set the combined image bit for both the TA and M4 images**

   - **Create the TA image with the combined image flag**

     ```shell
     commander rps convert <ta_image_combined.rps> --taapp <ta_image.rps> --combinedimage
     # Example:
     commander rps convert SiWG917-B.2.14.5.0.0.9_combined.rps --taapp SiWG917-B.2.14.5.0.0.9.rps --combinedimage
     ```

   - **Create the M4 image with the combined image flag**

     ```shell
     commander rps convert <m4_image_combined.rps> --app <m4_image.rps> --combinedimage
     # Example:
     commander rps convert SiWx917-lock-example_combined.rps --app SiWx917-lock-example.rps --combinedimage
     ```

2. **Combine the images**

   - Create the final combined image from the above-created TA and M4 images:

     ```shell
     commander rps convert "combined_image.rps" --app "m4_image_combined.rps" --taapp "ta_image_combined.rps"
     # Example:
     commander rps convert "combined_image.rps" --app "SiWx917-lock-example_combined.rps" --taapp "SiWG917-B.2.14.5.0.0.9_combined.rps"
     ```

#### Matter OTA Image Creation

**Create the Matter OTA file from the bootable image file**

- For a **combined image upgrade**, use the created `combined_image.rps` to generate the Matter OTA file.
- For **M4-only** or **TA-only** image upgrades, use the respective application(M4) or Wi-Fi(TA) firmware image to generate the Matter OTA file.

     ```shell
     # Example for combined image ota file
     ./src/app/ota_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 2 -vs "2.0" -da sha256 combined_image.rps combined_image.ota
     # Example for M4 alone application ota file
     ./src/app/ota_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 2 -vs "2.0" -da sha256 SiWx917-lock-example.rps SiWx917-lock-example.ota
     # Example for TA alone application ota file
     ./src/app/ota_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 2 -vs "2.0" -da sha256 SiWG917-B.2.14.5.0.0.9.rps SiWG917-B.2.14.5.0.0.9.ota
        ```

#### Running OTA-Provider

- Locate the **ota-provider** terminal. Run the Provider app along with the Matter OTA file created in the previous step.

    ```shell
     rm -r /tmp/chip_*
     # Example:
     ./out/debug/chip-ota-provider-app -f SiWx917-lock-example.ota
    ```

#### Running OTA-Requestor

Before running **ota-requestor** app, flash the **OTA-A** application(M4) and Wi-Fi(TA) firmware images for Silicon Labs Devices.

1. In a separate terminal, locate the chip-tool and ota-requestor, and run the chip-tool commands to provision the Provider.

    ```shell
     ./out/chip-tool pairing onnetwork <node_id> 20202021
     # Example:
     ./out/chip-tool pairing onnetwork 4 20202021

     ./out/chip-tool accesscontrol write acl '[{"fabricIndex": 1, "privilege": 5, "authMode": 2, "subjects": [112233], "targets": null}, {"fabricIndex": 1, "privilege": 3, "authMode": 2, "subjects": null, "targets": null}]' <node_id> 0
     # Example:
     ./out/chip-tool accesscontrol write acl '[{"fabricIndex": 1, "privilege": 5, "authMode": 2, "subjects": [112233], "targets": null}, {"fabricIndex": 1, "privilege": 3, "authMode": 2, "subjects": null, "targets": null}]' 4 0
    ```

2. If the application device had been previously commissioned, hold button 0 for 3 seconds to factory-reset the device.

3. In the chip-tool terminal, commission the device by passing below command.

    ```shell
     ./out/chip-tool pairing ble-wifi <node_id> "SSID" "PSK" 20202021 3840
     # Example:
     ./out/chip-tool pairing ble-wifi 1 my_ap my_psk 20202021 3840   
    ```

    where SSID and PSK are AP username and password.

4. Once the commissioning process completes, in the same terminal, run below requestor command to start downloading the image.

    ```shell
     ./out/chip-tool otasoftwareupdaterequestor announce-ota-provider 4 0 0 0 <node_id> 0
     # Example:
     ./out/chip-tool otasoftwareupdaterequestor announce-ota-provider 4 0 0 0 1 0
    ```

5. The application device will connect to the Provider and start the image download. Once the image is downloaded, the device will reboot into the downloaded image.

6. Once the device has rebooted and reconnected to the network, verify the software version using the following command:

    ```shell
    ./chip-tool basicinformation read software-version <node-id> 0
    # Example:
    ./chip-tool basicinformation read software-version 1 0
    ```

### Multi-Chip OTA images for SiWx917 NCP/SoC

Multi-Chip OTA images can be created using `ota_multi_image_tool.py` which creates .ota files that contain additional TLV headers.

>**Note**: SiWN917 NCP uses TLV tag 4 for Wi-Fi(TA) image upgrade.

#### Multi-Chip OTA image creation on SiWN917 NCP

Multi-Chip OTA on SiWN917 NCP supports application image upgrade, Wi-Fi(TA) image upgrade and combined image upgrade.

**Application Image Upgrade**

Create a bootable image file from *.s37* (using the lock application image as an example):

```shell
commander gbl create SiWx917-lock-example.gbl --app SiWx917-lock-example.s37 --compress lzma
```

```shell
./scripts/tools/silabs/ota/ota_multi_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 2 -vs "2.0" -da sha256 --app-input-file SiWx917-lock-example.gbl SiWx917-lock-example.ota
```

**Wi-Fi(TA) Image Upgrade**

```shell
./scripts/tools/silabs/ota/ota_multi_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 2 -vs "2.0" -da sha256 --wifi_ta_input_file SiWG917-B.2.14.5.0.0.10.rps SiWG917-B.2.14.5.0.0.10.ota
```

**Combined Image Upgrade**

```shell
./scripts/tools/silabs/ota/ota_multi_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 2 -vs "2.0" -da sha256 --app-input-file SiWx917-lock-example.gbl --wifi_ta_input_file SiWG917-B.2.14.5.0.0.10.rps combined_image.ota
```

#### Multi-Chip OTA image creation on SiWG917 SoC

>**Note**: SiWG917 SoC uses TLV tag 1 for all image upgrades M4 alone, TA alone and combined image upgrade.

**Application(M4) Image Upgrade**

```shell
./scripts/tools/silabs/ota/ota_multi_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 2 -vs "2.0" -da sha256 --app-input-file SiWx917-lock-example.rps SiWx917-lock-example.ota
```

**Wi-Fi(TA) Image Upgrade**

```shell
./scripts/tools/silabs/ota/ota_multi_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 2 -vs "2.0" -da sha256 --app-input-file SiWG917-B.2.14.5.0.0.10.rps SiWG917-B.2.14.5.0.0.10.ota
```

**Combined(TA+M4) Image Upgrade**
First combined image is formed from M4 and TA images using **Combined Image(TA+M4) Creation** section above.

```shell
./scripts/tools/silabs/ota/ota_multi_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 2 -vs "2.0" -da sha256 --app-input-file combined_image.rps combined_image.ota
```

**Encrypted Image Upgrade**

The TLV encryption will be controlled by the `--enc_enable` and `--input_ota_key` parameters passed to the `ota_multi_image_tool.py` script. The AES key will be programmed to the device by the Silicon Labs Matter Provisioning Tool (see https://docs.silabs.com/matter/2.2.0/matter-overview-guides/matter-provisioning and https://confluence.silabs.com/display/MATTER/Matter+Provisioning). The `ota_key` argument to the provision script should be used to provision the AES key to the device for decrypting OTA payload.

```shell
Example command:./provision.py write -ok <ota_key>
```

```shell
./scripts/tools/silabs/ota/ota_multi_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 2 -vs "2.0" -da sha256 --enc_enable --input_ota_key "<ota_key>" --app-input-file  SiWx917-lock-example.rps SiWx917-lock-example.ota
```
