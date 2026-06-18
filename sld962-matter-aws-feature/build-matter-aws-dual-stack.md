# Build Procedure for Matter + AWS Dual Stack

Follow the steps below to enable the **dual-stack flavor** of Matter + AWS on a **917 NCP** project. This configuration uses IPv6 on the EFR32 host for Matter and IPv4 on the SiWx917 NWP for AWS cloud connectivity.

For an architectural overview and flavor comparison, see [Matter + AWS Dual Stack Overview](./matter-aws-dual-stack-overview.md).

For the standard Matter + AWS build (917 SoC or standard 917 NCP with host LwIP transport), see [Build Procedure for Matter + AWS](./build-matter-aws.md).

> **Note:** Dual-stack Matter + AWS is currently **alpha quality** and supported on 917 NCP boards only (BRD4186C, BRD4187C, BRD4120A).

## Prerequisites

- A **917 NCP** Matter project or the reference example `matter_wifi_917_ncp_lock_app_dual_stack_freertos`.
- Matter Extension **2.9.0** or later and WiseConnect SDK **4.1.0** or later installed in Simplicity Studio.
- AWS cloud configured per [AWS installation](./aws-configuration-registration.md).
- Hardware and software requirements met as described in [Matter + AWS Prerequisites](./index.md#prerequisites).

## Adding the AWS Server, Client ID, and Cluster Details

AWS server, client ID, and cluster configuration is the same as the standard Matter + AWS flavor. Follow the steps in [Adding the AWS Server, Client ID, and Cluster Details](./build-matter-aws.md#adding-the-aws-server-client-id-and-cluster-details) in the standard build guide to update `MatterAwsConfig.h` and refresh the Matter extension in Simplicity Studio.

## Starting Point

You can create a dual-stack Matter + AWS project in either of these ways:

1. **From the reference example** — In Simplicity Studio, create a project from `matter_wifi_917_ncp_lock_app_dual_stack_freertos` (917 NCP Lock Dual Stack), then add the Matter AWS components described below.
2. **From an existing 917 NCP project** — Adapt a 917 NCP Matter project by replacing the standard network and BLE components with the dual-stack equivalents listed in the next section.

## Adding Dual-Stack Matter + AWS Components

Configure the project using the Simplicity Studio Project Configurator. The steps below cover only the **dual-stack-specific** differences from the [standard Matter + AWS build procedure](./build-matter-aws.md#adding-the-matter--aws-component).

### 1. Enable IPv4 on the Matter Wi-Fi Component

Go to **Software Components**, search for `Matter_Wifi`. Click the **Settings** symbol beside the Matter Wi-Fi component or select **Configure**, and enable **IPV4** configuration.

This sets `CHIP_DEVICE_CONFIG_ENABLE_IPV4` in `sl_matter_wifi_config.h`, which is required for AWS cloud connectivity.

![IPV4 Component](images/matter-wifi-component.png)

![IPV4 Settings Enable](images/matter-aws-ipv4-enable-2.png)

### 2. Install Matter AWS with NWP Transport

In **Software Components**, search for `aws` and install the **AWS for Matter WiFi** component (`matter_aws`).

When prompted for the AWS transport dependency, select **Matter AWS NWP Transport (Si91x)** (`matter_aws_transport_nwp`). Do **not** select Matter AWS LwIP Transport.

![Matter AWS NWP Transport Component](images/matter-aws-dependency-3.png)

Next, select the dependencies for the Matter AWS component. The order can vary, but in every case select the option with **"+ AWS"**:

![Default Entropy Source for Matter + AWS](images/matter-aws-dependency-1.png)

![X.509 Create certificates for Matter + AWS](images/matter-aws-dependency-5.png)

![X.509 Use certificates for Matter + AWS](images/matter-aws-dependency-4.png)


### 5. Install TLS 1.2 PRF (917 NCP Requirement)

In **Software Components**, search for `TLS 1.2 PRF` and install the **TLS 1.2 PRF** component (`psa_crypto_tls12_prf`).

This step is required for all 917 NCP Matter + AWS builds, including dual-stack.

![TLS 1.2 PRF Component](images/tls-prf-component-install.png)

## Building and Flashing the Application

1. Build the dual-stack Matter + AWS application in Simplicity Studio. For 917 NCP flash and boot procedures, refer to the [917 NCP getting started documentation](/matter/{build-docspace-version}/matter-wifi-getting-started-example/getting-started-siwx917-rcp).
2. Flash both the EFR32 host application and the SiWx917 NCP connectivity firmware as required for your board.

## Verifying the Build

After building and flashing the application, confirm AWS connectivity from the device logs. You should see `[MATTER_AWS]` messages after device bootup:

```console
[00:00:23.400][info  ][SVR] [MATTER_AWS] connection callback started
[00:00:23.690][info  ][SVR] [MATTER_AWS] MQTT connection status: 0
[00:00:23.995][info  ][SVR] [MATTER_AWS] MQTT sub request callback: 0
```

After subscribing to a topic in AWS IoT, publish logs should appear in the device console and in the AWS IoT console.

![Device Logs AWS](./images/aws-device-logs-thermostat-app.png)

![AWS IoT App Data](./images/matter-aws-iot-app-data.png)

Commission the device over **EFR32 BLE** and verify Matter control with chip-tool. For end-to-end Matter and cloud testing steps, refer to [End-to-End Test of Matter + AWS Application](./index.md#end-to-end-test-of-matter--aws-application) and [Running the Matter Demo Over Wi-Fi](/matter/{build-docspace-version}/matter-wifi-run-demo).

## Compile Using New Thing for Different Certificates

Two devices should not use the same client ID. Use a different client ID for your second connection. While using AWS, update the following information:

1. Add your AWS certificates in file `examples/platform/silabs/matter_aws/matter_aws_interface/include/MatterAwsNvmCert.cpp`.

   - Provide the AWS Root CA key (https://www.amazontrust.com/repository/AmazonRootCA1.pem).
   - Provide `device_certificate` and `device_key` with your device certificate and device key. For more details, refer to [OpenSSL Device Certificate Creation](./openssl-certificate-creation.md).
  
2. Add your AWS server and client ID information to the `examples/platform/silabs/matter_aws/matter_aws_interface/include/MatterAwsConfig.h` file.

   - Provide `MATTER_AWS_SERVER_HOST` with your AWS Server name.
   - Provide `MATTER_AWS_CLIENT_ID` with your device/thing ID.

> **Note:**
> - The supported certificate type for the 917 NCP matter dual stack is RSA keys.
> - AWS Root CA used for the 917 NCP matter dual stack https://www.amazontrust.com/repository/AmazonRootCA1.pem

## Troubleshooting

- **Matter commissioning or IPv6 connectivity issues** — Ensure `SLI_SI91X_ENABLE_IPV6=1` is defined and that your network supports IPv6 SLAAC. See the IPv6 troubleshooting section in the [Matter Wi-Fi FAQ](/matter/{build-docspace-version}/matter-faq/wifi-faq).
- **AWS MQTT connection failures** — IPv4 is enabled on the Matter Wi-Fi component, and AWS server details and credentials in `MatterAwsConfig.h` and `MatterAwsNvmCert.cpp` are correct.
- **Build errors about conflicting transport** — Remove `matter_aws_transport_lwip` if present; only one AWS transport component may be installed.

For architectural context and supported board list, see [Matter + AWS Dual Stack Overview](./matter-aws-dual-stack-overview.md).
