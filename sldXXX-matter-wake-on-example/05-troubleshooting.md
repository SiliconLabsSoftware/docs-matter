# Wake on Matter Troubleshooting

| Symptom | Resolution |
| ------- | ---------- |
| `verify_install.sh` reports `ifconfig not installed` | Install `net-tools`: `sudo apt-get install net-tools`. |
| `wpan0` never appears | No active dataset exists. Create one: `sudo ot-ctl dataset init new && sudo ot-ctl dataset commit active`. |
| `chip-tool pairing ble-thread` hangs | The accessory is not advertising, or the host cannot reach BlueZ. Make sure the device is in commissioning mode and that `sudo systemctl status bluetooth` shows the service is active. |
| `mmic_host matter_state` shows the wrong fabric node ID | A stale fabric is present. The validation script runs `mmic_host decommission` automatically in this case. If the check still fails, decommission the device manually and run the script again. |
| Subscription fails at Sigma1 with a `destinationId` mismatch | The accessory and NCP are on different fabrics, or the NCP has a stale IPK. Factory-reset the NCP. Decommission the accessory with `chip-tool pairing unpair <node-id>`. Then run the script again from step 2. |
| No logs appear on the serial port | This application outputs logs only through the [Segger RTT interface](https://www.segger.com/products/debug-probes/j-link/tools/rtt-viewer/). Use an RTT viewer. |
| Lost access to the target node after writing the ACL | `write acl` replaces the full ACL list. Factory-reset and recommission the target, then write the ACL again. Include the existing administrator entry. See [Configuring Wake on Matter](./03-configure-wake-on-matter.md#step-2-grant-acl-access-on-the-target-node). |
