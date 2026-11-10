# Configuring Wake on Matter

In this example, the Wake on Matter (WoM) device subscribes to attributes on another Matter device through the NCP attached to the host (for example, a Raspberry Pi). When a subscription report matches a configured wake-up trigger, the device wakes the host.

## Step 1: Commission the WoM Device

Commission the Wake on Matter device into a Matter over Thread network. You can do this from the host with `mmic_host`:

```sh
mmic_host commission <woM node ID>
mmic_host matter_state    # shows the new node ID
```

## Step 2: Grant ACL Access on the Target Node

On the target node, give the WoM device permission to open a CASE session and subscribe:

```sh
chip-tool accesscontrol write acl '[{"fabricIndex": 1, "privilege": 1, "authMode": 2, "subjects": [<woM node ID>], "targets": null}]' <target node ID> 0
```

> **Important:** `write acl` replaces the full ACL list. It does not add an entry. If the target node already has ACL entries, include them in the same JSON array. Otherwise, you lose access to the node. For example, to keep the administrator entry for `chip-tool` (node ID `112233`):
>
> ```sh
> chip-tool accesscontrol write acl '[{"fabricIndex": 1, "privilege": 5, "authMode": 2, "subjects": [112233], "targets": null}, {"fabricIndex": 1, "privilege": 1, "authMode": 2, "subjects": [<woM node ID>], "targets": null}]' <target node ID> 0
> ```

## Step 3: Establish a Subscription

On the host, establish a subscription from the WoM device to the target node:

```sh
mmic_host establish_subscription <fabricIndex> <nodeId> <endpointId> <clusterId> <attributeId>
```

For example, to subscribe to the `OnOff` attribute of the `OnOff` cluster on endpoint `1` of node `1`:

```sh
mmic_host establish_subscription 1 1 1 0x0006 0x0000
```

## Step 4: Set Up a Wake-Up Trigger

Add a wake-up trigger. When the device receives a subscription report that matches the trigger, it turns on the LED.

```sh
addWakeUp <clusterId> <attributeId> <mode> <operand>
```

| Argument      | Description                                         |
| ------------- | --------------------------------------------------- |
| `clusterId`   | Cluster ID to match                                 |
| `attributeId` | Attribute ID to match                               |
| `mode`        | Match mode: `0` = Boolean, `1` = Bitmask, `2` = Equal |
| `operand`     | Value compared with the reported attribute value    |

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

Toggle the target device (for example, `chip-tool onoff on <target node ID> 1`). The LED on the Wake on Matter device turns on.
