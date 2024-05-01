# Building the 917 SoC Matter Accessory Devices (MADs) using Simplicity Studio

In Simplicity Studio 5, create the Light MAD:

1. [Download](https://www.silabs.com/developers/simplicity-studio) and Install Simplicity Studio 5.
2. To install the software packages for Simplicity Studio, refer to the [Software Package Installation section](/matter/<docspace-docleaf-version>/matter-wifi-getting-started-example/software-installation#installation-of-software-packages).

3. Switch to the Launcher view (if not already in it).

    ![Silicon Labs - design](images/siwx917-Launcher.png)

4. Go to **All Products** in the **Launcher** tab and select a compatible board from the supported SiWx917 SOC dev boards.

    ```shell
      BRD4338A (Common Flash)
    ```

    ![Silicon Labs - design](images/siwx917-board.png)

5. Once it shows up in the **Debug Adapters** view, select it.

    ![Silicon Labs - design](images/siwx917-soc-debugadapter.png)

6. Open the **Example Projects and Demos** tab, select the **Matter** filter, and enter *Wi-Fi* in **Filter on keywords** and click **CREATE**.

    ![Silicon Labs - design](images/siwx917-project-create.png)

7. Rename the Project Name if you wish, and click **Finish**.

    ![Silicon Labs - design](images/siwx917-proj-config.png)

8. Once the project is created, right-click on the project and select **Build Project** in the **Project Explorer** tab.

    ![Silicon Labs - design](images/siwx917-build-proj.png)

9. To flash the application, connect the compatible dev board to the machine or PC if not yet done.

10. Once the project is compiled successfully, go to the Project Explorer view and select the binary to be flashed.

    ![Silicon Labs - design](images/siwx917-binary-selection.png)

11. Right-click the selected *_isp.bin* or *.rps* binary file and click on **Flash to Device**.

    ![Silicon Labs - design](images/siwx917-flash.png)

    **Note**: SiWX917 SoC device will support both **_isp.bin** and **.rps** file format to flash.

12. The Flash programmer window will open. Click the **Program** button to start the flashing.

    ![Silicon Labs - design](images/siwx917-flash-programmer.png)

    **Note**: Output of the SiWX917 SoC application will be displayed on the J-Link RTT Viewer.

13. In order to debug Matter Application, right-click the selected *_isp.bin* binary and click on **Debug As**.

    ![Silicon Labs - design](images/siwx917-debug-page.png)