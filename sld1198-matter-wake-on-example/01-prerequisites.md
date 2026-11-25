# Wake on Matter Prerequisites

Before you start, obtain the hardware and install the software described in the [Overview](/matter/{build-docspace-version}/matter-overview). You'll also need the following items.

## Host Packages

On an Ubuntu-based host, install `net-tools`. This package provides the `ifconfig`, command required by `verify_install.sh`.

```sh
sudo apt-get install net-tools
```

## Host Services

Make sure the following Silicon Labs services are running on your host:

- `cpcd.service`: The [CPC daemon](https://docs.silabs.com/multiprotocol/latest/multiprotocol-solution-linux/building-cpcd-locally), which connects the network co-processor (NCP) to the host.
- `otbr-agent.service`: The [OpenThread Border Router agent](https://docs.silabs.com/multiprotocol/latest/multiprotocol-solution-linux/building-otbr-locally).
- Bluetooth [HCI bridge](https://docs.silabs.com/multiprotocol/latest/multiprotocol-solution-linux/building-bluetooth-host-locally) (optional).

You also need a committed, active OpenThread dataset. If your host doesn't have one, create it by running the following commands:

```sh
sudo ot-ctl dataset init new
sudo ot-ctl dataset commit active
```

## Matter Tools and Devices
Make sure you have the following tools and devices:
- `chip-tool` built from the `connectedhomeip` tree and available on your `PATH`. For more information, see [Building the chip-tool](/matter/{build-docspace-version}/matter-wifi-getting-started-example/build-chip-tool)..
- `mmic_host` available on PATH. `PATH`. For more information, see [Building mmic_host](./02-build-and-flash.md#building-mmic_host).
- A device flashed with the Wake on Matter example and connected through the running `cpcd` instance.
- A second Matter accessory, such as the `lighting-app`, in commissioning mode (advertising over BLE). The accessory must accept the standard test setup PIN code `20202021` and discriminator `3840`.

## Verify the Installation

Run `scripts/verify_install.sh` to verify the host setup. The script checks that:

- `cpcd.service` and `otbr-agent.service` are installed and running.
- The `wpan0` interface is up. If `wpan0` is missing but an active OT dataset exists, the script attempts to bring up the interface using `ot-ctl`.

```sh
./scripts/verify_install.sh
```
