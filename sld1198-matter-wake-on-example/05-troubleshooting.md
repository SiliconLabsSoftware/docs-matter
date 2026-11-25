# Wake on Matter Troubleshooting
Use the following table to troubleshoot common issues with the Wake on Matter example.
| Symptom | Resolution |
| ------- | ---------- |
| `verify_install.sh` reports `ifconfig not installed` | Install the `net-tools` package by running `sudo apt-get install net-tools`. |
| `wpan0` doesn't appears | An active OpenThread dataset might be missing. Create one by running `sudo ot-ctl dataset init new && sudo ot-ctl dataset commit active`. |
| `chip-tool pairing ble-thread` stops responding | The accessory might not be advertising over Bluetooth Low Energy (BLE), or the host might be unable to communicate with BlueZ. Make sure the accessory is in commissioning mode and verify that the Bluetooth service is running by using `sudo systemctl status bluetooth`. |
| `mmic_host matter_state` shows an incorrect fabric node ID | A stale fabric might be present. The validation script automatically runs `mmic_host decommission` if it detects an existing fabric. If the check still fails, decommission the device manually and run the script again. |
| Subscription fails at Sigma1 with a `destinationId` mismatch | The accessory and NCP might be on different fabrics, or the NCP might have a stale Identity Protection Key (IPK). Factory-reset the NCP and decommission the accessory using `chip-tool pairing unpair <node-id>`. Then rerun the validation script from the accessory commissioning step. |
| No logs appear on the serial port | The application outputs logs only through the [Segger RTT interface](https://www.segger.com/products/debug-probes/j-link/tools/rtt-viewer/). Use J-Link RTT Viewer or another RTT client to view the logs. |
| Lost access to the target node after writing the ACL | The `write acl` command replaces the entire ACL list. Factory-reset and recommission the target node, then write the ACL again, making sure to preserve the existing administrator entry. For more information, see [Configuring Wake on Matter](./03-configure-wake-on-matter.md#step-2-grant-acl-access-on-the-target-node). |
