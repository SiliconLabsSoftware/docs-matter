# Light and Switch Step-by-Step Example

## Setting up the Matter Hub/Chip-Tool

This procedure prepares the Raspberry Pi 4B (RPi4B) to become a Matter Hub. You should have downloaded the Matter Hub Raspberry Pi image and Raspberry Pi Imager as described in the [Overview](/matter/<docspace-docleaf-version>/matter-overview). The Raspberry Pi image contains software called chip-tool, which provides a command-line interface into the Matter protocol. 

1. Install the Raspberry Pi Imager and insert the SD card into the PC to flash the image.

   1. Open the Imager, select the Operating System as 'Custom OS' and browse for the Raspberry Pi Image.

   2. Select the storage as an SD card.

   3. Click the settings icon to configure the access point (AP) credentials, Hostname and user credentials. Make sure the 5 GHz Wi-Fi credentials of the dual-band AP are entered.

   4. Click the 'write' option. **Note** this will erase all existing content on that SD card.

2. Insert the SD card into Raspberry Pi 4B (RPi4B).

3. Power-up the RPi4B. Once it is booted up, check the Raspberry Pi's IP address. Refer to [Finding Raspberry Pi IP address](/matter/<docspace-docleaf-version>/matter-references/find-raspi) in the References chapter to get the IP address or enter the Hostname directly in PuTTY. 

4. Use PuTTY to connect to RPi4B.

   1. The first time connecting to RPi4B, PuTTY will warn about a new host key or key fingerprint. Accept the key.
   2. The credentials (username: password) are the same given Step 1.
   3. Switch to root mode and navigate to path "/home/ubuntu/connectedhomeip/out/standalone" to find the chip-tool.

Matter hub/chip-tool are ready and working. Keep the PuTTY session open for the following steps.

## Creating the Matter Accessory Devices (MADs)

