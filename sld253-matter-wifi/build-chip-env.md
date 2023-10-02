# Building the chip-tool

## Build Environment for Linux

This section will go through the steps required to build the chip-tool for Linux.

**Do not execute any commands on this page as ROOT (no _su_ required), unless specified**

### Prepare Linux Packages

Update the latest packages by typing following commands in terminal:

```shell
$ sudo apt update
$ sudo apt install
```

### Prerequisites for Matter (CHIP) project on Linux

#### 1. Installing packages on Ubuntu Laptop/PC

- Open the Linux terminal from Start menu
- Install required packages on Ubuntu Laptop/PC using the following commands:

    ```shell
    $ sudo apt install git gcc g++ pkg-config libssl-dev libdbus-1-dev
    libglib2.0-dev libavahi-client-dev ninja-build python3-venv python3-dev python3-pip unzip libgirepository1.0-dev libcairo2-dev libreadline-dev
    ```

#### 2. Building the chip-tool Environment

- To build chip-tool environment, follow below steps for the Software setup and Compiling chip-tool:

##### Software Setup

If you have not downloaded or cloned this repository, you can run the following
commands on a Linux terminal running on either Linux machine, WSL or Virtual
Machine to clone the repository and run bootstrap to prepare to build the sample
application images.

1. To download the [SiliconLabs Matter codebase](https://github.com/SiliconLabs/matter.git) run the following commands.

    ```shell
     $ git clone https://github.com/SiliconLabs/matter.git
    ```

2. Bootstrapping:

    ```shell
    $ cd matter
    $ ./scripts/checkout_submodules.py --shallow --recursive --platform efr32
    $ . scripts/bootstrap.sh
    # Create a directory where binaries will be updated/compiled called `out`
    $ mkdir out
    ```

##### Compiling the chip-tool

In order to control the Wi-Fi Matter Accessory Device you will have to compile
and run the chip-tool on either a Linux, Mac or Raspberry Pi. The chip-tool builds
faster on the Mac and Linux machines so that is recommended, but if you have
access to a Raspberry Pi that will work as well.

1. Build the chip-tool

    ```shell
    $ ./scripts/examples/gn_build_example.sh examples/chip-tool out/standalone
    ```

This will build chip-tool in `out/standalone`.
