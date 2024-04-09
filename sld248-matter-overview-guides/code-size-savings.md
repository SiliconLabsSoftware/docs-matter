# Code Savings Guide for Building Matter Applications

Silicon Labs' Matter example applications come out of the box with various ease-of-life components allowing for a smoother development process (LCD functionality, debugging capability, Matter shell, etc). These components bring along with them some increase in the size of resulting application's image.

To reduce the total size of your application's image while still maintaining basic core Matter functionality, you can take a few steps:

1. Remove optional components in from the Matter Project in Studio that may not be needed for a certain application. For example, removing the components Matter Display and Matter QR Code Display will save flash by disabling the LCD screen.

2. Install the `matter_no_debug` and/or `matter_no_lcd_shell` components. This will automatically take care of removing these extra features (`matter_no_lcd_shell`) as well as implement the defines and configuration values (`matter_no_debug`) to achieve optimal image size reduction at the click of a button.

3. Remove clusters from the zap configuration. Example applications have clusters enabled to support both Thread and WiFi transport layers such as the Diagnostics clusters.
