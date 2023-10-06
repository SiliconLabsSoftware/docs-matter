# Build Procedure For Wi-Fi Direct Internet Connectivity (DIC)

The following components are common for all apps and should be modified in the corresponding app specific .slcp file.

## Add the DIC Component

To add DIC Component, modify corresponding app specific .slcp file.

```shell
  - id: matter_dic
    from: matter
```
## Add the DIC AWS OTA Component
To add DIC AWS OTA Component, modify corresponding app specific .slcp file.

```shell
  - id: aws_ota_wifi_dic
    from: matter
```
Note:- Building with aws_ota_wifi_dic component enables matter_dic component by default.

## App-Specific Changes

Replace the config_file, include and source in the .slcp file of the application from the path **matter/slc/sample-app/lighting-app/efr32/**.

### Enable DIC for Lighting App

In lighting-app-rs911x.slcp for rs9116 or lighting-app-wf200.slcp for wf200, replace with below changes:

```shell
config_file:
  - path: ../../../../examples/lighting-app/silabs/efr32/data_model/lighting-wifi-app.zap
    directory: common


include:
  - path: ../../../../examples/lighting-app/silabs/efr32/include
    file_list:
      - path: AppConfig.h
      - path: AppEvent.h
      - path: AppTask.h
      - path: CHIPProjectConfig.h
      - path: LightingManager.h
    directory: include
  - path: ../../../../silabs_examples/DIC_Examples
    file_list:
      - path: DIC_EventHandler.h
    directory: DIC_Examples

source:
  - path: ../../../../silabs_examples/DIC_Examples/DIC_lighting-app/efr32/src/AppTask.cpp
    directory: src
  - path: ../../../../examples/lighting-app/silabs/efr32/src/LightingManager.cpp
    directory: src
  - path: ../../../../examples/lighting-app/silabs/efr32/src/main.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_lighting-app/ZclCallbacks.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_EventHandler.cpp
    directory: DIC_Examples
```
In lighting-app-917-soc.slcp for Siwx917 SoC(dual flash) or lighting-app-917-soc-common.slcp for Siwx917 SoC(common flash), replace with below changes:

```shell
config_file:
  - path: ../../../../examples/lighting-app/silabs/SiWx917/data_model/lighting-wifi-app.zap
    directory: common

include:
  - path: ../../../../examples/lighting-app/silabs/SiWx917/include
    file_list:
      - path: AppConfig.h
      - path: AppEvent.h
      - path: AppTask.h
      - path: CHIPProjectConfig.h
      - path: LightingManager.h
    directory: include
  - path: ../../../../silabs_examples/DIC_Examples
    file_list:
      - path: DIC_EventHandler.h
    directory: DIC_Examples

source:
  - path: ../../../../silabs_examples/DIC_Examples/DIC_lighting-app/SiWx917/src/AppTask.cpp
    directory: src
  - path: ../../../../examples/lighting-app/silabs/SiWx917/src/LightingManager.cpp
    directory: src
  - path: ../../../../examples/lighting-app/silabs/SiWx917/src/main.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_lighting-app/ZclCallbacks.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_EventHandler.cpp
    directory: DIC_Examples
```

### Enable DIC for Lock App

In lock-app-rs911x.slcp for rs9116 or lock-app-wf200.slcp for wf200, replace with below changes:

```shell
config_file:
  - path: ../../../../examples/lock-app/lock-common/lock-app.zap
    directory: common

include:
  - path: ../../../../examples/lock-app/silabs/efr32/include
    file_list:
      - path: AppConfig.h
      - path: AppEvent.h
      - path: AppTask.h
      - path: LockManager.h
      - path: CHIPProjectConfig.h
      - path: EventHandlerLibShell.h
        condition: [matter_shell]
    directory: include
  - path: ../../../../silabs_examples/DIC_Examples
    file_list:
      - path: DIC_EventHandler.h
    directory: DIC_Examples

source:
  - path: ../../../../silabs_examples/DIC_Examples/DIC_lock-app/efr32/src/AppTask.cpp
    directory: src
  - path: ../../../../examples/lock-app/silabs/efr32/src/LockManager.cpp
    directory: src
  - path: ../../../../examples/lock-app/silabs/efr32/src/main.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_lock-app/ZclCallbacks.cpp
    directory: src
  - path: ../../../../examples/lock-app/silabs/efr32/src/EventHandlerLibShell.cpp
    condition: [matter_shell]
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_EventHandler.cpp
    directory: DIC_Examples
```
In lock-app-917-soc.slcp for Siwx917 SoC(dual flash) or lock-app-917-soc-common.slcp for Siwx917 SoC(common flash), replace with below changes:


```shell
config_file:
  - path: ../../../../examples/lock-app/lock-common/lock-app.zap
    directory: common

include:
  - path: ../../../../examples/lock-app/silabs/SiWx917/include
    file_list:
      - path: AppConfig.h
      - path: AppEvent.h
      - path: AppTask.h
      - path: LockManager.h
      - path: CHIPProjectConfig.h
      - path: EventHandlerLibShell.h
        condition: [matter_shell]
    directory: include
  - path: ../../../../silabs_examples/DIC_Examples
    file_list:
      - path: DIC_EventHandler.h
    directory: DIC_Examples

source:
  - path: ../../../../silabs_examples/DIC_Examples/DIC_lock-app/SiWx917/src/AppTask.cpp
    directory: src
  - path: ../../../../examples/lock-app/silabs/SiWx917/src/LockManager.cpp
    directory: src
  - path: ../../../../examples/lock-app/silabs/SiWx917/src/main.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_lock-app/ZclCallbacks.cpp
    directory: src
  - path: ../../../../examples/lock-app/silabs/SiWx917/src/EventHandlerLibShell.cpp
    condition: [matter_shell]
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_EventHandler.cpp
    directory: DIC_Examples
```


### Enable DIC for Window App

In window-app-rs911x.slcp for rs9116 or window-app-wf200.slcp for wf200, replace with below changes:

```shell
config_file:
  - path: ../../../../examples/window-app/common/window-app.zap
    directory: common

include:
  - path: ../../../../examples/window-app/silabs/efr32/include
    file_list:
    - path: AppConfig.h
    - path: CHIPProjectConfig.h
    - path: WindowAppImpl.h
    directory: include

  - path: ../../../../examples/window-app/common/include
    file_list:
    - path: WindowApp.h
    directory: include
  - path: ../../../../silabs_examples/DIC_Examples
    file_list:
      - path: DIC_EventHandler.h
    directory: DIC_Examples

source:
  - path: ../../../../silabs_examples/DIC_Examples/DIC_window-app/efr32/src/WindowAppImpl.cpp
    directory: src
  - path: ../../../../examples/window-app/silabs/efr32/src/main.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_window-app/common/src/WindowApp.cpp
    directory: src
  - path: ../../../../examples/window-app/common/src/ZclCallbacks.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_EventHandler.cpp
    directory: DIC_Examples
```
In window-app-917-soc.slcp for Siwx917 SoC(dual flash) or lock-app-917-soc-common.slcp for Siwx917 SoC(common flash), replace with below changes:

```shell
config_file:
  - path: ../../../../examples/window-app/common/window-app.zap
    directory: common

include:
  - path: ../../../../examples/window-app/silabs/SiWx917/include
    file_list:
    - path: AppConfig.h
    - path: CHIPProjectConfig.h
    - path: WindowAppImpl.h
    directory: include

  - path: ../../../../examples/window-app/common/include
    file_list:
    - path: WindowApp.h
    directory: include
  - path: ../../../../silabs_examples/DIC_Examples
    file_list:
      - path: DIC_EventHandler.h
    directory: DIC_Examples

source:
  - path: ../../../../silabs_examples/DIC_Examples/DIC_window-app/SiWx917/src/WindowAppImpl.cpp
    directory: src
  - path: ../../../../examples/window-app/silabs/SiWx917/src/main.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_window-app/common/src/WindowApp.cpp
    directory: src
  - path: ../../../../examples/window-app/common/src/ZclCallbacks.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_EventHandler.cpp
    directory: DIC_Examples
```

### Enable DIC for Thermostat App

In thermostat-rs911x.slcp for rs9116
or thermostat-wf200.slcp for wf200, replace with below changes:

```shell
config_file:
  - path: ../../../../examples/thermostat/thermostat-common/thermostat.zap
    directory: common

include:
  - path: ../../../../examples/thermostat/silabs/efr32/include
    file_list:
      - path: AppConfig.h
      - path: AppEvent.h
      - path: AppTask.h
      - path: SensorManager.h
      - path: TemperatureManager.h
      - path: CHIPProjectConfig.h
  - path: ../../../../silabs_examples/DIC_Examples
    file_list:
      - path: DIC_EventHandler.h
    directory: DIC_Examples

source:
  - path: ../../../../silabs_examples/DIC_Examples/DIC_thermostat/efr32/src/AppTask.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_thermostat/efr32/src/TemperatureManager.cpp
    directory: src
  - path: ../../../../examples/thermostat/silabs/efr32/src/main.cpp
    directory: src
  - path: ../../../../examples/thermostat/silabs/efr32/src/ZclCallbacks.cpp
    directory: src
  - path: ../../../../examples/thermostat/silabs/efr32/src/SensorManager.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_EventHandler.cpp
    directory: DIC_Examples
```

### Enable DIC for onoff-plug-app

In onoff-plug-app-rs911x.slcp for rs9116
or onoff-plug-app-wf200.slcp for wf200, replace with below changes:

```shell
config_file:
  - path: ../../../../silabs_examples/onoff-plug-app/onoff-plug-common/onoff-plug-app.zap
    directory: common

include:
  - path: ../../../../silabs_examples/onoff-plug-app/efr32/include
    file_list:
      - path: AppConfig.h
      - path: AppEvent.h
      - path: AppTask.h
      - path: CHIPProjectConfig.h
      - path: OnOffPlugManager.h
    directory: include
  - path: ../../../../silabs_examples/DIC_Examples
    file_list:
      - path: DIC_EventHandler.h
    directory: DIC_Examples
    
source:
  - path: ../../../../silabs_examples/DIC_Examples/DIC_onoff-plug-app/efr32/src/AppTask.cpp
    directory: src
  - path: ../../../../silabs_examples/onoff-plug-app/efr32/src/main.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_onoff-plug-app/ZclCallbacks.cpp
    directory: src
  - path: ../../../../silabs_examples/onoff-plug-app/efr32/src/OnOffPlugManager.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_EventHandler.cpp
    directory: DIC_Examples
```

In onoff-plug-app-917-soc.slcp for Siwx917 SoC(dual flash) or lock-app-917-soc-common.slcp for Siwx917 SoC(common flash), replace with below changes:

```shell
config_file:
  - path: ../../../../silabs_examples/onoff-plug-app/onoff-plug-common/onoff-plug-app.zap
    directory: common

include:
  - path: ../../../../silabs_examples/onoff-plug-app/SiWx917/include
    file_list:
      - path: AppConfig.h
      - path: AppEvent.h
      - path: AppTask.h
      - path: CHIPProjectConfig.h
      - path: OnOffPlugManager.h
    directory: include
  - path: ../../../../silabs_examples/DIC_Examples
    file_list:
      - path: DIC_EventHandler.h
    directory: DIC_Examples
    
source:
  - path: ../../../../silabs_examples/DIC_Examples/DIC_onoff-plug-app/SiWx917/src/AppTask.cpp
    directory: src
  - path: ../../../../silabs_examples/onoff-plug-app/SiWx917/src/main.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_onoff-plug-app/ZclCallbacks.cpp
    directory: src
  - path: ../../../../silabs_examples/onoff-plug-app/SiWx917/src/OnOffPlugManager.cpp
    directory: src
  - path: ../../../../silabs_examples/DIC_Examples/DIC_EventHandler.cpp
    directory: DIC_Examples
```

## Compile Using New/Different Certificates

   - Two devices should not use the same `DIC_CLIENT_ID`. To use a different Client ID for your second connection do the following:
   - If using AWS, Change the following file `matter_extension/examples/platform/silabs/DIC/matter_abs_interface/src/dic_nvm_cert.cpp` under `#if USE_AWS`
        *  Use device_certificate and device_key with your device cert and device key.
        *  Use `DIC_CLIENT_ID` macro value with your Client ID in `matter_extension/examples/platform/silabs/DIC/matter_abs_interface/inc/dic_config.h`
   - The preferred certificate type to use in the application is ECDSA.
   - If using mosquitto, change the following file `matter_extension/examples/platform/silabs/DIC/matter_abs_interface/src/dic_nvm_cert.cpp` enable `USE_MOSQUITTO` and disable `USE_AWS`. 
   - Under `#if USE_MOSQUITTO`
        * Use ca_certificate, device_certificate and device_key with your ca_certificate, device cert and device key.
        * Use `DIC_CLIENT_ID` macro value with your Client ID.
   - The preferred certificate type to use in the application is ECDSA.