# Upgrading the Wi-Fi Connectivity Firmware

Silicon Labs recommends that an upgrade of the NCP combos connectivity firmware be done under the following circumstances:

- When the EFR32 evaluation kit (EVK) is first received.
- When the radio board is first received.
- When upgrading to a new version of the WiSeConnect SDK v2.x or v3.x extension.

## Upgrading the Connectivity Firmware on NCP devices

The SiWx917 NCP or RS9116 EVK connectivity firmware can be upgraded using Tera Term or kermit.

### Connectivity Firmware Upgrade Using Tera Term

#### Firmware Upgrade On RS9116

1. Connect the EVK to PC using the USB interface labeled **UART** as identified below.

    ![Switch Position before firmware flash](images/rs916-board.png)

2. If this is the first time connecting the EVK to your PC, verify that it is properly detected by the PC. The EVK will appear to the PC as a COM port labeled **USB Serial Port (COMx)**.

3. Configure your terminal application with the following settings:

   - Configure the serial port settings to 115200 baud / 8-bit data / No parity / 1 stop bit
   - Enable local echo
   - Set receive and transmit new-line characters to CR+LF

4. Refer to [Setup Tera Term and Updating the Firmware](https://docs.silabs.com/rs9116/wiseconnect/2.0/tera-term-setup).

    ```shell
    Instructions are the same for both SiWx917 NCP and RS9116 EVK.
    ```

5. Once firmware flashing is done, the console displays **Loading...** followed by **Loading Done**.

#### Firmware Upgrade On SIWx917 NCP

1. Connect USB-UART Cable to Machine and WPK board as well with SOC Mounted on it.

    ![Connect NCP Board](./images/ncp-board-connect.png)

2. Connect USB-UART cable 2 (Yellow) to **F9** and 3 (Green) to **F8** on WPK Board shown below.

    ![Connect Port Wires](./images/connect-board-port.png)

3. Configure your terminal application with the following settings:

   - Configure the serial port settings to 115200 baud / 8-bit data / No parity / 1 stop bit
   - Enable local echo
   - Set receive and transmit new-line characters to CR+LF

4. Refer to [Setup Tera Term and Updating the Firmware](https://docs.silabs.com/rs9116/wiseconnect/2.0/tera-term-setup).

    ```shell
    Instructions are the same for both SiWx917 NCP and RS9116 EVK.
    ```

5. Once firmware flashing is done, the console displays **Loading...** followed by **Loading Done**.

### Troubleshooting an NCP Firmware Update Failure

If the firmware update fails, try the following:

- Toggle the power switch toward **AEM** (Advanced Energy Monitoring) on the WPK board.
- Perform the following steps and try the firmware update again.
  - Press the **RESET** button on the WSTK board.
  - Retry the firmware upgrade.

## Upgrading the Connectivity Firmware on SoC Devices

- SiWx917 SOC connectivity firmware can be upgraded using Simplicity Commander.

### Connectivity Firmware Upgrade Using Simplicity Commander
  
1. On the Simplicity Studio home page, click **Tools**.
  
2. In the Tools dialog, select **Simplicity Commander** and click **OK**.

    ![Silicon Labs - design](./images/select-commander.png)

3. In the Simplicity Commander window, click **Select Kit** and choose your radio board.

    ![Silicon Labs - design](./images/commander-select-board.png)

4. In the navigation pane, go to the **Flash** section.

5. Click **Browse** next to the **Binary File** field.

    ![Silicon Labs - design](./images/select-flash-option-in-commander.png)

6. Refer to [Firmware for SiWx917 SoC](/matter/<docspace-docleaf-version>/matter-prerequisites/matter-artifacts#siwx917-firmware-for-siwx917-so-c) to identify the correct firmware to be flashed into the specific hardware. Locate and select the firmware file to flash.
  
7. Click **Flash**.

    ![Silicon Labs - design](./images/commander-click-flash-button.png)

8. The firmware will be flashed, and the Log Window will display a "Resetting" message.

    ![Silicon Labs - design](./images/commander-flash-success.png)

### Troubleshoot SiWx917 SOC Firmware Update Failure

If the firmware update fails, try the following:

- Toggle the power switch toward **AEM** (Advanced Energy Monitoring) on the WSTK board.
- Perform the following steps and try the firmware update again
  - Press the **RESET** button on the WSTK board.
  - Retry the firmware upgrade.
  