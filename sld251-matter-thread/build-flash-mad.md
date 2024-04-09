# How to Build and Flash the Matter Accessory Device (MAD)

The Matter Accessory Device, such as the lighting-app, is the actual Matter device that you will commission onto the Matter network and control using the chip-tool.

## Step 1: Get the Image File to Flash the MAD

We have provided two ways to get the required image to flash the MAD. You can use one of the following options:

1. Use the pre-built image file from either Simplicity Studio or Silicon Labs Matter GitHub.
2. Build the image file from Simplicity Studio or out of the Silicon Labs Matter GitHub `matter` repository.

### Using the Pre-Built Image File

Prebuilt image files are available both on GitHub and inside Simplicity Studio.

#### Simplicity Studio

To find the demos within Simplicity Studio, even if you do not have a device connected:

1. Go to the Launcher within Simplicity Studio, you can see the Launcher tab in the upper right hand corner
2. Under "Get Started" choose "All Products"
3. Choose a board to start with such as "BRD4186C Rev A01" and click "Start", this will bring up the launcher window for that part
4. In the top navigation choose "Example Projects & Demos"
5. In the left hand navigation choose "Matter" to show all the Matter demos.
6. The demos are marked as "demo" and allow you to "Run" them, Projects can be "Created"
7. Choose the demo you wish to use and click "Run" to flash it onto your board

#### Silicon Labs GitHub

If you are interested in using prebuilt image files from GitHub, all of the Matter Accessory Device image files are accessible through the [Matter Artifacts page](/matter/<docspace-docleaf-version>/matter-prerequisites/matter-artifacts). If you are using a pre-built image file, you can skip forward to Step #2: Flashing the MAD.

If you are coming from Simplicity Studio, you may have already installed the demo image in Simplicity Studio, in which case you can skip forward to the next step.

### Building the Matter Image File

There are two ways to build a Matter Accessory Device image file. You can build it using the Silicon Labs Matter GitHub Repo or you can build it using Simplicity Studio. The entire build process for Simplicity Studio is covered in the [Matter Over Thread Quick Start Guide](/matter/<docspace-docleaf-version>/matter-thread-getting-started/).

- [Build Using the Matter GitHub Repo](https://github.com/SiliconLabs/matter/blob/latest/examples/lighting-app/silabs/efr32/README.md)
- [Build Using Simplicity Studio](/matter/<docspace-docleaf-version>/matter-thread-getting-started/03-light-switch-step-by-step-example#creating-the-matter-accessory-devices-ma-ds)

## Step 2: Flash the Matter Accessory Device

For more information on how to flash your Silicon Labs development platform, see the following instructions: [How to Flash a Silicon Labs Device](/matter/<docspace-docleaf-version>/matter-references).

Once your Matter Accessory Device has been flashed, it should show a QR code on the LCD. If no QR Code is present, it may be that you need to add a bootloader to
your device. Bootloader images are provided on the [Matter Artifacts page](/matter/<docspace-docleaf-version>/matter-prerequisites/matter-artifacts).
