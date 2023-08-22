# Commissioning Wi-Fi Device using Android

Commissioning can be done using an Android Phone through the following steps.

Download pre-built application from the
[Matter Artifacts page](/matter/<docspace-docleaf-version>/matter-prerequisites/matter-artifacts).

1. Open the .apk that is installed in the Android mobile.
2. Connect the Android phone to the Wi-Fi Access Point that is going to be used.
3. Run the installed CHIP app.
4. Click 'Provision Chip device with Wi-Fi'.
5. The app will bring up the camera:
    - Hold the camera to the LCD on the WSTK board
    - Scan the QR Code displayed on LCD screen of EFR32 MG12 Platform
6. Input the SSID/Passphrase of the Wi-Fi Access Point on the next screen. You will see messages (Toasts) pop up - saying that the App is 'Scanning', then 'Pairing', followed by 'Commissioning Done'
7. Once commissioning is completed, the app will go back to the original/home
   screen
8. Click on 'Light ON/OFF & Level Cluster'
9. You can then bring up the On/Off Cluster and send On/Off Commands (Toggle
   does not work as required currently) - this will cause LED 1 on the WSTK to
   change states

If the Commissioning is not successful, try rebooting your mobile and try
again.

Once commissioning is completed, if you want to repeat the test, follow these
steps:

-   Disconnect the system (EFR32MG12 + RS9116) from power.
-   Power up the system again - this should cause the LCD to turn on and the QR
    code to show up
-   Press the BTN0 button and keep it pressed for about 1 min - this should
    cause LED0 and LED1 to turns ON and OFF for 3 times. You can then release
    the button
