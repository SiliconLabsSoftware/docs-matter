# Creating Matter Applications using SLC CLI

**Silicon Labs Configurator (SLC)**: SLC offers command-line access to application configuration and generation functions. [Software Project Generation and Configuration with SLC-CLI](https://docs.silabs.com/simplicity-studio-5-users-guide/latest/ss-5-users-guide-tools-slc-cli/) provides instructions on downloading and using the SLC-CLI tool.

This guide lists the steps to create and build a Silicon Labs Matter SLC project using SLC-CLI and `make`. These scripts are evaluation quality and have been verified to work on Ubuntu 22.04.3 LTS, MacOS Version 13.5.1, and Windows 10.

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
To use SiWx91x Wi-Fi applications, clone the WisConnect SDK inside the extension directory.

```C
git clone https://github.com/SiliconLabs/wiseconnect.git
```


Your path to the Matter extension and WisConnect extension should look like:

```C
<Path/To/Gsdk/Download>/extension/matter_extension
<Path/To/Gsdk/Download>/extension/wiseconnect
```

Install the following python packages:

```C
pip3 install dload
pip3 install python-dotenv  
```

Change directory to cloned extension directory and run the `sl_setup.py` script. This will install the ARM gcc toolchain, SLC-CLI, ZAP, Simplicity Commander, Ninja, and Java.

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

The `sl_setup_env.py` script creates an .env file to be used to set the environment variables needed for the installed tools, ARM toolchain, SLC-CLI, Java ZAP, Simplicity-commander, ninja, and Java.

It will also create `environment_variables_vscode.txt` this file can be referred to add environment variables for VS code based builds. 

The script will ask user permission to trust the gecko_sdk, matter_extension and wiseconnect . 

## Creating an Application Project

Run the `sl_create_new_app.py` script to create a BRD4161A project with name `MyNewApp` starting from the `lighting-app-thread.slcp` example application project file:

The script will ask user permission to trust the `gecko_sdk` and `matter_extension` before generating.

For Mac and Linux:

```C
python3 slc/sl_create_new_app.py MyNewApp slc/sample-app/lighting-app/efr32/lighting-app-thread.slcp brd4161a
```

For Windows:

```C
python slc\sl_create_new_app.py MyNewApp slc\sample-app\lighting-app\efr32\lighting-app-thread.slcp brd4161a
```

## Building an Application Project

After a project is created the `sl_build.py` script can be used to re-generate the `MyNewApp` project and build it:

For Mac and Linux:

```C
python3 slc/sl_build.py MyNewApp/lighting-app-thread.slcp brd4161a
```

For Windows:

```C
python slc\sl_build.py MyNewApp\lighting-app-thread.slcp brd4161a
```

Alternately, one can use SLC-CLI commands directly to generate the project and then use `make` to build it.

Windows users will need to install `make` in their system. You can use your own or follow these steps to get `make`.

1. Install the MSYS terminal, which provides a Unix-like environment on Windows.
2. Open the MSYS terminal and install `make` using the command `pacman -S make`.
3. Run command `where make`, copy the path, and add it to the PATH environment variable.
4. Restart your command line terminal and run `slc/sl_build.py` or run make directly. You might need to reboot.

Note: In rare cases, the build may fail due to missing files in the `zap-generated/` directory. The workaround is to delete the `.zap` folder in the home directory.

## Modifying an Application Project

The resulting user project can be modified like any other SLC project: software components can be added or removed by modifying the project's .slcp file, configuration can be applied by modifying the files in the `config` directory, the application logic can be managed through the files in the `src` directory. Various SLC-CLI commands can be used to examine, validate, or re-generate the project after a modification, see [Software Project Generation and Configuration with SLC-CLI](https://docs.silabs.com/simplicity-studio-5-users-guide/latest/ss-5-users-guide-tools-slc-cli/) for more information.

For modifying Matter endpoints and clusters invoke the ZAP tool passing to it the application's ZAP file:

```C
./scripts/tools/zap/run_zaptool.sh MyNewApp/config/common/lighting-thread-app.zap
```

##Edit and Build with Visual Studio Code 

Install "Simplicity Studio for VS Code" extension on VS code.

Add the POST_BUILD_EXE and NINJA_BUILD_EXE variables from the `slc\tools\environment_variables_vscode.txt` to the environment variables. 

Run the `sl_setup_env.py` and `sl_create_new_app.py` to setup and create a sample application, then load the application in VS code by following the "Adding a VS Code-Enabled Simplicity Studio Project to VS Code" section from [Simplicity Studio User Guide](https://docs.silabs.com/simplicity-studio-5-users-guide/latest/ss-5-users-guide-tools-slc-cli/)

User can make all the changes in source files and regenerate app using 'slc generate' commands.
