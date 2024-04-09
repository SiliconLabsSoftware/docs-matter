
# Running a Matter over Wi-Fi Application

To run a Matter over Wi-Fi application, you must first create a Matter network using the chip-tool, and then control the Matter device from the chip-tool.

## Creating the Matter Network

This procedure uses the chip-tool installed on the Matter Hub. The commissioning procedure does the following:

- Chip-tool scans BLE and locates the Silicon Labs device that uses the specified discriminator.
- Establishes operational certificates.
- Sends the Wi-Fi SSID and Passkey.
- The Silicon Labs device will join the Wi-Fi network and get an IP address. It then starts providing mDNS records on IPv4 and IPv6.
- Future communications (tests) will then happen over Wi-Fi.

Commissioning can be done using chip-tool running either on Linux or Raspberry Pi.

1. Get the SSID and PSK of the Wi-Fi network (WPA2 - Security) you are connected to.
2. Go to **$MATTER_WORKDIR/matter** directory and run the following:

```shell
$ out/standalone/chip-tool pairing ble-wifi <node_id> <ssid> <password> <pin_code> <discriminator>
```

In this command:

- node_id is the user-defined ID of the node being commissioned.
- ssid and password are credentials.
- pin_code and discriminator are device-specific keys.

  **Note**: You can find these values in the logging terminal of the device (for instance UART) when the device boots up. For example:

![Device Configuration](./images/device-configuration.png)

The node ID used here is 1122. This will be used in future commands. '\$SSID' is a placeholder for your Wi-Fi SSID, and '\$PSK' is a placeholder for the password of your Wi-Fi network. '20202021' is the Setup Pin Code used to authenticate the device. '3840' is the Setup Discriminator used to discern between multiple commissionable device advertisements.

If there are any failures, run the following command and then re-run the chip-tool command:

```shell
$ rm -rf /tmp/chip_*
```

If you are having difficulty getting the chip-tool to commission the device successfully, it may be because you have more than one network interface available to the chip-tool. The device on which you are running the chip-tool must be on the same Wi-Fi network. For instance, if you have an Ethernet connection as well as a Wi-Fi connection, you need to unplug the Ethernet connection and try running the chip-tool.

## Controlling the Matter Accessory Device

1. In a PuTTY session to the Matter hub, use the chip-tool to test the Matter light device.

   1. Control the light status of the light MAD Using `./chip-tool onoff on nodeID  1`. You can also use  `chip-tool toggle nodeID 1`.
   2. For dev board with buttons available, you can use **BTN1** to toggle the light status locally.

## Factory Reset the Device

As the device remembers the Access Point credentials given for commissioning, if you want to run the demo multiple times, do a factory reset by pressing **BTN0**
on the WSTK for about 6-7 seconds. The **LED0** will flash 3 times.
