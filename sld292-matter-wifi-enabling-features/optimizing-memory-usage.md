# Optimizing Memory Usage

This page provides information on optimizing memory usage for Silicon Labs devices.

## Memory Reports for Silicon Labs Devices

Memory usage information is provided in the reports below:

 - Memory usage of silicon labs devices can be checked at

   ![Memory Usage Report](./images/memory-usage-report.png)

 - Detailed Memory Footprint can be checked at

   ![Memory FootPrint](./images/memory-footprint-report.png)

## How to Optimize Memory

To optimize an application's memory footprint, check the following:

1. Analyze and reduce stack usage of the application wherever possible.
2. Disable any included debug modules.
3. Turn off unused peripherals, features and functions.

### Disabling Debug Logging

Memory can be optimized by disabling debug logs. The **matter_no_debug** component disables the following from the project.
  - Disables Silabs specific logging used in Matter
  - Disables Hard Fault logs
  - Keeps Log Level to None

To add **matter_no_debug** Component, modify the corresponding app-specific **.slcp** project file.

 ```shell
  - id: matter_no_debug  
    from: matter
```