### Hardware Requirements
-   SiWx917 / BRD4002A / Wireless Starter Kit
-   SiWx917 SoC Mode
    -   SiWx917 SoC / Common Flash Radio Board / 2.4GHz
        -   BRD4338a - B0 common flash v2.0

    **Note:**
    Refer [SiWx917 SoC](https://www.silabs.com/development-tools/wireless/wi-fi/siwx917-pro-kit?tab=techdocs) for more details.

### Software Requirements
- In order to Run Light and Switch Example on SiWx917 SOC, softwares to be installed on System. Refer to[Software Requirements](/matter/<dospace-docleaf-version>/matter-prerequisites/software-requirements)

- **Note**: Light and Switch application is not supported for NCP hardwares.

1. In Simplicity Studio 5, create the Light MAD:

   1. Switch to the Launcher view (if not already in it).

   2. Connect one compatible dev board to the development computer. 

   3. Once it shows up in the Debug Adapters view, select it.

   4. Open the Example Projects and Demos tab, select the **Matter** filter and enter "*Wi-Fi*" in **Filter on keywords**.

   5. Select the *Matter - Lighting over Wi-Fi* example, click **Create**, rename the project if you wish, and click **Finish**.

   6. Once the project is created, the perspective changes to the Simplicity IDE perspective. In the Project Explorer view, right-click the project and select *Build Project*.

   7. Once the project has compiled, in the Debug Adapters view right-click the board and select *Upload application*.

   8. Select the *Application image path* (Select the path for .s37 for efr32 and .rps for soc in the path '\<workspace\>\project_name\GNU ARM v10.3.1 - Default') for the newly compiled project and a *Bootloader image for EFR32*. The EFR32MG24 devices must be programmed with a bootloader. Obtain those here: [Silicon Labs Matter Artifacts](/matter/<docspace-docleaf-version>/matter-prerequisites/matter-artifacts).

   9. Disconnect the dev board from development computer.

   10. **Optional**: Label this device (eg: my_light or my_switch) to make it easier to identify later.

2. Repeat the process with the second Dev board, but select the *Matter - Light Switch over Wi-Fi* example instead.

## Creating the Matter Network

This procedure uses the chip-tool installed on the Matter Hub. Chip-tool includes many commands. The following are some that are used in this example:

- `chip-tool ble-wifi pairing`
- `chip-tool onoff`
- `chip-tool toggle`
- `chip-tool accesscontrol`
- `chip-tool binding`

In a PuTTY session to the Matter hub, use the chip-tool to commission the Matter light device.The various compatible boards will have different setups for their LED(s). Typically one LED (or a color channel, if RGB) will be used to indicate the network status of the device:

- A short flash indicates the MAD is advertising to join a network

- A rapid flash indicates the commissioning is in progress

- Solid ON: the MAD is now in the network

1. Power up the Matter Light device.

2. Once it is powered up and booted, use the PuTTY session to commission the device using

   `./*chip-tool pairing ble-wifi  nodeID SSID PSK 20202021 3840`
  
   where `nodeID` is replaced with the desired ID (for example `./chip-tool pairing ble-wifi 1122 Silabs PSK 20202021 3840`).

3. Make sure the SSID and PSK given here are of 2.4 GHz of the Dual Band AP.

   Be sure to note which nodeIDs are used for Matter light and  Matter light_switch devices. These will be needed later for modifying the Matter light's ACL & the Matter light switch's binding table.

4. Power up the Matter light switch device and commission it too, using a different `nodeID`.

Now two Matter accessory devices (MADs) are on the network and ready to be used.

## Controlling the Light MAD

1. In a PuTTY session to the Matter hub, use the chip-tool to test the Matter light device.

   1. Control the light status of the light MAD Using `./chip-tool onoff on nodeID  1`. You can also use `chip-tool onoff off`  and `chip-tool toggle`.
   2. For dev board with buttons available, you can use BTN1 to toggle the light status locally.

2. In a PuTTY session to the Matter hub, use the chip-tool to bind the light_switch MAD to the light MAD, thus allowing the switch to control the light.

   1. First, modify the Access Control List (ACL) of the Matter light device. This list determines which device in the network the Matter light device will react to. Use: `./chip-tool accesscontrol write acl '[ { "fabricIndex" : 1 , "privilege" : 5 , "authMode" : 2 , "subjects" : [`**`112233`**`] , "targets" : null } , { "fabricIndex" : 1 , "privilege" : 3 , "authMode" : 2 , "subjects" : [`**`nodeID-switch`**` ], "targets" : null }]' `**`nodeID-light 0`**, where the highlighted parameters are:

      - **112233**: The node ID of the controller. This is always 112233.

      - **nodeID-switch**: The node ID of the Matter light switch device.

      - **nodeID-light**: The node ID of the Matter light device.

      - **0**: The endpoint in the Matter light device that holds the ACL. This is always 0.

      To read the ACL for a Matter device use: `./chip-tool accesscontrol read acl`**`nodeID 0`**, where the highlighted parameters are:

      - **nodeID**: The nodeID of the Matter device (Light or Light_switch) to read the ACL contents from.

      - **0**: The endpoint in the Matter device that holds the ACL. This is always 0.

   2. Second, bind the switch's write command to the light. This is done by updating the binding table of the Matter light_switch device. This can be done using the command: `./chip-tool binding write binding '[ { "fabricIndex" : 1 , "node" :`**`nodeID-light`**,` "endpoint" : `**`1`**,`"cluster" :`**`6`**`} ]'`**`nodeID-switch 1`**, where the highlighted parameters are:

      - **nodeID-light**: The node ID of the Matter light device.

      - **1**: The application endpoint in the light. This is always 1.

      - **6**: The on/off cluster in the light. This is always 6.

      - **nodeID-switch**: The node ID of the switch.

      - **1**: This is the application endpoint in the switch that holds the binding table. This is always 1.

      The binding table from a Matter device can be read using: `./chip-tool binding read binding`**`nodeID-switch 1`**, where the highlighted parameters are:

      - **nodeID-switch**: The node ID of the Matter switch.

      - **1**: The application endpoint in the switch that holds the binding table. This is always 1.

3. With the binding complete, a button press (BTN1) on Matter light_switch device should now toggle the light status of Matter light device.
