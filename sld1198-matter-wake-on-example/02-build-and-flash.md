# Building and Flashing the Wake on Matter Example

## Building the Device Application

The Wake on Matter application supports only the SLC toolchain. Use one of the following methods to build the application:

- Install the SLC toolchain using the [Silicon Labs Tool (SLT)](https://www.silabs.com/software-and-tools/simplicity-studio/silicon-labs-tool?tab=overview), and then build the application from the command line. For more information, see [Matter SLC CLI](/matter/{build-docspace-version}/matter-overview-guides/matter-slc-cli).
- Build the application in [Simplicity Studio](https://www.silabs.com/software-and-tools/simplicity-studio?tab=overview). For more information, see [Using Simplicity Studio](/matter/{build-docspace-version}/matter-references/using-studio).

To flash the resulting image to your device, see [Flashing a Silicon Labs Device](/matter/{build-docspace-version}/matter-references/flash-silabs-device).

After flashing, connect the device to your Linux host and verify that `cpcd` detects it.

## View Log Output

This application outputs logs only through the [Segger RTT interface](https://www.segger.com/products/debug-probes/j-link/tools/rtt-viewer/). Use J-Link RTT Viewer or another RTT client to view the device logs.

## Build mmic_host

`mmic_host` is a host-side command-line interface (CLI) tool that controls the network co-processor (NCP). Use it to commission the device, query its state, and establish subscriptions.
The source files are in third_party/matter_sdk/examples/platform/silabs/mmic/.
If `cpcd` is already bridging the device to the host, use the recommended CPC transport:

```sh
cd third_party/matter_sdk/examples/platform/silabs/mmic
cmake -S . -B build -DMMIC_USE_CPC=ON
cmake --build build
```

The build generates the `build/mmic_host` executable. Add it to your `PATH`.

Alternatively, set `MMIC_HOST=/full/path/to/mmic_host` to specify the executable's location for the validation script.

For all available build options, see `third_party/matter_sdk/examples/platform/silabs/mmic/README.md`. These options include compiler selection, nonstandard libcpc locations, and one-shot or interactive mode.
