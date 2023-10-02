# Serial Port Communication on Silicon Labs Platform
  The matter-shell exposes the configuration and the management APIs via matter command line interface (matter CLI). This interface can be used to change the state of the device.

## Hardware Requirement
- To run matter shell on Silicon Labs Platform, refer [Hardware Requirments](/matter/<docspace-docleaf-version>/matter-prerequisites/hardware-requirements)

## Software Requirement
- To run matter shell on Silicon Labs Platform, refer [Software Requirments](/matter/<docspace-docleaf-version>/matter-prerequisites/software-requirements)

## Execution of Matter Shell on Silicon Labs Platform

1. [Download](https://www.silabs.com/developers/simplicity-studio) and Install Simplicity Studio.
   
2. To install the software packages for Simplicity Studio, refer [Software Package Installation](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example/software-installation#installation-of-software-packages)

3. Log in to Simplicity Studio and connect the EFR32 board to the computer.

4. Go to the All Products section.
   ![Silicon Labs - design](./images/all-products-selection.png)

5. Type and Select the radio board from the displayed list and select Start.
   ![Silicon Labs - design](./images/select-efx-board.png)

6. The Launcher page will display the selected radio board's details.
   ![Silicon Labs - design](./images/overview-tab-efx32.png)

7. Verify the following in the General Information section:
   - The Debug Mode is Onboard Device (MCU).
   - The Preferred SDK is the version you selected earlier.
   ![Silicon Labs - design](./images/create-project-verify-efx-general-information.png)

8. Click on Example Projects and Demos Option and Create Project for **Matter Lock Application**.
   ![Silicon Labs - design](./images/create-project-select-efx-lock-example.png)

9. In the New Project Wizard window, click Finish.
   ![Silicon Labs - design](./images/create-project-lock-click-finish.png)

10. After creation of project , click on **Software Components** tab and in search bar type **Matter Shell** and install it.
    ![Silicon Labs - desing](./images/matter-shell-enable.png)

11. Build the Project after Enabling **Matter Shell** Component.

12. After successful build commission the device , refer [Commission Matter Platform](./run-matter-demo#creating-the-matter-network)

13. Open Tera Term and under New Connection, under Serial Port, select JLink port and click **OK**.
    ![Silicon Labs - design](./images/tera-term-select-jlink-port.png)

14. Click on Setup from Menu bar and change the value to 115200 under Speed category, then click on New setting.
    ![Silicon Labs - design](./images/tera-term-selection-in-terminal.png)

15. Inside **Terminal** Set the below values and click **OK**.
  - Terminal Size : 80 * 24
  - New-Line
    - Receive : CR+LF
    - Transmit : CR+LF
    ![Silicon Labs - design](./images/tera-term-terminal-setup.png)

16. Click on File from Menu bar again, select **Serial Port** option.
    ![Silicon Labs - design](./images/tera-term-select-serial-port.png)

17. Increase the speed to **115200** and click on **New setting**.
    ![Silicon Labs - design](./images/tera-term-select-speed.png)

18. Click on File from Menu bar, select TTY Record. Create any empty file with extension " .tty " and click on save.
    ![Silicon Labs - design](./images/tera-term-tty-record.png)

19. After creating tty file just click on **Enter** button from Keyboard then it will show you **matterCli** terminal.
    ![Silicon Labs - design](./images/tera-term-matter-cli.png)

20. Send any command through **matterCli** terminal, from the below list of commands:

  1. doorlock event door-state-change "DoorState"
      - Door State List
        - DoorOpen = 0
        - DoorClosed = 1
        - DoorJammed = 2
        - DoorForcedOpen = 3
        - DoorUnspecifiedError = 4
        - DoorAjar = 5
  2. doorlock event lock-alarm "AlarmCode"
        - Alarm Code List
        - LockJammed = 0
        - LockFactoryReset = 1
        - LockRadioPowerCycle = 3
        - WrongCodeEntryLimit = 4
        - FrontEsceutcheonRemoved = 5
        - DoorForcedOpen = 6
        - DoorAjar = 7
        - ForcedUser = 8
  3. onboardingcodes ble, command will show QR Code.
      ![Silicon Labs - design](./images/matter-shell-command-send.png)

21. After changing DoorState and AlarmCode in **matterCli**, run below commands using chip-tool in raspberry pi to verify the event.
  - To Read Door State
  
    ./chip-tool doorlock read-event door-state-change "node_id" "endpoint"
  
  - To Read Alarm Code
  
    ./chip-tool doorlock read-event door-lock-alarm "node_id" "endpoint"

  **Note**: Type **help** in matterCli terminal for more information about supported features.