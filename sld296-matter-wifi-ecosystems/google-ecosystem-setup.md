# Google Ecosystem Setup and Demo Execution

## Hardware Requirements

For the hardware required for the Google Nest Hub Ecosystem, refer to the [Ecosystem overview Prerequisites section](./index#prerequisites).

## Software Requirements

- Google Account
- Google Home App

## Set Up Google Home and Android Smartphone

### Prerequisites for Google Setup

To run the Google Ecosystem demo, you need both Google and a Matter device. You also need a Google Nest Hub 2nd Generation and an Android phone (at least a Pixel 5 is recommended) that can run at least Android 8 (8.1, API Level 27) or newer and has Bluetooth LE capability.

### Set Up the Android Phone

Follow these instructions to set up the Android phone with the necessary applications:

- [Install the Google Home app](https://play.google.com/store/apps/details?id=com.google.android.apps.chromecast.app&pli=1)
- Follow the in-app steps.

**NOTE:** Currently SiWx917 SoC only supports 2.4GHz channels so ensure that the phone and hub are connected to the 2.4GHz WiFi SSID.

## Matter Integration Setup in the Developer Console

You have now completed setting up the following:

- Your home in the Google home app in your Android smartphone
- A device running the Matter application e.g. lighting, light-switch, lock.

Having finished the above, the only step left to have your setup ready is to open a QR code webpage for the light device type in your PC. A QR Code link will be present in Device configuration section of logs. Copy the link and paste it in google chrome so you will be able to QR Code.

![QR code link page](./images/matter-rtt-qr-code-link.png)

## Matter Demo Execution using Google Home

### Commission Matter Device through Google Home App

1. Refer to [Getting Started Overview Guide](/matter/{build-docspace-version}/matter-wifi-getting-started-example) for setting up a Silicon Labs Matter Accessory Device.

2. Connect board to a computer.

   - For Wi-Fi NCP Mode Boards, see [Connect EFR32 Board to Computer](/matter/{build-docspace-version}/matter-wifi-getting-started-example/getting-started-efx32-ncp#connect-the-efx32-boards-to-a-computer).
   - For Wi-Fi SOC Mode Boards, see [Connect SiWx917 SOC to Computer](/matter/{build-docspace-version}/matter-wifi-getting-started-example/getting-started-with-soc#connect-siwx917-soc-to-computer).

3. Flash the bootloader binary for your device along with the application (for example, lighting, lock, thermostat, window covering, or light-switch) using [Simplicity Commander](/matter/{build-docspace-version}/matter-wifi-run-demo/flashing-using-commander).

4. Open the Google Home app on your phone.

5. Click **Devices Section** and tap **Add**.

   ![Add device](./images/google-home-app-add-device.png?width=40%&height=40%)

6. On the **Set up a device** screen, tap **New device**.

   ![New Device](./images/google-home-app-new-device.png?width=40%&height=40%)

   **NOTE:** If the device is running a development version of the application, a prompt will appear stating that "Uncertified device". Proceed to set up the device anyway.

7. On the **Choose a home** screen, select your home and tap **Next**.

   ![home selection](./images/google-home-app-select-home.png?width=40%&height=40%)

8. The Google Home App searches for a nearby Matter device.

   ![looking for device](./images/google-home-app-looking-for-device.png?width=40%&height=40%)

9. If the device is found, tap the application that you flashed on the device, such as Light or Lock.

10. If the device is not found, tap **Matter-enabled device**.

    ![Matter enabled device](./images/google-home-app-matter-enabled-device.png?width=40%&height=40%)

11. Once the Google Home app has found the device, it will ask you to scan its QR code.

12. Google Home app asks if you want to connect this device to your Google account. Tap **Agree**.

    ![Add to account](./images/google-home-app-account-prompt.png?width=40%&height=40%)

13. The Google Home app now starts to commission the device with Bluetooth LE.

    ![Commissioning](./images/google-home-app-connecting.png?width=40%&height=40%)

14. Once you see the **Device connected** message, tap **Done**.

    ![App Connected](./images/google-home-app-connected.png?width=40%&height=40%)

15. The Google Home App now asks you to select a room where you want to keep the **Application**. You can select any room from the list and tap **Next**.

    ![Select room](./images/google-home-app-select-room.png?width=40%&height=40%)

16. At the prompt to create a unique name for the application (For Example: Light, Lock), create any name to identify the application and tap **Next**.

    ![app name](./images/google-home-app-give-app-name.png?width=40%&height=40%)

17. You will now see your device (for example, Light) shown as being connected to your Google account and added to your selected room at Step 15.

    ![Light added](./images/google-home-app-light-added.png?width=40%&height=40%)

### Control the Light via Google Home App

1. In the Google Home app, you will now be able to tap your light to turn it ON and OFF.
2. You can control the light by giving a voice command (for example, 'Ok Google! Turn ON Light') and through the app user interface.
3. You will see the **LED1** on your WSTK board turned on or off depending on the command you enter.

## Deleting Matter Application from Google Home

1. Press and hold **Matter Application** for a detailed view.
2. Tap **Setting** on the top right corner.
3. Select the **Remove device** option.
4. At **Unlink all Matter apps & services from device**, select **Unlink**.
