# Matter OTA for 917 SOC
The scope of this page describes the matter OTA upgrade on 917 SoC mode for combined image(TA+M4) as well as single M4 and TA image upgrade.

## Hardware Requirements

- To run matter ota on Silicon Labs Platform, refer [Hardware Requirements](/matter/<docspace-docleaf-version>/matter-prerequisites/hardware-requirements).

## Software Requirements

- To run matter ota on Silicon Labs Platform, refer [Software Requirements](/matter/<docspace-docleaf-version>/matter-prerequisites/software-requirements).

## Combined Image Upgrade

For 917 SoC, storing a single Matter combined upgrade image(TA+M4) and then providing sample code that can transfer the image to the co-processor and rewrite the 917 firmware as well as M4 firmware Image then boot loading with the upgraded TA processor image and the M4 processor image.

Host will initiate OTA download to receive combined image (TA+M4) on to host. Host will store M4 and TA image on flash backup location. 

### Use Case of OTA :
- Combined image will be created and uploaded onto raspberry pi which provides the firmware image chunk by chunk to the device.
- Host will initiate the OTA download and provider app will start the OTA image transfer.
- Host will receive combined image and host will transfer the M4 and TA firmware images on to TA  chunk by chunk. . TA will write the TA image onto TA flash backup location. 
- Once both images are downloaded the device will reboot into the downloaded image.

### Create Combined (TA+M4) firmware image
- The first step is to create a combined Image that contains both the firmware (TA & M4).  
- This image is created by combining the binary images of both images. 
- For Matter OTA file, create a bootable image file (using the Lighting application image as an example) and then create the Matter OTA file from the bootable image file using commands provided below
- Once combined image .ota file is created , the same will be uploaded onto raspberry pi where OTA provider application is running. 

## Generating the Combined OTA image

- Create TA  image (.rps) with combined image flag set by using command
```shell
commander rps convert <ta_image_combined.rps> --taapp <ta_image.rps> --combinedimage
```
- Create M4 .rps file from .s37 using below command
```shell
- commander rps create <m4_image.rps> --app <m4_image.s37>
```
- Create M4 (.rps) with combined image flag set by using command
```shell
commander rps convert <m4_image_combined.rps> --app <m4_image.rps> --combinedimage
```
- Create combined image from the above created TA and M4 images
```shell
commander rps convert "combined_image.rps" --app "m4_image_combined.rps" --taapp "ta_image_combined.rps" 
```
- Create the Matter OTA file from the bootable image file
```shell
./src/app/ota_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 2 -vs "2.0" -da sha256 combined_image.rps combined_image.ota
```

### Running OTA Provider
- Locate **ota-provider** terminal start the Provider app passing to it the path to the Matter OTA bootable image file created in the previous step:

```shell
    rm -r /tmp/chip_*
    ./out/debug/chip-ota-provider-app -f combined_image.ota
```

### Setting up OTA-Requestor

- Before running **ota-requestor** app flash the bootloader binary images for Silicon Labs Devices.

### Running OTA-Requestor
- Enhancements to the wifi sdk IOT firmware upgrade application for matter OTA combined firmware application.

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

**Note:** once image downloaded done please disconnect jlink, it will reboot automatically with new image.


## Matter Software Update with SOC M4 Example Applications
- Host will initiate OTA download to receive M4 image on to host. Host will store M4 image on flash backup location.

### Use Case M4(alone) OTA
- OTA image will be created and uploaded onto raspberry pi which provides the firmware image chunk by chunk to the device.
- Host will initiate the OTA download and provider app will start the OTA image transfer.
- Host will receive M4 image and host will transfer the M4 image on to flash chunk by chunk.
- TA will write the M4 image onto flash backup location. 
Once image is downloaded the device will reboot into the upgraded M4 image.

## Generating the M4 OTA image

- Create M4 (.s37) image to  (.rps) image using below command
```shell
- commander rps create <m4_image.rps> --app <m4_image.s37>
```
- Create the Matter OTA file from the bootable image file
```shell
./src/app/ota_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 2 -vs "2.0" -da sha256 m4_image.rps m4_image.ota
```

### Running OTA Provider
- Locate **ota-provider** terminal start the Provider app passing to it the path to the Matter OTA file created in the previous step:

```shell
    rm -r /tmp/chip_*
    ./out/debug/chip-ota-provider-app -f m4_image.ota
```

### Setting up OTA-Requestor

- Before running **ota-requestor** app flash the bootloader binary images for Silicon Labs Devices.

### Running OTA-Requestor
- Enhancements to the wifi sdk IOT firmware upgrade application for matter OTA combined firmware application.

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

**Note:** once image downloaded done please disconnect jlink, it will reboot automatically with new image.

## Matter Software Update with SOC TA Example Application
- Host will initiate OTA download to receive TA image on to host. Host will transfer the image chunk by chunk on to TA flash backup location. 

### Use Case TA(alone) OTA:
- OTA image will be created and uploaded onto raspberry pi which provides the firmware image chunk by chunk to the device.
- Host will initiate the OTA download and provider app will start the OTA image transfer.
- Host will receive TA image and host will transfer the TA image on to flash chunk by chunk. 
- TA will write the TA upgrade image onto flash backup location. 
Once image is downloaded the device will reboot into the upgraded TA image.

## Generating the TA OTA image
- For Matter OTA file, create a bootable image file (using the Lighting application image as an example) and then create the Matter OTA file from the bootable image file using commands provided below
- Once  .ota file is created , the same will be uploaded onto raspberry pi where OTA provider application is running. 

- Create the Matter OTA file from the bootable image file
```shell
    ./src/app/ota_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 2 -vs "2.0" -da sha256 ta_image.rps ta_image.ota
```