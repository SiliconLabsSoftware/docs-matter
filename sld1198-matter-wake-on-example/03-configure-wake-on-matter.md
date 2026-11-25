# Configure Wake on Matter

In this example, the Wake on Matter (WoM) device subscribes to attributes on another Matter device through a NCP connected to the host, such as a Raspberry Pi. When a subscription report matches a configured wake-up trigger, the WoM device wakes the host.

## Step 1: Commission the WoM Device

Commission the WoM device onto a Matter over Thread network. To commission the device from the host, use `mmic_host`:

```sh
mmic_host commission <woM node ID>
mmic_host matter_state    # shows the new node ID
```

## Step 2: Grant ACL Access on the Target Node

On the target node, grant the WoM device permission to establish a Certificate Authenticated Session Establishment (CASE) session and subscribe to attributes:

```sh
chip-tool accesscontrol write acl '[{"fabricIndex": 1, "privilege": 1, "authMode": 2, "subjects": [<woM node ID>], "targets": null}]' <target node ID> 0
```

> **Important:** The `write acl` command replaces the entire access control list (ACL). It doesn't add an entry to the existing list. If the target node already has ACL entries, include them in the same JSON array to avoid losing access to the node.

For example, to preserve the administrator entry for chip-tool (node ID 112233) while adding the WoM device:
>
> ```sh
> chip-tool accesscontrol write acl '[{"fabricIndex": 1, "privilege": 5, "authMode": 2, "subjects": [112233], "targets": null}, {"fabricIndex": 1, "privilege": 1, "authMode": 2, "subjects": [<woM node ID>], "targets": null}]' <target node ID> 0
> ```

## Step 3: Establish a Subscription

On the host, establish a subscription from the WoM device to the target node:

```sh
mmic_host establish_subscription <fabricIndex> <nodeId> <endpointId> <clusterId> <attributeId>
```

For example, to subscribe to the `OnOff` attribute of the `OnOff` cluster on endpoint `1` of node `1`,  run::

```sh
mmic_host establish_subscription 1 1 1 0x0006 0x0000
```

## Step 4: Set Up a Wake-Up Trigger

Add a wake-up trigger. When the WoM device receives a subscription report that matches the trigger, it turns on the LED.

```sh
addWakeUp <clusterId> <attributeId> <mode> <operand>
```
The command accepts the following arguments:
| Argument      | Description                                         |
| ------------- | --------------------------------------------------- |
| `clusterId`   | Cluster ID to match                                 |
| `attributeId` | Attribute ID to match                               |
| `mode`        | Match mode: `0` = Boolean, `1` = Bitmask, `2` = Equal |
| `operand`     | Value to compare with the reported attribute value    |

For example, to wake up when the `OnOff` cluster reports the `OnOff` attribute changing to on:

```sh
addWakeUp 6 0 0 1
```

## Step 5: Verify the Wake-Up Triggers

List the active triggers to check that the trigger was added:

```sh
> wakeUpList
Active wake-up triggers (1):
cluster=0x00000006 attribute=0x00000000 mode=Boolean(0) operand=0x0000000000000001
```

To test the trigger, toggle the target device. For example, run:

`chip-tool onoff on <target node ID> 1`

When the WoM device receives a matching subscription report, its LED turns on.
