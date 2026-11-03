# All-Devices Application

The All-Devices application is a Matter example for Zephyr. It can include one or more device types, selected at build time. The default device type is an on/off light.

The application uses code-driven clusters. C++ code defines the endpoints, clusters, and device types instead of a ZAP configuration file. You do not need to run ZAP to configure this application.

## Copy the Application

Complete [Set Up the Zephyr Workspace](02-setup-zephyr.md) first. The commands below use `~/workspace` as the West workspace.

Copy the application to a separate directory so you can customize it without editing the Matter SDK:

```sh
cd ~/workspace
mkdir -p applications/all-devices-app
cp -r modules/lib/matter/examples/all-devices-app/zephyr applications/all-devices-app/
```

Keep the `zephyr` directory name: the application's sysbuild configuration uses it as the image name. The copied application still uses the shared device and cluster implementations in `modules/lib/matter`.

## Build and Flash

Build for the EFR32xG26 Radio Board BRD4118A:

```sh
west build -p always -b xg26_rb4118a --sysbuild \
	applications/all-devices-app/zephyr -d build/all-devices-app
```

Sysbuild builds MCUboot and the application. Use a board with a matching application overlay and bootloader configuration. See [Supported Hardware](01-introduction.md#supported-hardware).

Connect the board, then flash the images:

```sh
west flash -d build/all-devices-app
```

## Select Device Types

Open the application's text-based configuration interface from its image build directory:

```sh
west build -d build/all-devices-app/zephyr -t menuconfig
```

Under **Matter device types**, select the required types, save, and exit. Rebuild without `-p always` to keep these settings:

```sh
west build -d build/all-devices-app
```

Menuconfig changes apply to the current build directory. To preserve them for a clean build, add the corresponding options to `applications/all-devices-app/zephyr/prj.conf`. For example:

```ini
CONFIG_ALL_DEVICES_DEVICE_ON_OFF_LIGHT=y
CONFIG_ALL_DEVICES_DEVICE_OCCUPANCY_SENSOR=y
```

Select only the device types you need to limit RAM and flash use. Selecting no device types enables all types. If you set the CMake option `ALL_DEVICES_ENABLED_DEVICES`, it takes precedence over Kconfig selections.

## Customize Initialization

`AppTaskBase<Derived>` uses the Curiously Recurring Template Pattern (CRTP). It calls initialization steps through the final application type. A derived class can replace a step by declaring a method with the same name, or extend it by calling the base implementation first.

Set `APP_TASK_IMPL_HEADER` to a header that defines the final `chip::app::AllDevices::AppTask` class. This lets you customize initialization without changing the generic application task.

The Silicon Labs SDK selects `silabs/SilabsAppTask.h` by default. Its `SilabsAppTask` layer replaces `InitCredentials()` to install providers for device information, commissioning data, and attestation credentials.

By default, the application uses example credentials for development. To use provisioned factory data, add this option to `applications/all-devices-app/zephyr/prj.conf` and rebuild:

```ini
CONFIG_CHIP_FACTORY_DATA=y
```

Provision the device before running this configuration. See [Matter Provisioning](../sld5257-matter-provisioning/matter-provisioning.md#zephyr) for the workflow. Do not use example credentials in production.