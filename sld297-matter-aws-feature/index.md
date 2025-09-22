# Matter + AWS Component

-   Matter + AWS is a silabs only feature to connect matter devices to
    proprietary cloud solutions(AWS) directly. As such, a Matter Wi-Fi device
    must support connecting locally on the Matter Fabric, via IPv6, and
    connecting to the Internet via IPv4.
-   Matter devices can be controlled by chip-tool or controller and the
    respective status of the attribute modified will be published to the cloud.
-   Remote user can install the cloud specific application to get the
    notification on the attribute status.

## Matter + AWS Feature Diagram

1. Below diagram gives end-to-end flow about Direct Internet Connectivity.

![Silicon Labs - Matter + AWS design](./images/matter-aws-flow.png)

## Prerequisites

### Hardware Requirements

For the list of hardware requirements for Matter + AWS feature , see the
official
[Silicon Labs Matter HW requirements](https://siliconlabs.github.io/matter/latest/general/HARDWARE_REQUIREMENTS.html)
documentation.

### Software Requirements

For the list of software requirements for Matter + AWS feature , see the
official
[Silicon Labs Matter Software requirements](https://siliconlabs.github.io/matter/latest/general/SOFTWARE_REQUIREMENTS.html)
documentation.

## End-to-End Set-up bring up

### Message Queuing Telemetry Transport (MQTT)

-   MQTT is an OASIS standard messaging protocol for the Internet of Things
    (IoT). It is designed as an extremely lightweight publish/subscribe
    messaging transport that is ideal for connecting remote devices with a small
    code footprint and minimal network bandwidth. Refer https://mqtt.org/ for
    more details

### Configuring the MQTT server

To set up and configure AWS for Matter + AWS support, see the following documentation:

- [AWS installation](./aws-configuration-registration.md)

### Remote User Setup (MQTT Explorer) (optional)

A remote user is used to check the state of a Matter device. In this context, MQTT explorer is used as a remote user. See [MQTT explorer setup and configuration](./mqtt-explorer-setup.md).

### Building Matter + AWS Application using Simplicity Studio

1. Follow instructions in [Build MATTER + AWS](./build-matter-aws.md) to enable the MATTER + AWS feature in code.


## End-to-End Test of Matter + AWS Application

User Setup (MQTT Explorer):

- Sharing status of device to cloud
  - The following diagram shows the end-to-end flow for sharing status from a Matter device to the Cloud.

![Silicon Labs - Matter + AWS design](images/dic-status-sharing.png)

  **Note**: For reference, Lighting App commands are given in the above image. Other application commands also can be passed.

- For the end-to-end commands to be executed from chip-tool, refer to [Running the Matter Demo Over Wi-Fi](/matter/{build-docspace-version}/matter-wifi-run-demo).
- Below are the application-specific attributes or states shared to the cloud:
  - For Lighting App, On/Off Attributes
  - For Lock App, lock/unlock Attributes
  - For Windows App, lift/tilt Attributes
  - For Thermostat App, SystemMode/CurrentTemp/LocalTemperature/OccupiedCoolingSetpoint/OccupiedHeatingSetpoint Attributes
  - For On/off Plug App, On/Off Attributes
  - Application status would be updated on the mqtt_explorer UI, as shown in below image.
  
      ![Matter + AWS status update](images/mqtt-explorer-4.png)

- Control of the device through cloud interface
  - The diagram below shows the end-to-end flow for control of the Matter device through a cloud interface.
  
      ![Silicon Labs - Matter + AWS design](images/dic-control-part.png)

    **Note**: For reference, Lighting App commands are shown in the above image. Similarly, other application commands also can be passed.

  - Make sure the Matter device is up and commissioned successfully. Refer to [Running the Matter Demo Over Wi-Fi](/matter/{build-docspace-version}/matter-wifi-run-demo).
  - For controlling the device, set topic name and the commands to be executed in the mqtt_explorer for the following applications.

```shell
    - Lighting App
      - Topic: command
        - Commands:
           - toggle
           - on
           - off
    - Onoff-plug App
      - Topic: command
        - Commands:
          - toggle
          - on
          - off
    - Lock App
      - Topic: command
        - Commands:
          - lock
          - unlock
    - Thermostat App
      - Topic: command
        - Commands:
          - SetMode/value(value need to provide 1,2,3,4 ex:SetMode/1)
          - Heating/value(value need to provide 2500,2600 ex:HeatingSetPoint/2500)
          - Cooling/value(value need to provide 2500,2600 ex:CoolingSetPoint/2500)
    - Window App
      - Topic: command
        - Commands:
          - Lift/value(value need to provide in range 1000 to 10000)
          - Tilt/value(value need to provide in range 1000 to 10000)
```

- Click **Publish** to execute the command.

![Silicon Labs - Matter + AWS design](images/control-device-through-cloud.png)
