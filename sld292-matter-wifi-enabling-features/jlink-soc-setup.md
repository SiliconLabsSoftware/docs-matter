# Ozone and JLink RTT Environment Setup for a SiWx917 SoC Device
- For Common Flash Boards Ozone debugging support is not enabled. To get the logs use for SOC **JLink RTT** tool will be used.
- Auto detection of SiWx917 SoC device in **Ozone or JLink RTT** is not enabled.
- Follow the steps to manually configure the SiWx917 SoC with Latest **JLink RTT**

## Steps to Configure the SiWx917 SoC on the JLink-RTT Logging and Ozone Debugger

1.  Update the JlinkDevices.xml and ELF files found in the [Matter Artifacts Page](/matter/<docspace-docleaf-version>/matter-prerequisites/matter-artifacts)
    - Download the JLinkDevices.xml file and copy it in your **JLink RTT** installation path shown in this [JlinkDevices Folder](https://wiki.segger.com/J-Link_Device_Support_Kit#JLinkDevices_folder).  If there is no JLinkDevices Folder, create a JLinkDevices folder and copy the JlinkDevices.xml file.
    - In the `JLinkDevices` folder, create a `Devices` folder and then create a sub-folder named `SiliconLabs`.
    - Download the **ELF** file (Flash driver) and copy it in the created `SiliconLabs` folder.

2. Launch **JLink RTT**. The SiWx917 Common Flash SoC device should be visible in the Device field’s selection list.

![Search SOC](./images/search-soc-jlink.png)

3. Select **SI917COMMONFLASH** and, click Ok.

![Select SOC](./images/select-common-flash-soc.png)