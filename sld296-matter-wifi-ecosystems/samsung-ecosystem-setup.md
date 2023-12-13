# Samsung Ecosystem Setup and Demo Execution

## Hardware Requirements

For the hardware required for a Samsung Smart Thing EcoSystem, refer to the [Ecosystem Prerequisites section](./index#prerequisites).

## Software Requirements

- Samsung Account
- Samsung Smart things App on smartphone, as described in the next section

## Setup of Samsung Smart Home Hub

See the Aeotec instructions on [How to Set Up a Smart Home Hub](https://aeotec.freshdesk.com/support/solutions/articles/6000240326-how-to-setup-smart-home-hub).

## Matter Demo Execution using Samsung Smart Aeotec

1. Refer to the [Getting Started Overview Guide](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example) for setting up a Silicon Labs Matter Accessory Device.

2. Connect a board to a computer.

   - For Wi-Fi NCP Mode Boards, see [Connect EFR32 Board to Computer](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example/getting-started-efx32-ncp#connect-the-boards-to-a-computer).
   - For Wi-Fi SoC Mode Boards, see [Connect SiWx917 SoC to Computer](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example/getting-started-with-soc#connect-siwx917-soc-to-computer).

3. Flash the bootloader binary for your device along with the application (for example, lighting, lock, thermostat, window covering, or light-switch) using [Simplicity Commander](/matter/<docspace-docleaf-version>/matter-wifi-run-demo/flashing-using-commander).

4. Open the Smart Things app, tap **'+**, and select **Add device**.
![Add device](./images/samsung-app-add-device.png?width=40%&height=40%)

5. Select Partner Devices.
![Partner devices](./images/samsung-app-select-partner.png?width=40%&height=40%)

6. Through the Smart Things app scan the Application QR code to trigger commissioning.

7. After scanning the QR code, verify commissioning is triggered by checking on the DUT logs.
![commissioning in logs](./images/samsung-app-commissioning.png?width=40%&height=40%)

8. The last step of the commissioning process is to register your device with Access Point.
![Register device](./images/samsung-register-device.png?width=40%&height=40%)

9. Once commissioning has succeeded, verify the Matter application is added in one room of the Smart Things app and is in online mode.
![Light added](./images/samsung-light-added.png?width=40%&height=40%)

10. In the Samsung Smart Thing app, you can now tap your light to turn it ON and OFF. You will see the LED1 on your WSTK board turned on or off depending on the command you enter. **Note**: Samsung Smart Things does not support voice control commands.

## Deleting the Matter Application From Samsung Smart Things App

- In order to remove the Matter application from Samsung Smart Things app go to **Devices Section**.
- Long Press and Hold Matter application and click **Remove**.
- If you want to add the Matter application again follow the procedure above.
