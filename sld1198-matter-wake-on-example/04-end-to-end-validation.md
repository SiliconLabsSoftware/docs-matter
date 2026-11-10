# Wake on Matter End-to-End Validation

The example's `scripts/` directory includes two helper scripts. Together, they test a complete Wake on Matter setup from an Ubuntu-based OpenThread Border Router (OTBR) host:

- `scripts/verify_install.sh`: checks that `cpcd.service`, `otbr-agent.service`, and the `wpan0` interface are present and running.
- `scripts/tests/end_to_end_validation.sh`: runs the checks above. Then it commissions an accessory and the Wake on Matter NCP, writes the ACL, and establishes a subscription.

> **Note:** The end-to-end validation script is a work in progress. Use it at your own risk.

## Running the Script

Complete the [Prerequisites](./01-prerequisites.md) first, then run:

```sh
./scripts/tests/end_to_end_validation.sh
```

## Script Steps

The script runs these steps in order:

1. **Verify the installation:** runs `verify_install.sh` to check `cpcd.service`, `otbr-agent.service`, and `wpan0`. If a dataset exists but `wpan0` is down, the script brings it up with `ot-ctl`.
2. **Commission the accessory over BLE-Thread:** reads the active dataset with `sudo ot-ctl dataset active -x`, then runs:

   ```sh
   chip-tool pairing ble-thread <ACCESSORY_NODE_ID> hex:<dataset> <SETUP_PINCODE> <DISCRIMINATOR>
   ```

3. **Commission the Wake on Matter NCP:** first checks the device with `mmic_host matter_state`. If a fabric is already present, the script runs `mmic_host decommission` and checks that the fabric count is back to 0. Then it runs:

   ```sh
   mmic_host commission <NCP_NODE_ID>
   mmic_host matter_state          # must show the new nodeId
   ```

4. **Grant ACL access:** lets the NCP open a CASE session with the accessory:

   ```sh
   chip-tool accesscontrol write acl \
       '[{"fabricIndex": 1, "privilege": 1, "authMode": 2, "subjects": [<NCP_NODE_ID>], "targets": null}]' \
       <ACCESSORY_NODE_ID> 0
   ```

5. **Establish a subscription** from the NCP to the accessory:

   ```sh
   mmic_host establish_subscription \
       <SUB_FABRIC_INDEX> <ACCESSORY_NODE_ID> \
       <SUB_ENDPOINT_ID> <SUB_CLUSTER_ID> <SUB_ATTRIBUTE_ID>
   ```

Each step prints `[PASS]` or `[FAIL]`. The script stops at the first failed step with exit code `1`, then prints a summary. If you press `Ctrl+C`, the script stops with exit code `130`.

## Configuration

You can override every value with an environment variable. Default values are shown below.

| Variable             | Default                          | Purpose                                    |
| -------------------- | -------------------------------- | ------------------------------------------ |
| `CHIP_TOOL`          | `chip-tool`                      | chip-tool binary                           |
| `MMIC_HOST`          | `mmic_host`                      | mmic_host binary                           |
| `VERIFY_SCRIPT`      | `<script_dir>/verify_install.sh` | Path to `verify_install.sh`                |
| `ACCESSORY_NODE_ID`  | `1`                              | Node ID assigned to the Matter accessory   |
| `NCP_NODE_ID`        | `100`                            | Node ID assigned to the Wake on Matter NCP |
| `SETUP_PINCODE`      | `20202021`                       | Accessory setup PIN code                   |
| `DISCRIMINATOR`      | `3840`                           | Accessory setup discriminator              |
| `SUB_FABRIC_INDEX`   | `1`                              | Fabric index used for the subscription     |
| `SUB_ENDPOINT_ID`    | `0`                              | Subscription endpoint                      |
| `SUB_CLUSTER_ID`     | `0x0028`                         | Basic Information cluster                  |
| `SUB_ATTRIBUTE_ID`   | `0x0000`                         | DataModelRevision attribute                |
| `COMMISSION_TIMEOUT` | `180`                            | BLE-Thread commissioning timeout (s)       |
| `CHIP_TOOL_TIMEOUT`  | `60`                             | chip-tool ACL write timeout (s)            |
| `MMIC_TIMEOUT`       | `30`                             | mmic_host command timeout (s)              |

### Example

This example commissions the NCP with node ID `200`. It targets a `lighting-app` accessory with node ID `42`, subscribing to the `OnOff` attribute (`0x0000`) of the `OnOff` cluster (`0x0006`) on endpoint `1`:

```sh
NCP_NODE_ID=200 \
ACCESSORY_NODE_ID=42 \
SUB_CLUSTER_ID=0x0006 \
SUB_ATTRIBUTE_ID=0x0000 \
SUB_ENDPOINT_ID=1 \
./scripts/tests/end_to_end_validation.sh
```
