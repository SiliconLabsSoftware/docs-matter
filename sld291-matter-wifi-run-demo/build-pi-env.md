# Using the Pre-Built Raspberry Pi "Matter Hub" Image

When using a Raspberry Pi as a controller in your Matter network you have two options
  - Building the Raspberry Pi Environment "from scratch" using a Raspberry Pi 4
  - Using the Silicon Labs Pre-Built Raspberry Pi image available on the [Matter Artifacts page](/matter/<docspace-docleaf-version>/matter-prerequisites/matter-artifacts) page.
## Building Environment using Raspberry Pi 4

### To flash the Ubuntu OS onto the SD card:

1. Insert the flashed SD card (directly or using a card reader) into the
   laptop/PC that will run the Raspberry Pi Imager tool.
2. Launch Raspberry Pi 4 Imager.
3. Flash the Pi image using any one of the following procedure: 
   
   - Click 'Choose OS' --> 'Other General-purpose OS' --> 'Ubuntu' --> 'Ubuntu
   xx.xx 64-bit server OS'
   Note: Flash the latest version of Ubnutu Server (64-bit server OS for arm64 architecture)
   
   - Download the Matter Hub Raspberry Pi Image provided on the [Matter Artifacts page](/matter/<docspace-docleaf-version>/matter-prerequisites/matter-artifacts), then click 'Choose OS' --> 'Use custom' --> select the Matter Hub Raspberry Pi Image which you downloaded.
   
4. Click 'Storage' and select the 'SD card detect'.
5. This Raspberry Pi 4's console can be accessed in   multiple ways.
    In [this guide](https://www.raspberrypi.com/documentation/computers/remote-access.html)
    Raspberry Pi 4 is being accessed using Putty.
6. Enter the details like User name, Password, SSID and its password to connect
   to network. Click 'Save'.
7. Click 'Write' and then 'Yes' when you are asked for permission to erase data
   on the SD card. It will then start flashing the OS onto the SD card.
8. When it is done, click 'Continue'.
9. Remove the SD card from the reader and insert it into the Raspberry Pi as
   shown below:

![Inserting SD into Pi](images/sd-into-pi.png)

On powering up the board, the red and green lights should start blinking. 

### To start using the Raspberry Pi:

1. Power-up the RPi4B. Once it is booted up, check the Raspberry Pi's IP address. Refer to [Finding Raspberry Pi IP address](/matter/<docspace-docleaf-version>/matter-references/find-raspi) in the References chapter to get the IP address or enter the Hostname directly in PuTTY. 
2. Once you find the IP address, launch Putty, select `Session`, enter the IP
   address of the Raspberry Pi, and click `Open`
3. Enter the username and password given at the time of flashing and click
   `Enter` 
   
   Note: If username and password not provided while flashing then by default 
   Username: ubuntu
   Password: ubuntu

4. Switch to root mode and navigate to path "/home/ubuntu/connectedhomeip/out/standalone" to find the chip-tool.
   On the pre-built Matter Hub image, the chip-tool will be ready and working. Keep the PuTTY session open for the further steps.
   
5. If you are building the chip-tool from scratch, update the latest packages by running following commands in the terminal:
   ```shell
   $ sudo apt update 
   $ sudo apt install
   ```
6. Install required packages using the following commands:
    ```shell
   $ sudo apt-get install git gcc g++ pkg-config libssl-dev libdbus-1-dev libglib2.0-dev libavahi-client-dev ninja-build python3-venv python3-dev python3-pip unzip libgirepository1.0-dev libcairo2-dev libreadline-dev
   ```

   If you see any popups between installs, you can select 'Ok' or 'Continue'

## Build Environment

1. Installing prerequisites on Raspberry Pi 4
Follow the instructions in 
[the Project CHIP GitHub Site](https://github.com/project-chip/connectedhomeip/blob/master/docs/guides/BUILDING.md),
in the section "Installing prerequisites on Raspberry Pi
4".

2. To build environment follow the `Software setup` and `Compiling chip-tool` steps given in [Software setup](./../sld120-matter-wifi-getting-started/04-light-switch-step-by-step-example.md),

## Bluetooth Setup

Make sure Bluetooth LE (BLE) is up and running on Raspberry Pi. Raspberry Pi internally has
some issues with BLE that may cause it to crash. Because BLE is used for
commissioning on Matter, make sure BLE is running.

```shell
$ sudo systemctl status bluetooth.service
```

To stop BLE if it is already running:

```shell
$ sudo systemctl stop bluetooth.service
```

To restart the Bluetooth service, first enable it:

```shell
$ sudo systemctl enable bluetooth.service
```

When you check the status of the Bluetooth service, it will be inactive because
it has been enabled but not restarted:

```shell
$ sudo systemctl status bluetooth.service
```

Restart the service:

```shell
$ sudo systemctl restart bluetooth.service
```

Now the status of the service should be active and running:

```shell
$ sudo systemctl status bluetooth.service
```
