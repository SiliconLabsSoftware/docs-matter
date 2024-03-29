# Build Procedure For Wi-Fi Direct Internet Connectivity (DIC)

The following components are common for all apps and should be modified in the corresponding app specific .slcp file.

## How to Add the DIC Component

To add DIC Component, modify corresponding app specific .slcp file.

```shell
  - id: matter_dic
    from: matter
```

## How to Add the DIC AWS OTA Component

To add DIC AWS OTA Component, modify corresponding app specific .slcp file.

```shell
  - id: aws_ota_wifi_dic
    from: matter
```

Note:- Building with aws_ota_wifi_dic component enables matter_dic component by default.

## Building DIC Application

- After Modification in **.slcp** Project file as above step, refresh the **matter-extension** in Simplicity Studio.

- Select **Preferences** in **Launcher** tab.

 ![Select Preferences](./images/select-preferences.png)

- Expand Simplicity Studio section and click on **SDKs** Tab.

 ![Select SDK](./images/select-studio-sdk-option.png)

- Expand **Gecko SDK** and click the **Refresh** button from side menu.

 ![Select Refresh](./images/select-refresh-option.png)

- Build the DIC application using Simplicity Studio
  - [Build EFx32 Application Using Studio](/matter/<docspace-docleaf-version>/matter-wifi-run-demo/build-efx32-application-using-studio)
  - [Build SOC Application Using Studio](/matter/<docspace-docleaf-version>/matter-wifi-run-demo/build-soc-application-using-studio)

## Compile Using New/Different Certificates

- Two devices should not use the same `DIC_CLIENT_ID`. To use a different Client ID for your second connection, do the following:
- If using AWS, change the following file `matter_extension/examples/platform/silabs/DIC/matter_abs_interface/src/dic_nvm_cert.cpp` under `#if USE_AWS`.
  - Use `DIC_SERVER_HOST` name with your Server host name.
    - For Example: a2m21kovu9tcsh-ats.iot.ap-southeast-1.amazonaws.com 
  - Use AWS CA certificate as ca_certificate, device_certificate and device_key with your device cert and device key.
  - Use `DIC_CLIENT_ID` macro value with your Client ID in `matter_extension/examples/platform/silabs/DIC/matter_abs_interface/inc/dic_config.h`
  - The preferred certificate type to use in the application is ECDSA.
- If using mosquitto, change the following file `matter_extension/examples/platform/silabs/DIC/matter_abs_interface/src/dic_nvm_cert.cpp` enable `USE_MOSQUITTO` and disable `USE_AWS`.
  - Under `#if USE_MOSQUITTO`
  - Use `DIC_SERVER_HOST` name with your Server host name where Mosquitto Broker is running.
  - Use OpenSSL CA certificate as ca_certificate, device_certificate and device_key.
  - `DIC_CLIENT_ID` is not required here but `DIC_CLIENT_USER` and `DIC_CLIENT_PASS` in `matter_extension/examples/platform/silabs/DIC/matter_abs_interface/inc/dic_config.h` needs to be updated as per your Mosquitto password file.
  - The preferred certificate type to use in the application is ECDSA.
