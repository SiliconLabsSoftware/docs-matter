# Optimizing Memory Usage
This document provides information on Optimizing Memory Usage for the Silicon Labs Devices.

## Memory Reports for Silicon Labs Devices
Below reports provides memory usage information:
 - Memory usage of silicon labs devices can be chekced at

   ![Memory Usage Report](./images/memory-usage-report.png)

 - Detailed Memory Footprint can be checked at.

   ![Memory FootPrint](./images/memory-footprint-report.png)

## How to Optimize Memory
To optimize memory footprint, ensure application is optimized with the following:
  1. Analyze and reduce stack usage of the application where ever possible.
  2. Disabling the debugging modules.
  3. Turn off unused peripherals, features and functionalities.
   
### Disabling debug Logging
- Memory can be optimizied by disabling debug logs. 
- **matter_no_debug** component will disable the below from the project.
        - Disables Silabs specific logging used in matter
        - Disables Hard Fault logs
        - Keeping Log Level to None
- To add **matter_no_debug** Component, modify corresponding app specific **.slcp** project file.
 ```shell     
  - id: matter_no_debug  
    from: matter
```