# Create a Project for an EFR32 Application

This page provides a detailed description on how to create an Wi-Fi NCP project for EFR32 boards.

1. [Download](https://www.silabs.com/developers/simplicity-studio) and Install Simplicity Studio.

2. To install the software packages for Simplicity Studio, refer to [Software Package Installation](/matter/<docspace-docleaf-version>/matter-prerequisites/software-requirements#installation-of-software-packages).

3. Log in to Simplicity Studio and connect the EFR32 WSTK board to the computer.

4. Go to the **All Products** section.

   ![All Products](images/ncp-all-products.png)

   

5. Search and select the radio board from the displayed list and select **Start**.

   ![Select the radio board](images/ncp-board-selection.png)

6. The Launcher page will display the selected radio board's details.

   ![Overview tab](images/overview-tab-efx32.png)

7. Verify the following in the General Information section:
   - The Debug Mode is Onboard Device (MCU).
   - The Preferred SDK is the version you selected earlier.

   ![Verify SDK](images/create-project-verify-efx-general-information.png)

8. Open the **Example Projects and Demos** tab, select a project, and click **Create Project**.

   ![Create Project](images/ncp-proj-create.png)

9. In the New Project Wizard window, click **Finish**.

   ![Finish project](images/ncp-proj-config.png)

10. Once the solution is created, right-click the project and select **Build Project** in the Project Explorer tab.

    ![Build project](images/ncp-build-proj.png)

11. Once the project is compiled successfully, go to the Project Explorer view and expand the binaries folder to flash the binary.

    ![Select binary](images/ncp-binary-selection.png)

12. Right-click the selected '.s37' binary and click **flash to device**.

    ![flash to device](images/ncp-flash-binary.png)

13. The Flash programmer window opens. Click **Erase** and then **Program** to start flashing.

    ![Flash binary](images/ncp-flash-binary-efr32.png)

**Note:** Output of the EFR32 NCP Host application will be displayed on the J-Link RTT Viewer.
