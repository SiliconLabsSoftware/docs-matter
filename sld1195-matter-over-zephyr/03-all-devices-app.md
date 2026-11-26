# All-Devices Application

The All-Devices application is a Matter example for Zephyr. You can include one or more device types, which you select at build time. The default device type is an on/off light.

The application uses code-driven clusters. C++ code defines the endpoints, clusters, and device types instead of a ZAP configuration file. You do not need to run ZAP to configure the application.

## Copy the Application

Complete [Set up the Zephyr workspace](02-setup-zephyr.md). The following commands use `~/workspace` as the West workspace.

Copy the application to a separate directory to customize it without modifying the Matter SDK:

```sh
cd ~/workspace
mkdir -p applications/all-devices-app
cp -r modules/lib/matter/examples/all-devices-app/zephyr applications/all-devices-app/
```

Keep the `zephyr` directory name because the application's sysbuild configuration uses it as the image name. The copied application continues to use the shared device and cluster implementations in `modules/lib/matter`.

## Build and Flash

Build the application for the EFR32xG26 Radio Board BRD4118A:

```sh
west build -p always -b xg26_rb4118a --sysbuild \
	applications/all-devices-app/zephyr -d build/all-devices-app
```

Sysbuild builds MCUboot and the application. Use a board with a matching application overlay and bootloader configuration. For more information, see [Supported hardware](01-introduction.md#supported-hardware).

Connect the board, and then flash the images:

```sh
west flash -d build/all-devices-app
```

## Select Device Types

Open the application's text-based configuration interface from its image build directory:

```sh
west build -d build/all-devices-app/zephyr -t menuconfig
```

Under **Matter device types**, select the required device types, save your selections, and exit. Rebuild without `-p always` to preserve these settings:

```sh
west build -d build/all-devices-app
```

Menuconfig changes apply only to the current build directory. To preserve these settings for a clean build, add the corresponding options to `applications/all-devices-app/zephyr/prj.conf`. For example:

A single device type:

```ini
CONFIG_ALL_DEVICES_DEVICE_DISHWASHER=y
```

Multiple device types:

```ini
CONFIG_ALL_DEVICES_DEVICE_ON_OFF_LIGHT=y
CONFIG_ALL_DEVICES_DEVICE_OCCUPANCY_SENSOR=y
```

Select only the device types you need to limit RAM and flash usage. If you do not select any device types, all types are enabled. If you set the CMake option `ALL_DEVICES_ENABLED_DEVICES`, it takes precedence over the Kconfig selections.

## Customize Initialization

`AppTaskBase<Derived>` uses the Curiously Recurring Template Pattern (CRTP). It calls initialization steps through the final application type. A derived class can replace an initialization step by declaring a method with the same name or extend it by calling the base implementation first.

Set `APP_TASK_IMPL_HEADER` to a header that defines the final `chip::app::AllDevices::AppTask` class. This lets you customize initialization without modifying the generic application task.

By default, the Silicon Labs SDK selects `silabs/SilabsAppTask.h`. Its `SilabsAppTask` layer replaces `InitCredentials()` to install providers for device information, commissioning data, and attestation credentials.

The application uses example credentials for development by default. To use provisioned factory data, add the following option to `applications/all-devices-app/zephyr/prj.conf` and rebuild:

```ini
CONFIG_CHIP_FACTORY_DATA=y
```

Provision the device before running the application with this configuration. See [Matter provisioning](../sld5257-matter-provisioning/matter-provisioning.md#zephyr) for the workflow. Do not use example credentials in production.
