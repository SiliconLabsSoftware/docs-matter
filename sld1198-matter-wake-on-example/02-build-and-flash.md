# Building and Flashing the Wake on Matter Example

## Building the Device Application

The Wake on Matter application supports only the SLC toolchain. Build it in one of these ways:

- Install the SLC toolchain with the [Silicon Labs Tool (SLT)](https://www.silabs.com/software-and-tools/simplicity-studio/silicon-labs-tool?tab=overview), then build from the command line. See [Matter SLC CLI](/matter/{build-docspace-version}/matter-overview-guides/matter-slc-cli).
- Build the application in [Simplicity Studio](https://www.silabs.com/software-and-tools/simplicity-studio?tab=overview). See [Using Simplicity Studio](/matter/{build-docspace-version}/matter-references/using-studio).

To flash the resulting image, see [Flashing a Silicon Labs Device](/matter/{build-docspace-version}/matter-references/flash-silabs-device).

After flashing, connect the device to the Linux host. Make sure `cpcd` detects it.

## Viewing Logging Output

This application outputs logs only through the [Segger RTT interface](https://www.segger.com/products/debug-probes/j-link/tools/rtt-viewer/). Use J-Link RTT Viewer, or another RTT client, to view device logs.

## Building mmic_host

`mmic_host` is the host-side CLI that controls the NCP. It can commission the device, query its state, and establish subscriptions. Its sources are in `third_party/matter_sdk/examples/platform/silabs/mmic/`.

If `cpcd` already bridges the device, use the CPC transport (recommended):

```sh
cd third_party/matter_sdk/examples/platform/silabs/mmic
cmake -S . -B build -DMMIC_USE_CPC=ON
cmake --build build
```

The build produces `build/mmic_host`. Add it to your `PATH`. As an alternative, point the validation script to it with `MMIC_HOST=/full/path/to/mmic_host`.

For all build options, see `third_party/matter_sdk/examples/platform/silabs/mmic/README.md`. Options include compiler selection, non-standard `libcpc` locations, and one-shot versus interactive mode.
