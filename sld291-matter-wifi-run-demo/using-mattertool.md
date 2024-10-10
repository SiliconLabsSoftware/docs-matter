# Using the Mattertool (chip-tool)

The following commands show how to commission a 917 SoC Matter End Device (Matter Accessory Device), and then send the on/off commands with the `mattertool` automated script. The `mattertool` script provides an interface into various chip-tool commands used to create and interact with a Matter network.

## Prerequistes

- Download the raspi image and flash the image onto pi using with default '**ubuntu**' username and enable ssh in the options.

https://www.silabs.com/documents/public/software/SilabsMatterPi_2.3.0-1.3.zip

- Erase 917 SoC (brd4338a) and Flash the lighting app on 917 SoC and flash the connectivity firmware image.
- command for commission using mattertool :

```shell
  mattertool bleWifi -s <SSID> -p <passcode>
```

## Basic Mattertool Commands

| **Context**          | **Command**                                                       | **Usage**                                                                  |
| -------------------- | ----------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `Commissioning`      | `mattertool bleWifi`                                              | Starts commissioning of a Matter Accessory Device using the chip-tool      |
| `Commissioning`      | `mattertool pairing code`                                         | Commission a Matter end device which is already in the IPv6 local network  |
| `Commissioning`      | `<node_id> <pairing code>`                                        | using it's pairing code                                                    |
| `Multi-fabric`       | `mattertool pairing open-commissioning-window`                    | Open a commissioning window for a Matter end device                        |
| `Multi-fabric`       | `<node_id> <option> <window_timeout> <iteration> <discriminator>` | so that it can join another fabric                                         |
| `Device interaction` | `mattertool on`                                                   | Sends the _on_ command to the Matter Accessory Device using the chip-tool  |
| `Device interaction` | `mattertool off`                                                  | Sends the _off_ command to the Matter Accessory Device using the chip-tool |
| `Device interaction` | `mattertool onoff`                                                | Control the OnOff cluster of a specific Endpoint of a specific device      |

You can also use the full chip-tool command set (still using mattertool):

```shell
$ mattertool levelcontrol read current-level 106 1
```

| **Command**  | **Description**                                                                                   |
| ------------ | ------------------------------------------------------------------------------------------------- |
| help         | Prints help options                                                                               |
| bleWifi      | For Matter Bluetooth LE Wi-FI commissioning with 917 SoC device                                   |
| buildCT      | Clean build of the chip-tool                                                                      |
| cleanVars    | Erase every Set variable used in the script. They will be set back to default or randomized value |
| off          | Turn off the Light on the already-commissioned 917 SoC device                                     |
| on           | Turn on the Light on the already-commissioned 917 SoC device                                      |
| toggle       | Toggle the Light on the already-commissioned 917 SoC device                                       |
| parsePayload | Parse the given Payload (QrCode string)                                                           |
| rebuildCT    | Rebuild the chip-tool                                                                             |
| vars         | Print the Variables in use by the script                                                          |

Some options/arguments can be added to the command to update the values of the variables used by the script.

Available commands:

| **Command**           | **Description**                                       |
| --------------------- | ----------------------------------------------------- |
| -h, --help            | Prints help options                                   |
| -n, --nodeId DIGIT    | Specify the Nodeid you are trying to reach            |
| -e, --endpoint DIGIT  | Specify an endpoint for the desired cluster           |
| -s, --ssid STRING     | Wi-Fi AP SSID that the end devices need to connect to |
| -p, --password STRING | Wi-Fi AP password                                     |

These configurations are held until overwritten, cleared with cleanVars or when Raspberry Pi reboots.

Active variables used by mattertool:

| **Variable**  | **Value**                                             |
| ------------- | ----------------------------------------------------- |
| MATTER_ROOT   | /home/ubuntu/connectedhomeip                          |
| CHIPTOOL_PATH | /home/ubuntu/connectedhomeip/out/standalone/chip-tool |
| NODE_ID       | 31354                                                 |
| PINCODE       | 20202021                                              |
| DISCRIMINATOR | 3840                                                  |
| SSID          | \<your_SSID>                                          |
| lastNodeId    | 0                                                     |

You can preset them with export X=Y before running the script or use some available options to change some of them.

In most cases, MATTER_ROOT, CHIPTOOL_PATH, PINCODE, and DISCRIMINATOR should remain at the default set value.

For commissioning commands ( bleWifi), NODE_ID will be randomized if it is the same as the last pairing.

### Scripts Alias

The commands presented above are linked to scripts. You can edit **_.bashrc_** and rename the following alias to your liking.

```shell
$ alias mattertool=‘source $HOME/scripts/matterTool.sh’
```
