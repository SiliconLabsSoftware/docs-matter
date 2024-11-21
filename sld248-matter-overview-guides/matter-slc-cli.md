# Creating Matter Applications using SLC CLI

**Silicon Labs Configurator (SLC)**: SLC offers command-line access to application configuration and generation functions. [Software Project Generation and Configuration with SLC-CLI](https://docs.silabs.com/simplicity-studio-5-users-guide/latest/ss-5-users-guide-tools-slc-cli/) provides instructions on downloading and using the SLC-CLI tool.

This guide lists the steps to create and build a Silicon Labs Matter SLC project using SLC-CLI and `make`. These scripts are evaluation quality and have been verified to work on Ubuntu 22.04.3 LTS, MacOS Version 13.5.1, and Windows 10.

## Setting up the Environment

Clone Simplicity SDK:

```C
https://github.com/SiliconLabsSoftware/matter_extension.git
```

Install the following python packages:

```C
pip3 install dload
pip3 install python-dotenv  
```

The `sl_setup_env.py` script creates an `.env` file which contains all the relevant virtual environment paths to be use by `sl_create_new_app.py` and `sl_build.py` scripts. The file is not meant to be used directly and is mentioned here only for reference.

It will also create `environment_variables_vscode.txt`. This file can be referenced to add environment variables for VS Code-based builds.
For Mac and Linux:

```C
cd extension/matter_extension
python3 slc/sl_setup_env.py
```

For Windows:

```C
cd extension\matter_extension
python slc\sl_setup_env.py
```
The `sl_setup_env.py` script syncs and checkouts the submodules and creates symlinks for matter_extension. Windows users may need to enable long paths in the system and run the terminal with admin privileges to create the symlinks. 

Users may enable long paths for git by running
```
git config --system core.longpaths true  
```

## Creating an Application Project

Run the `sl_create_new_app.py` script to create a BRD4187C project with name `MyNewApp` starting from the `lighting-app-thread.slcp` example or from the `lighting-app-thread-bootloader.slcw` [solution](../sld248-matter-overview-guides/matter-solutions.md) application project file:

Sample-App Example:
For Mac and Linux:

```C
python3 slc/sl_create_new_app.py MyNewApp slc/sample-app/lighting-app/efr32/lighting-app-thread.slcp brd4187c
```

For Windows:

```C
python slc\sl_create_new_app.py MyNewApp slc\sample-app\lighting-app\efr32\lighting-app-thread.slcp brd4187c
```

Solutions Examples:

For Mac and Linux:

```C
python3 slc/sl_create_new_app.py MyNewApp slc/solutions/lighting-app/series-2/lighting-app-thread-bootloader.slcw brd4187c
```

For Windows:

```C
python slc\sl_create_new_app.py MyNewApp slc\solutions\lighting-app\series-2\lighting-app-thread-bootloader.slcw brd4187c
```

## Building an Application Project

After a project is created the `sl_build.py` script can be used to re-generate the `MyNewApp` project and build it:

Sample-App Example:
For Mac and Linux:

```C
python3 slc/sl_build.py MyNewApp/lighting-app-thread.slcp brd4187c
```

For Windows:

```C
python slc\sl_build.py MyNewApp\lighting-app-thread.slcp brd4187c
```

Solutions Examples:

For Mac and Linux:

```C
python3 slc/sl_build.py MyNewApp/lighting-app-thread-bootloader.slcw brd4187c
```

For Windows:

```C
python slc\sl_build.py MyNewApp\lighting-app-thread-bootloader.slcw brd4187c
```

Alternately, one can use SLC-CLI commands directly to generate the project and then use `make` to build it.

Windows users will need to install `make` in their system. You can use your own or follow these steps to get `make`.

1. Install the MSYS terminal, which provides a Unix-like environment on Windows.
2. Open the MSYS terminal and install `make` using the command `pacman -S make`.
3. Run command `where make`, copy the path, and add it to the PATH environment variable.
4. Restart your command line terminal and run `slc/sl_build.py` or run make directly. You might need to reboot.

Note: In rare cases, the build may fail due to missing files in the `zap-generated/` directory. The workaround is to delete the `.zap` folder in the home directory.

## Modifying an Application Project

The resulting user project can be modified like any other SLC project. Software components can be added or removed by modifying the project's .slcp file, configuration can be applied by modifying the files in the `config` directory, the application logic can be managed through the files in the `src` directory. Various SLC-CLI commands can be used to examine, validate, or re-generate the project after a modification, see [Software Project Generation and Configuration with SLC-CLI](https://docs.silabs.com/simplicity-studio-5-users-guide/latest/ss-5-users-guide-tools-slc-cli/) for more information.

For modifying Matter endpoints and clusters invoke the ZAP tool passing to it the application's ZAP file:

```C
./scripts/tools/zap/run_zaptool.sh MyNewApp/config/common/lighting-thread-app.zap
```

## Edit and Build with Visual Studio Code

Install the "Simplicity Studio for VS Code" extension on VS code.

Add the POST_BUILD_EXE and NINJA_BUILD_EXE variables from the `slc\tools\environment_variables_vscode.txt` to the environment variables.

Run the `sl_setup_env.py` and `sl_create_new_app.py` to set up and create a sample application, then load the application in VS Code by following the "Adding a VS Code-Enabled Simplicity Studio Project to VS Code" section from [Simplicity Studio User Guide](https://docs.silabs.com/simplicity-studio-5-users-guide/latest/ss-5-users-guide-tools-slc-cli/).

You can make all the changes in source files and regenerate app using 'slc generate' commands.
