# Code Savings Guide for Building Matter Applications

* Remove unnecessary clusters from the zap configuration. Example applications have clusters enabled to support both Thread and WiFi transport layers such as the Diagnostics clusters. 

* Remove optional components in from the Matter Project in Studio that may not be needed for a certain application. For example, removing the components Matter Display and Matter QR Code Display will save flash by disabling the LCD screen. 
