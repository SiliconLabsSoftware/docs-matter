# Creating Matter Applications using SLC CLI

The Silicon Labs Configurator (SLC) defines a way of creating and configuring embedded software projects for Silicon Labs IoT devices. The SLC Command Line Interface (SLC-CLI) tool resolves project and component dependencies and generates a project for a specified embedded target and build system (for example, GNU tools via a Makefile). See _UG520: Software Project Generation and Configuration with SLC-CLI_ for a complete description.

This guide lists the steps that can be followed to create and build a Silicon Labs Matter SLC project using SLC-CLI and `make`. These scripts are evaluation quality and have been verified to work on Ubuntu 22.04.3 LTS and MacOS Version 13.5.1, Windows support will come in the future releases.

## Setting up the Environment

Clone Gecko SDK:

```C
git clone https://github.com/SiliconLabs/gecko_sdk.git
```

Create a directory named `extension` inside the Gecko SDK directory.

Clone the  Matter GSDK Extension inside the `extension` directory:

```C
git clone https://github.com/SiliconLabs/matter_extension.git
```

Your path to the Matter extension should look like

```C
<Path/To/Gsdk/Download>/extension/matter_extension
```

Install the following python packages:

```C
pip3 install dload
```

Export the path of your GSDK download to the environment variable `GSDK_ROOT`. Then cd to cloned extension directory and run the `sl_setup.py` script. This will install the ARM gcc toolchain, SLC-CLI, ZAP and Java.

```C
export GSDK_ROOT=Path/To/Gsdk/Download
cd extension/matter_extension
python3 slc/sl_setup_env.py
```

The sl_setup_env.py script creates a shell script script that can be used to set the environment variables needed for the installed tools, ARM toolchain, SLC-CLI, Java and ZAP.

```C
source slc/tools/sl_env_vars.sh
```

## Creating an Application Project

Run the `sl_create_new_app.py` script to create a BRD4161A project with name `MyNewApp` starting from the `lighting-app-thread.slcp` example application project file:

```C
python3 slc/sl_create_new_app.py MyNewApp slc/sample-app/lighting-app/efr32/lighting-app-thread.slcp brd4161a
```

## Building an Application Project

After a project is created the `sl_build.py` script can be used to re-generate the `MyNewApp` project and build it:

```C
python3 slc/sl_build.py MyNewApp/lighting-app-thread.slcp brd4161a
```

Alternately, one can use SLC-CLI commands directly to generate the project and then use `make` to build it.

## Modifying an Application Project

The resulting user project can be modified like any other SLC project: software components can be added or removed by modifying the project's .slcp file, configuration can be applied by modifying the files in the `config` directory, the application logic can be managed through the files in the `src` directory. Various SLC-CLI commands can be used to examine, validate or re-generate the project after a modification, see _UG520: Software Project Generation and Configuration with SLC-CLI_ for more info.

For modifying Matter endpoints and clusters invoke the ZAP tool passing to it the application's ZAP file:

```C
./scripts/tools/zap/run_zaptool.sh MyNewApp/config/common/lighting-thread-app.zap
```
