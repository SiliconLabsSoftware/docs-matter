# Apple Ecosystem Setup and Demo Execution

This page describes how to set up the Apple Ecosystem for Matter and test a Matter application using Apple Home Pod Mini.

## Hardware Requirements

For the Hardware required for an Apple EcoSystem, refer to the [Ecosystem overview Prerequisites section](./index#prerequisites).

## Software Requirements

- Apple Account
- Apple Home App on Smartphone

**Note:** Apple only has Matter support with IOS version-16.1 or higher.

## Set Up Apple HomePod and Apple Phone

Refer to Apple's [Set up HomePod or HomePod mini](https://support.apple.com/en-in/HT208241)

## Matter Demo Execution using Apple HomePod

1. Refer to [Getting Started with Matter over Wi-Fi](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example) for instructions on setting up Silicon Labs Matter Accessory Device.

2. Connect a board to a computer.

   - For Wi-Fi NCP Mode Boards, see [Connect EFR32 Board to Computer](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example/getting-started-efx32-ncp#connect-the-boards-to-a-computer).
   - For Wi-Fi SoC Mode Boards, see [Connect SiWx917 SoC to Computer](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example/getting-started-with-soc#connect-siwx917-soc-to-computer).

3. Flash the bootloader binary for your device along with the application (for example, lighting, lock, thermostat, window covering, or light-switch) using [Simplicity Commander](/matter/<docspace-docleaf-version>/matter-wifi-run-demo/flashing-using-commander).

4. In the Apple Home App, click the "+" button.
![Apple Home App](./images/apple-home-app.png?width=40%&height=40%)

5. Select **Add Accessory**.
![Add accessory](./images/apple-home-app-add-accessory.png?width=40%&height=40%)

6. It will prompt you to scan the QR Code using a smartphone camera.
![scan QR code](./images/apple-home-app-scan-qr-code.png?width=40%&height=40%)

7. Connect the device to a computer and scan the QR code within the Home app.

8. Proceed to add the device to your home. You should see LED0 fast blinking when commissioning happens.

9. Once commissioning is complete, the Apple Home app prompts you to **select One Room** for your Matter application. Select any room as per your choice and enter the Application name. (For Example: Light, Lock)

### Control the Light via Apple Home App

- In the Apple Home app, you can now tap your light to turn it ON and OFF.
- You can control the light by giving a voice command (for example, 'Hey Siri! Turn ON Light') and through the app user interface.
- You will see the LED1 on your WSTK board turned on or off depending on the command you enter.

### Delete the Matter Application From Apple Home

1. Click the Matter Application for the detailed view.
2. Scroll down to the end.
3. Select **Remove Accessory**.
4. Confirm to remove from **My Home** and your Matter application is removed from Apple Home.

**Note**: Removing the Matter application from Apple Home App removes it from Apple Home Pod as well.
