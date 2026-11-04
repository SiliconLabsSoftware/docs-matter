# Wake on Matter Prerequisites

Before you start, obtain the hardware and install the software described in the [Overview](/matter/{build-docspace-version}/matter-overview). You also need the items below.

## Host Packages

On an Ubuntu-based host, install `net-tools`. It provides `ifconfig`, which `verify_install.sh` requires.

```sh
sudo apt-get install net-tools
```

## Host Services

The following Silicon Labs services must run on the host:

- `cpcd.service`: the [CPC daemon](https://docs.silabs.com/multiprotocol/latest/multiprotocol-solution-linux/building-cpcd-locally), which bridges the NCP to the host.
- `otbr-agent.service`: the [OpenThread Border Router agent](https://docs.silabs.com/multiprotocol/latest/multiprotocol-solution-linux/building-otbr-locally).
- Bluetooth [HCI bridge](https://docs.silabs.com/multiprotocol/latest/multiprotocol-solution-linux/building-bluetooth-host-locally) (optional).

You also need a committed active OpenThread dataset. If the host does not have one, create it:

```sh
sudo ot-ctl dataset init new
sudo ot-ctl dataset commit active
```

## Matter Tools and Devices

- `chip-tool` on your `PATH`, built from the `connectedhomeip` tree. See [Building the chip-tool](/matter/{build-docspace-version}/matter-wifi-getting-started-example/build-chip-tool).
- `mmic_host` on your `PATH`. See [Building mmic_host](./02-build-and-flash.md#building-mmic_host).
- A device flashed with the Wake on Matter example and connected through the running `cpcd` instance.
- A second Matter accessory, such as the `lighting-app`, in commissioning mode (advertising over BLE). It must accept the standard test setup PIN code `20202021` and discriminator `3840`.

## Verifying the Installation

Run `scripts/verify_install.sh` to check the host setup. The script checks that:

- `cpcd.service` and `otbr-agent.service` are present and running.
- The `wpan0` interface is up. If `wpan0` is missing but an active OT dataset exists, the script tries to bring it up with `ot-ctl`.

```sh
./scripts/verify_install.sh
```
