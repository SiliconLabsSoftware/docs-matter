
# Using the Mattertool (chip-tool)

The following commands show how to start a new wi-fi network, commission an 917 SoC Matter End Device (Matter Accessory Device), and then send the on/off commands with the `mattertool` automated script. The `mattertool` script provides an interface into various chip-tool commands used to create and interact with a Matter 
network.

## Basic Mattertool Commands

| **Context**	   | **Command**              | **Usage**                                                                 |
| --------------   | ------------------------ | ------------------------------------------------------------------------- |
| `Commissioning`  | `mattertool bleWifi`   | Starts commissioning of a Matter Accessory Device using the chip-tool      |
| `Commissioning`  | `mattertool pairing ble-thread`| Commission a Matter end device which is advertising itself           |
| `Commissioning`  | `<node_id> <Thread dataset> <pincode> <discriminator>` | with the provided pincode and discriminator  |
| `Commissioning`  | `mattertool pairing code` | Commission a Matter end device which is already in the IPv6 local network |
| `Commissioning`  | `<node_id> <pairing code>`| using it's pairing code                                                   |
| `Multi-fabric`   | `mattertool pairing open-commissioning-window` | Open a commissioning window for a Matter end device  |
| `Multi-fabric`   | `<node_id> <option> <window_timeout> <iteration> <discriminator>`| so that it can join another fabric |
| `Device interaction` | `mattertool on`       | Sends the _on_ command to the Matter Accessory Device using the chip-tool |
| `Device interaction` | `mattertool off`      | Sends the _off_ command to the Matter Accessory Device using the chip-tool|
| `Device interaction` | `mattertool onoff`    | Control the OnOff cluster of a specific Endpoint of a specific device     |
| `Device interaction` | `<action> <node_id> <endpoint_id>`      |                                                         |
| `Device interaction` | `mattertool doorlock set-user`          | Set a user for a Matter Lock                            |
| `Matter lock`        | `<OperationType> <UserIndex> <UserName> <UserUniqueId> <UserStatus> <UserType> <CredentialRule>`  |
| `Matter lock`        | `<node_id> <endpoint_id> --timedInteractionTimeoutMs <timeout value>`|                            |
| `Device interaction` | `mattertool doorlock set-credential`    | Set credential for a specific user of a Matter Lock     |
| `Matter lock`        | `<OperationType> <Credential> <CredentialData> <UserIndex> <UserStatus> <UserType> <node_id>`     |
| `Matter lock`        | `<endpoint_id> --timedInteractionTimeoutMs <timeout value>`|                                      |
| `Device interaction` | `mattertool doorlock unlock-door `      | Unlock a Matter Lock                                    |
| `Matter lock`        | `<node_id> <endpoint_id> --timedInteractionTimeoutMs <timeout value> `                            |
| `Device interaction` | `mattertool doorlock lock-door `        | Lock a Matter Lock                                      |
| `Matter lock`        | `<node-id/group-id> --timedInteractionTimeoutMs <timeout value> `                                 |
| `Device interaction` | `mattertool levelcontrol `              | Set the brightness level for a Matter dimmable light    |
| `Matter dimmabe light`|`move-to-level <desired_level> 0 1 1 <node_id> <endpoint_id> `                                    |
| `Device interaction` | `mattertool colorcontrol  `             | Set the saturation level for a Matter RGB light         |
| `Matter RGB light`   | `move-to-saturation <desired_saturation> 0 1 1 <node_id> <endpoint_id> `                          |
| `Device interaction` | `mattertool colorcontrol  `             | Set the hue level for a Matter RGB light                |
| `Matter RGB light`   | `move-to-hue <desired_hue> 0 0 1 1 <node_id> <endpoint_id> `                                      |
| `Device interaction` | `mattertool thermostat  `               | Read the local temperature from a Matter thermostat     |
| `Matter thermostat`  | `read local-temperature <node_id> <endpoint_id> `                                                 |
| `Device interaction` | `mattertool windowcovering  `           | Move the windows cover to a specific lift value         |
| `Matter window cover`| `go-to-lift-value <LiftValue> <node_id> <endpoint_id> `                                           |
| `Device interaction` | `mattertool windowcovering  `           | Open the windows cover                                  |
| `Matter window cover`| `up-or-open <node_id> <endpoint_id> `                                                             |
| `Device interaction` | `mattertool occupancysensing  `         | Read the occupancy status of a Matter occupancy sensor  |
| `Matter occupancy sensor`| `read occupancy <node_id> <endpoint_id> `                                                     |

You can also use the full chip-tool command set (still using mattertool):

```shell
$ mattertool levelcontrol read current-level 106 1
```

# Prerequistes 
- Downloaded the raspi image and flash the image onto pi using with default **ubuntu** username and enable ssh in the options.

https://www.silabs.com/documents/public/software/SilabsMatterPi_2.3.0-1.3.zip

- Erase 917 SoC (brd4338a) and  Flash the lighting app on 917 SoC. 
- command for commission using mattertool :

  mattertool bleWifi -s <SSID> -p <passcode>

| **Command**  | **Description**                                                                                               |
| ------------ | ------------------------------------------------------------------------------------------------------------- |
| help         | Prints help options                                                                                           |
| bleWifi      | For Matter Bluetooth LE Wi-FI commissioning with 917 SoC device                                              |
| buildCT      | Clean build of the chip-tool                                                                                   |
| cleanVars    | Erase every Set variable used in the script. They will be set back to default or randomized value             |
| off          | Turn off the Light on the already-commissioned 917 SoC device                                                   |
| on           | Turn on the Light on the already-commissioned 917 SoC device                                                    |
| toggle       | Toggle the Light on the already-commissioned EFR32 device                                                     |
| parsePayload | Parse the given Payload (QrCode string)                                                                       |
| rebuildCT    | Rebuild the chip-tool                                                                                          |
| vars         | Print the Variables in use by the script                                                                      |

Some options/arguments can be added to the command to update the values of the variables used by the script.

Available commands:

| **Command**              | **Description**                                       |
| ------------------------ | ----------------------------------------------------- |
| -h, --help               | Prints help options                                   |
| -n, --nodeId DIGIT       | Specify the Nodeid you are trying to reach            |
| -e, --endpoint DIGIT     | Specify an endpoint for the desired cluster           |
| -s, --ssid STRING        | Wi-Fi AP SSID that the end devices need to connect to |
| -p, --password STRING    | Wi-Fi AP password                                     |

These configurations are held until overwritten, cleared with cleanVars or when Raspberry Pi reboots.

Active variables used by mattertool:

| **Variable**    | **Value**                                             |
| --------------- | ----------------------------------------------------- |
| MATTER_ROOT     | /home/ubuntu/connectedhomeip                          |
| CHIPTOOL_PATH   | /home/ubuntu/connectedhomeip/out/standalone/chip-tool |
| NODE_ID         | 31354                                                 |
| PINCODE         | 20202021                                              |
| DISCRIMINATOR   | 3840                                                  |
| SSID            | \<your_SSID>                                          |
| lastNodeId      | 0                                                     |

You can preset them with export X=Y before running the script or use some available options to change some of them.

In most cases, MATTER_ROOT, CHIPTOOL_PATH, PINCODE, and DISCRIMINATOR should remain at the default set value.

For commissioning commands ( bleWifi), NODE_ID will be randomized if it is the same as the last pairing.


### Scripts Alias

The commands presented above are linked to scripts. You can edit **_.bashrc_** and rename the following alias to your liking.

```shell
$ alias mattertool=‘source $HOME/scripts/matterTool.sh’
```
