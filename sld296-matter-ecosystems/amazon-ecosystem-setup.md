# Amazon Ecosystem Setup and Demo Execution

## Hardware Requirements

For the hardware required for an Amazon EcoSystem, refer to the [Ecosystem Prerequisites section](./index#prerequisites).

## Software Requirements

- Amazon account
- Amazon Alexa App on a smartphone

## Amazon Alexa and Android Smartphone Setup

### Amazon Alexa MSS (Matter Simple Setup) - Wi-Fi

As part of partnership with Amazon, the following link contains information required for Matter device certification with Amazon.

[https://developer.amazon.com/docs/frustration-free-setup/matter-simple-setup-for-wifi-overview.html](https://developer.amazon.com/docs/frustration-free-setup/matter-simple-setup-for-wifi-overview.html)

In the context of MSS for Wi-Fi, the provisionee, or commissionee, is the device that is to be automatically set up. If you want to make your device eligible to be an MSS commissionee, you must satisfy the following:

1. Create an Amazon Developer Account

   Sign up for an Amazon Developer account at https://developer.amazon.com/ if you don't already have one.

2. Create a Test Product in the Developer Console

   In the Amazon Developer Console, create a new test product for Matter Simple Setup (MSS).
   
   Reference: https://developer.amazon.com/docs/frustration-free-setup/matter-simple-setup-getting-started.html#create-your-product

3. Generate and Upload Control Logs

   This step involves three parts: generating control logs, uploading them to Amazon and downloading the feedback form.

   a. Generate Control Logs
   
      Follow Option 1 in the Amazon documentation: https://developer.amazon.com/docs/frustration-free-setup/matter-simple-setup-getting-started.html#generating-control-logs
      
      1. Install Gradle.
      2. Run the following command (replace placeholder values with your actual values):

      ```bash
      gradle run --args="-apid APID -dsn DeviceSerialNumber -vid MatterVendorID -pid MatterProductID -p MatterDevicePasscode -a MATTER_V0 -d MatterDeviceDiscriminator -udid Base64EncodedUniqueDeviceId -pk "PublicKeyOfProduct"
      ```

      Command Inputs:

      - `-apid`: Amazon-provided Advertised Product ID (Go to FFS Console → Products -> <your_product> -> Advertised Product ID)
      - `-dsn`: Serial Number of the Amazon Echo Device
      - `-vid`: Vendor ID
      - `-pid`: Product ID
      - `-p`: Matter device passcode
      - `-a`: Matter encryption algorithm
      - `-d`: Device discriminator
      - `-udid`: Base64-encoded Unique Device ID
      - `-pk`: Public key of your Amazon product (FFS Console → Products → <your_product> → Device Cryptographic Material)

   b. Upload Control Logs to Amazon
   
      - Follow the documentation steps to upload the generated control logs : https://developer.amazon.com/docs/frustration-free-setup/matter-simple-setup-getting-started.html#uploading-control-logs

   c. Download Feedback logs from Amazon
   
      - Follow the steps given in : https://developer.amazon.com/docs/frustration-free-setup/matter-simple-setup-getting-started.html#getting-control-log-feedback-files


4. Pre-Register Test Devices

   Pre-register your test devices by following the instructions here:
   
   https://developer.amazon.com/docs/frustration-free-setup/matter-simple-setup-getting-started.html#test-devices

5. Verify Amazon Account Settings

   - Open your account settings: https://www.amazon.com/hz/mycd/preferences/myx#/home/settings/payment
   - Ensure Country/Region is set to United States (US).
   - Confirm that Simple Sign-In and Frustration-Free Setup automations are enabled.


6. Barcode Specification

   Integrate a unique barcode on your device packaging. You can also use an existing unique barcode on your packaging, such as a serial number, or MAC address. Refer to this link for more details:
   
   https://developer.amazon.com/docs/frustration-free-setup/matter-simple-setup-for-wifi-overview.html#packaging-barcode

7. Complete Frustration-Free Setup Certification

   The certification process given by Amazon can be found here:
   
   https://developer.amazon.com/docs/frustration-free-setup/provisionee-certification.html

8. Amazon ASIN Onboarding

   For configuring the Amazon Standard Identification Number (ASIN), refer to the documentation given by Amazon here:
   
   https://developer.amazon.com/docs/frustration-free-setup/asin-configuration.html

**Changes that should be made in the application:**

Amazon FFS requires use of an optional feature in Matter called additional advertising. This can be enabled in a Matter Studio project by adding the **GATT Additional Advertising** component to the project. In a GN based build, it can be included by adding the two optional build arguments to the GN build:

```
chip_enable_additional_data_advertising=true
chip_enable_rotating_device_id=true
```

Ensure that the device advertises the fields mentioned in this link over BLE:

https://developer.amazon.com/docs/frustration-free-setup/matter-simple-setup-for-wifi-overview.html#ble-beaconing 


### Amazon Alexa MSS (Matter Simple Setup) - Thread

As part of partnership with Amazon, the following link contains information required for Matter device certification with Amazon.

[https://developer.amazon.com/docs/frustration-free-setup/matter-simple-setup-for-thread-overview.html](https://developer.amazon.com/docs/frustration-free-setup/matter-simple-setup-for-thread-overview.html)

In the context of MSS for Thread, the provisionee, or commissionee, is the device that is to be automatically set up. If you want to make your device eligible to be an MSS commissionee, you must satisfy the following:

1. Configure your device to beacon over BLE with specific fields needed for MSS for Thread (detailed below)

2. Onboard your device via the FFS developer portal by creating a Matter new device type. On the developer portal, you will manage your FFS onboarding lifecycle tasks, like managing your test devices and manufacturing data and submitting for certification.

3. Integrate a unique barcode on your device packaging. You can also use an existing unique barcode on your packaging, such as a serial number, or MAC address.

4. Share your device control log data with Amazon services. Control Logs are a mechanism that allows manufacturers to provide Amazon with unique device identifiers and authentication material, such as the Matter passcode, that are critical to ensure a frictionless customer setup. The unique package barcode is associated with your device identifier through the control logs. See the Matter Control Logs section for more details.

5. Complete Frustration-Free Setup certification and Amazon ASIN onboarding. Review the certification section below for more information.

### Amazon Alexa Setup

Refer to [Set up Alexa in a Few Easy Steps](https://www.amazon.com/alexa-setup-guide/b?ie=UTF8&node=17978645011).

## Matter Demo Execution using Amazon Alexa

1. Refer to the [Getting Started Overview Guide](/matter/{build-docspace-version}/matter-wifi-getting-started-example) for setting up a Silicon Labs Matter Accessory Device.

2. Connect a board to a computer.
   - For Wi-Fi NCP Mode Boards, see [Connect EFR32 Board to Computer](/matter/{build-docspace-version}/matter-wifi-getting-started-example/getting-started-efx32-ncp#connect-the-boards-to-a-computer).
   - For Wi-Fi SoC Mode Boards, see [Connect SiWx917 SoC to Computer](/matter/{build-docspace-version}/matter-wifi-getting-started-example/getting-started-with-soc#connect-siwx917-soc-to-computer).

3. Flash the bootloader binary for your device along with the application (for example, lighting, lock, thermostat, window covering, light-switch) using [Simplicity Commander](/matter/{build-docspace-version}/matter-wifi-run-demo/flashing-using-commander).

4. Once the Amazon Alexa setup is done, make sure echo dot is ready.

5. Make sure the Matter Application is flashed into the Matter Device (for example, EFR32MG24, SiWx917 SoC, SiWx917 NCP).

6. In the Alexa app, tap **Devices**.

   ![Devices section](./images/amazon-alexa-app.png?width=40%&height=40%)

7. Tap "+" at the top right corner. Three options are displayed:

   - Add device
   - Add group
   - Combine speakers

8. Tap **Add Device**. Several options are displayed.

   ![Add Device](./images/amazon-alexa-add-device.png?width=40%&height=40%)

9. Scroll down and select **Other** option.

   ![Device selection](./images/amazon-alexa-device-selection.png?width=40%&height=40%)

10. Logos such as “Matter”, “Bluetooth”, “Zigbee”, “Wi-fi”, and “Z-wave" are displayed. Tap the “Matter” logo.

    ![Matter logo](./images/amazon-alexa-logos.png?width=40%&height=40%)

11. Alexa will ask **Does your device have a matter logo?** Select **Yes**.

12. Alexa will prompt **Locate a QR code shown for your device**. Select **Scan QR Code**.

    ![Scan QR code](./images/amazon-alexa-scan-qr-code.png?width=40%&height=40%)

13. After scanning the QR code through a smartphone camera, verify that commissioning is started by checking the Device logs.

    **NOTE:** If the device is running a development version of the application, a prompt will appear stating that "This device isn't Matter compatible". Proceed to set up the device anyway.

14. Once commissioning is triggered, the Alexa app will prompt for Access Point Credentials. Add them. The results on this page vary based on the device used. Sometimes a device does not show the particular Access Point so add it manually.

15. After Access Point Credentials are provided, the device will join to the network and commissioning is completed.

    ![App added](./images/amazon-alexa-app-added.png?width=40%&height=40%)

16. Next, select a group for your device (for example, Bedroom), and tap **Add To Group**.

    ![Select a group](./images/amazon-alexa-select-group.png?width=40%&height=40%)

17. Now the application is ready to use. You can see the Matter application in the Amazon Alexa app inside the **Groups Panel** at the **Bedroom** tab.

![Alexa application added to group](./images/amazon-alexa-application-added-to-group.png?width=40%&height=40%)

In the Amazon Alexa app, you will now be able to tap your light to turn it ON and OFF. You can also control the light by giving a voice command (for example, 'Hey Alexa! Turn ON Light') and through the app user interface.

The **LED1** on your WSTK board will turn on or off depending on the command you enter.

## Deleting Matter Application from Amazon Alexa

1. Tap the Matter Application for a detailed view.
2. Tap the **Setting** button on top right corner.
3. Select **Dustbin Button** on top right corner. It will prompt **Remove "First light"**. Tap **DELETE**.
