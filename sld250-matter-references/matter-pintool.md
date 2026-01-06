# Using Simplicity Studio's Pintool and Project Configuration with Matter

At some point during product development you may need to move your project over to your custom hardware. In this case,
you will likely need to change the pinout and hardware configuration in the example project to reflect your own custom project. You can do this
with Simplicity Studio's Pintool starting from a blank C++ project.

## 1. Locate the board support files in the Matter repo

The pin and peripheral configuration for your example application is stored
within the Silicon Labs Matter support directory. For all the examples used in
the matter repository, the peripheral and pin configurations are stored at

`./third_party/silabs/matter_support/matter/efr32/<chip_family>/<board>/config`

When creating a configuration for a custom board do the following:

1. Create a Custom C++ project within Simplicity Studio.
2. Include your desired peripherals in the project.
3. Copy the generated output config files into a custom board support directory
   within the Matter repository.

## 2. Create a Sample "Empty C++ project" in Simplicity Studio

1. In Simplicity Studio, next to **Start a New Project**, click **all projects & demos** to start the project wizard. 
2. In the upper right, click **Select Device** to choose your development board, and in the dropdown, select the appropriate Simplicity SDK.
3. Scroll to the **Empty C++ Project** example, and click **Create**.
4. Click **Finish** to create your project.
   to start the project wizard. Choose your development board type via the `+ Select Device` button, and the
   latest Simplicity SDK you'll be working from

5. Select the `Empty C++ Project` example and click **Create**.

6. Select a compatible device then click **Next**.

7. Click **Finish** to create your project.

## 3. Customize your Components and Pin configuration in Simplicity Studio

Once you have your project created, you will see your project and project
configuration in Simplicity Studio's Project Configurator. For full documentation on the use of the Project Configurator and Pin Tool, see the [Simplicity Studio User's Guide](https://docs.silabs.com/ssv6ug/latest/ssv6-configure-project/pin-tool).
the use of the Project Configurator and Pin Tool are located here:
[Simplicity Studio User's Guide](https://docs.silabs.com/ssv6ug/latest/ssv6-configure-project/pin-tool)

## 4. Generate your Component and Pin Configuration in Simplicity Studio

When you save your project configuration, Simplicity Studio
saves all the generated header files out into a `config` directory in your
project. These are the files that make up the software component and pin tool
configuration for your device.

## 5. Move your pin configuration over to your Matter project

All of the header files in your `config` project directory constitute the
hardware configuration for your device. Copy these files 
into your Matter project so that they can be used in place of the ones provided
in the example.
