# Building the 917 SoC Matter Accessory Devices (MADs) using Simplicity Studio

In Simplicity Studio 5, create the Light MAD:

1. [Download](https://www.silabs.com/developers/simplicity-studio) and Install Simplicity Studio 5.

2. To install the software packages for Simplicity Studio, refer to the [Software Package Installation Section](/matter/{build-docspace-version}/matter-wifi-getting-started-example/software-installation#installation-of-software-packages).

3. Switch to the Launcher view (if not already in it).

    ![Silicon Labs - design](images/siwx917-soc-launcher-tab.png)

4. Go to **All Products** in the **Launcher** tab and select one compatible board from the below supported list of SiWx917 SOC dev boards.

    ```shell
      BRD4338A (Common Flash)
    ```

    ![Silicon Labs - design](images/siwx917-soc-boardselection.png)

5. Once it shows up in the **Debug Adapters** view, select it.

    ![Silicon Labs - design](images/siwx917-soc-debugadapter.png)

6. Open the **Example Projects and Demos** tab, select the **Matter** filter, enter "*Wi-Fi*" in **Filter on keywords**, and click **CREATE**.

    ![Silicon Labs - design](images/siwx917-soc-create-wifiprojects.png)

   **Note**:- Make sure Installed Simplicity Studio is having IDE/GNU ARM v12.2.x version.

7. Rename the **Project Name** if you wish, and click **Finish**.

    ![Silicon Labs - design](images/siwx917-soc-projectwizard.png)

8. Once the project is created, right-click the project and select **Build Project** in the **Project Explorer** tab.

    ![Silicon Labs - design](images/siwx917-soc-build-wifiproject.png)

9. To flash the application, connect the compatible dev board to the machine or PC if not yet done.

10. Once the project is compiled successfully, go to the Project Explorer view and select the binary to be flashed.

    ![Silicon Labs - design](images/siwx917-soc-isp-binaryselection.png)

11. Right-click the selected *_isp.bin* binary and click **flash to device**.

    ![Silicon Labs - design](images/siwx917-soc-flashtodevice.png)

12. The Flash programmer window will open. Click the **Program** button to start the flashing.

    ![Silicon Labs - design](images/siwx917-soc-flashprogram.png)

    **Note:**
   Output of the SiWX917 SoC application will be displayed on the J-Link RTT Viewer.

13. In order to debug Matter Application, right-click the selected *_isp.bin* binary and click **Debug As**.

    ![Silicon Labs - design](images/siwx917-socdebug.png)
