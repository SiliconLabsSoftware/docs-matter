# Wake on Matter End-to-End Validation

The example's `scripts/` directory includes two helper scripts that you can use to validate a complete Wake on Matter setup on an Ubuntu-based OpenThread Border Router (OTBR) host:

- `scripts/verify_install.sh`: Checks that `cpcd.service` and `otbr-agent.service` are installed and running, and that the `wpan0` interface is available and up.
- `scripts/tests/end_to_end_validation.sh`: Runs the installation checks, commissions a Matter accessory and the Wake on Matter NCP, configures the ACL, and establishes a subscription.

> **Note:** The end-to-end validation script is still under development. Use it at your own risk.

## Run the Script

Complete the [Prerequisites](./01-prerequisites.md) before running the validation script:

```sh
./scripts/tests/end_to_end_validation.sh
```

## Validate Script Steps

The script performs the following steps in order:

1. **Verify the installation:** Runs `verify_install.sh` to check `cpcd.service`, `otbr-agent.service`, and `wpan0`. If an active dataset exists but `wpan0` is down, the script attempts to bring up the interface using `ot-ctl`.
2. **Commission the accessory over BLE-Thread:** Reads the active dataset using `sudo ot-ctl dataset active -x` and then runs:

   ```sh
   chip-tool pairing ble-thread <ACCESSORY_NODE_ID> hex:<dataset> <SETUP_PINCODE> <DISCRIMINATOR>
   ```

3. **Commission the Wake on Matter NCP:** Checks the device state using `mmic_host matter_state`. If a fabric already exists, the script runs `mmic_host decommission` and verifies that the fabric count returns to 0. It then runs:

   ```sh
   mmic_host commission <NCP_NODE_ID>
   mmic_host matter_state          # must show the new nodeId
   ```

4. **Grant ACL access:** Grant the NCP permission to establish  a CASE session with the accessory:

   ```sh
   chip-tool accesscontrol write acl \
       '[{"fabricIndex": 1, "privilege": 1, "authMode": 2, "subjects": [<NCP_NODE_ID>], "targets": null}]' \
       <ACCESSORY_NODE_ID> 0
   ```

5. **Establish a subscription**: Establishes a subscription from the NCP to the accessory:

   ```sh
   mmic_host establish_subscription \
       <SUB_FABRIC_INDEX> <ACCESSORY_NODE_ID> \
       <SUB_ENDPOINT_ID> <SUB_CLUSTER_ID> <SUB_ATTRIBUTE_ID>
   ```

The script reports `[PASS]` or `[FAIL]` for each step. If a step fails, the script stops with exit code `1`, tand prints a summary. If you interrupt the script using `Ctrl+C`, it stops with exit code `130`.

## Configuration

You can override the default configuration values using environment variables.

The following table lists the available variables and their default values.

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

This example commissions the Wake on Matter NCP with node ID `200` and targets a `lighting-app` accessory with node ID `42`. It subscribes to the `OnOff` attribute (`0x0000`) of the `OnOff` cluster (`0x0006`) on endpoint `1`:
Run the following command to override the default values:
```sh
NCP_NODE_ID=200 \
ACCESSORY_NODE_ID=42 \
SUB_CLUSTER_ID=0x0006 \
SUB_ATTRIBUTE_ID=0x0000 \
SUB_ENDPOINT_ID=1 \
./scripts/tests/end_to_end_validation.sh
```
