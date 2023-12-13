# Amazon Ecosystem Setup and Demo Execution

## Hardware Requirements

For the hardware required for an Amazon EcoSystem, refer to the [Ecosystem Prerequisites section](./index#prerequisites).

## Software Requirements

- Amazon account
- Amazon Alexa App on a smartphone

## Amazon Alexa and Android Smartphone Setup

### Amazon Alexa MSS (Matter Simple Setup)

As part of partnership with Amazon, the following link contains information required for Matter device certification with Amazon.

[https://developer.amazon.com/docs/frustration-free-setup/matter-simple-setup-for-wifi-overview.html](https://developer.amazon.com/docs/frustration-free-setup/matter-simple-setup-for-wifi-overview.html)

In the context of MSS for Wi-Fi, the provisionee, or commissionee, is the device that is to be automatically set up. If you want to make your device eligible to be an MSS commissionee, you must satisfy the following:

  1. Configure the device to beacon over Bluetooth LE (BLE) with specific fields needed for MSS for Wi-Fi (detailed below).
  
  2. Onboard your device via the FFS developer portal by creating a Matter new device type. On the developer portal, you will manage your FFS onboarding lifecycle tasks, like managing your test devices and manufacturing data and submitting for certification.
  
  3. Integrate a unique barcode on your device packaging. You can also use an existing unique barcode on your packaging, such as a serial number, or MAC address.
  
  4. Share your device control log data with Amazon services. Control Logs are a mechanism that allows manufacturers to provide Amazon with unique device identifiers and authentication material, such as the Matter passcode, that are critical to ensure a frictionless customer setup. The unique package barcode is associated with your device identifier through the control logs. See the Matter Control Logs section for more details.
  
  5. Complete Frustration-Free Setup certification and Amazon ASIN onboarding. Review the certification section below for more information.

### Amazon Alexa Setup

Refer to [Set up Alexa in a Few Easy Steps](https://www.amazon.com/alexa-setup-guide/b?ie=UTF8&node=17978645011).

## Matter Demo Execution using Amazon Alexa

1. Refer to the [Getting Started Overview Guide](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example) for setting up a Silicon Labs Matter Accessory Device.

2. Connect a board to a computer.

   - For Wi-Fi NCP Mode Boards, see [Connect EFR32 Board to Computer](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example/getting-started-efx32-ncp#connect-the-boards-to-a-computer).
   - For Wi-Fi SoC Mode Boards, see [Connect SiWx917 SoC to Computer](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example/getting-started-with-soc#connect-siwx917-soc-to-computer).

3. Flash the bootloader binary for your device along with the application (for example, lighting, lock, thermostat, window covering, light-switch) using [Simplicity Commander](/matter/<docspace-docleaf-version>/matter-wifi-run-demo/flashing-using-commander).

4. Once the Amazon Alexa setup is done, make sure echo dot is ready.

5. Make sure the Matter Application is flashed into the Matter Device (for example, EFR32MG24, SiWx917 SoC, SiWx917 NCP).

6. In the Alexa App, tap **Devices section**.

![Devices section](./images/amazon-alexa-app.png?width=40%&height=40%)

7. Tap "+" at the top right corner. Three options are displayed: 

   - Add device
   - Add group
   - Combine speakers

8. Tap **Add device**.  Several options are displayed.

    ![Add device](./images/amazon-alexa-add-device.png?width=40%&height=40%)

9. Scroll down and select **other** option.

    ![Device selection](./images/amazon-alexa-device-selection.png?width=40%&height=40%)

10. Logos such as “Matter”, “Bluetooth”, “Zigbee”, “Wi-fi”, “Z-wave" are displayed. Tap the “Matter” logo.

    ![Matter logo](./images/amazon-alexa-logos.png?width=40%&height=40%)

11. Alexa App will ask "Does your device have a matter logo?" Select "Yes".

12. Alexa will prompt "Locate a QR code shown for your device." Select **Scan QR Code**.

    ![Scan QR code](./images/amazon-alexa-scan-qr-code.png?width=40%&height=40%)

13. After scanning the QR code through a smartphone camera, verify Commissioning is started by checking the Device logs.

14. Once commissioning is triggered the Alexa app will prompt for Access Point Credentials. Add them.

15. After Access Point Credentials are provided the device will join to the network and commissioning is completed.

    ![App added](./images/amazon-alexa-app-added.png?width=40%&height=40%)

16. Next, select a group for your device (for example, Bedroom), and click **Add to Group**.

    ![Select a group](./images/amazon-alexa-select-group.png?width=40%&height=40%)

17. Now the application is ready to use. You can see the Matter application in Amazon Alexa app inside the **Groups Panel** at the **Bedroom** tab.

   ![Alexa application added to group](./images/amazon-alexa-application-added-to-group.png?width=40%&height=40%)

In the Amazon Alexa app, you will now be able to tap your light to turn it ON and OFF. You can also control the light by giving a voice command (for example, 'Hey Alexa! Turn ON Light') and through the app user interface.

The LED1 on your WSTK board will turn on or off depending on the command you enter.

## Deleting Matter Application from Amazon Alexa

1. Click Matter Application for detailed view.
2. Click **Setting** button on top right corner.
3. Select **Dustbin Button** on top right corner, it will prompt **Remove "First light"**. Click **DELETE**.
