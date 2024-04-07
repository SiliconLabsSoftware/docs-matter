# Matter Intermittently Connected Devices (ICD)

Matter introduces the concept of Intermittently Connected Devices (ICD) in the SDK and in the specification. An Intermittently Connected Device is the Matter representation of a device that is not always reachable. This covers battery-powered devices that disable their underlying hardware when in a low-power mode or devices that can be disconnected from the network, like a phone app.

This page focuses on features designed to improve the performance and reliability of battery-powered devices. Matter ICD functionality can be enabled with the `matter_icd_management` component. The Matter light-switch and lock examples are ICDs by default.

## ICD Device Types

Matter introduces two types of ICDs.

- Short Idle Time ICDs
- Long Idle Time ICDs

### Short Idle Time ICDs

Short Idle Time ICDs are battery powered devices that can always be reached by clients. This means that their polling intervals are small enough to guarantee that a message sent from a client will be able to reach the ICD without any synchronization. A door lock, for example, is typically a short idle time ICD because it needs to be able to receive commands from clients at any given time. These devices are usually not the initiators in the communication flow.

### Long Idle ICDs

Long Idle Time ICDs are battery powered devices that require synchronization between the client and the ICD for communication to succeed. A sensor device is an example of a device that are typically long idle time ICDs.

Long Idle Time ICDs are provisional with the Matter 1.2 release.

## ICD Management Cluster

The ICD Management Cluster enables configuration of the ICD’s behavior. It is required for an ICD to have this cluster enabled on endpoint 0.

The ICDM Cluster exposes three configuration attributes that enable to configure an ICD.

:::custom-table{width=18%,10%,13%,59%}
| Attribute | Type | Constraints | Description |
|-|-|-|-|
| IdleModeInterval      | uint32 | 1 to 64800 | Maximum interval in seconds or milliseconds the server can stay in idle mode |
| ActiveModeInterval    | uint32 | min 300    | minimum interval in milliseconds the server will stay in active mode |
| ActiveModeThreshold   | uint32 | min 300    | minimum amount of time in milliseconds the server typically will stay active after network activity when in active mode |
:::

These configurations can be changed by modifying the values within `sl_matter_icd_config.h` or within the settings of the `matter_icd_management` component.

```cpp
    #define SL_IDLE_MODE_INTERVAL = 600     // 10min Idle Mode Interval
    #define SL_ACTIVE_MODE_INTERVAL = 1000  // 1s Active Mode Interval
    #define SL_ACTIVE_MODE_THRESHOLD = 500  // 500ms Active Mode Threshold
```

## Creating an ICD Example via Simplicity Studio

### Enabling/Building

To begin creating an OpenThread ICD example, create a generic Matter over Thread solution example via the **New Project Wizard**. Lighting solution example will be used for demonstration purposes.

**Lock and Light-Switch applications come out-of-box with ICD enabled. The low power component can be added by user.**

1. Create project.

    ![Project Generation](images/icd-project-generation.png)

2. Navigate to the **Configuration Tools** section and open the **Zigbee Cluster Configurator**.

    ![ICD ZAP](images/icd-open-zap.png)

3. Search for the ICD Management cluster and enable for **Server**. You will receive a warning that the corresponding component was unable to be installed. This is due to component conflicts within Simplicity Studio.

    ![ICD Cluster](images/icd-enable-icd-cluster.png)

4. Navigate to the **Software Components** tab and install the ICD Management Server Cluster component.

    ![ICD Component](images/icd-install-icd-component.png)

5. Replace all subsequent conflicting components via the ensuing pop-up options (See below). This will install the necessary Thread Network Layer (MTD) component and ICD source code. This will also remove the conflicting Thread Network Layer (FTD) component.

    ![ICD Component Conflicts](images/icd-resolve-conflicts.png)

**Recommended: Install the `matter_platform_low_power` and `matter_subscription_synchronization` components to achieve further energy savings. See details below.**

ICD functionality should be installed and ready to build. Build the project as you would a normal example and flash the resulting binary to your specified end device. You should be able to commission the device the same way as non-ICD examples using the QR code URL (generated within the RTT logs at startup or **BTN0** press).

## **Power Saving Components**

### **Minimal Power Consumption**

The Lower Power Mode component is optional for low-power builds with the component `matter_platform_low_power`.

The Lower Power Mode component will disable:

- Matter Shell
- OpenThread CLI
- LCD and QR Code
  
### **Persistent Subscriptions**

Persistent subscriptions were added to Matter as a means to ensure that an ICD can re-establish its subscription and by extension its secure session to a subscriber in the event of a power cycle. When a device accepts a subscription request, it will persist the subscription. When the device reboots, it will try to re-establish its subscription with the subscriber. If the subscription is torn down during normal operations or if the re-establishment fails, the subscription will be deleted.

Persistent subscriptions are enabled by default on all Silicon Labs sample applications via the `matter_subscription_persistence` component.

### **Subscription Timeout Resumption**

Matter also provides a retry mechanism for devices to try to re-establish a lost subscription with a client. This functionality is provided by the component `matter_subscription_timeout_resumption`. This feature should not be used on an ICD since it can significantly reduce battery life.

This feature is enabled by default on all examples with the exception of the door-lock and light-switch example.

### **Subscription Synchronization**

To avoid forcing an ICD to become active multiple times, the Matter SDK allows an ICD to synchronize its subscription reporting and send all the reports at the same time. The mechanism synchronizes the maximum interval of all subscriptions to only require the ICD to become active once. This functionality is provided by component `matter_subscription_synchronization`.

This feature is enabled by default on the door-lock sample app and the light-switch sample application.

## **Configuration**

To change default values corresponding to Matter ICD examples, modify them in either:

1. `config/sl_matter_icd_config.h`
2. ICD component configurator

![ICD Configuration](images/icd-config.png)

## Subscription Maximum Interval

The subscription mechanism is used by ecosystems and controllers to receive attribute change updates and liveness checks. The maximum interval of a subscription request is what defines the frequency at which a device will send a liveness check if there are no attribute changes.

Within the subscription request / response model, a device has the opportunity to decide the maximum interval at which it will send its liveness check (Empty Report Update). The device can set a maximum interval within this range if and only if it is an ICD:

```shell
MinIntervalRequested ≤ MaxInterval ≤ MAX(IdleModeInterval, MaxIntervalRequested)
```

The following table shows the subscribe response fields.
| Action Field | Type | Description |
|-|-|-|
| SubscriptionId | uint32 | identifies the subscription |
| MaxInterval | uint16 | the final maximum interval for the subscription in seconds |

### Maximum Interval Negotiation

The Matter SDK provides a default implementation that allows an ICD to negotiate its MaxInterval. The goal of the algorithm is to set the MaxInterval to the IdleModeInterval.

```cpp
#if CHIP_CONFIG_ENABLE_ICD_SERVER

    // Default behavior for ICDs where the wanted MaxInterval for a subscription is the IdleModeInterval
    // defined in the ICD Management Cluster.
    // Behavior can be changed with the OnSubscriptionRequested function defined in the application callbacks

    // Default Behavior Steps :
    // If MinInterval > IdleModeInterval, try to set the MaxInterval to the first interval of IdleModeIntervals above the
    // MinInterval.
    // If the next interval is greater than the MaxIntervalCeiling, use the MaxIntervalCeiling.
    // Otherwise, use IdleModeInterval as MaxInterval

    // GetPublisherSelectedIntervalLimit() returns the IdleModeInterval if the device is an ICD
    uint32_t decidedMaxInterval = GetPublisherSelectedIntervalLimit();

    // Check if the PublisherSelectedIntervalLimit is 0. If so, set decidedMaxInterval to MaxIntervalCeiling
    if (decidedMaxInterval == 0)
    {
        decidedMaxInterval = mMaxInterval;
    }

    // If requestedMinInterval is greater than the IdleTimeInterval, select next active up time as max interval
    if (mMinIntervalFloorSeconds > decidedMaxInterval)
    {
        uint16_t ratio = mMinIntervalFloorSeconds / static_cast<uint16_t>(decidedMaxInterval);
        if (mMinIntervalFloorSeconds % decidedMaxInterval)
        {
            ratio++;
        }

        decidedMaxInterval *= ratio;
    }

    // Verify that decidedMaxInterval is an acceptable value (overflow)
    if (decidedMaxInterval > System::Clock::Seconds16::max().count())
    {
        decidedMaxInterval = System::Clock::Seconds16::max().count();
    }

    // Verify that the decidedMaxInterval respects MAX(GetPublisherSelectedIntervalLimit(), MaxIntervalCeiling)
    uint16_t maximumMaxInterval = std::max(GetPublisherSelectedIntervalLimit(), mMaxInterval);
    if (decidedMaxInterval > maximumMaxInterval)
    {
        decidedMaxInterval = maximumMaxInterval;
    }

    // Set max interval of the subscription
    mMaxInterval = static_cast<uint16_t>(decidedMaxInterval);

#endif // CHIP_CONFIG_ENABLE_ICD_SERVER
```

If the default implementation does fit within the use-case, an implementation can override the default implementation. The first step is to implement the `ApplicationCallback` class from the `ReadHandler.h` header.

```cpp
/*
 * A callback used to interact with the application.
 */
class ApplicationCallback
{
public:
    virtual ~ApplicationCallback() = default;
    /*
     * Called right after a SubscribeRequest has been parsed and processed. This notifies an interested application
     * of a subscription that is about to be established. It also provides an avenue for altering the parameters of the
     * subscription (specifically, the min/max negotiated intervals) or even outright rejecting the subscription for
     * application-specific reasons.
     *
     * TODO: Need a new IM status code to convey application-rejected subscribes. Currently, a Failure IM status code is sent
     * back to the subscriber, which isn't sufficient.
     *
     * To reject the subscription, a CHIP_ERROR code that is not equivalent to CHIP_NO_ERROR should be returned.
     *
     * More information about the set of paths associated with this subscription can be retrieved by calling the appropriate
     * Get* methods below.
     *
     * aReadHandler:            Reference to the ReadHandler associated with the subscription.
     * aSecureSession:          A reference to the underlying secure session associated with the subscription.
     *
     */
    virtual CHIP_ERROR OnSubscriptionRequested(ReadHandler & aReadHandler, Transport::SecureSession & aSecureSession)
    {
        return CHIP_NO_ERROR;
    }
    /*
     * Called after a subscription has been fully established.
     */
    virtual void OnSubscriptionEstablished(ReadHandler & aReadHandler){};
    /*
     * Called right before a subscription is about to get terminated. This is only called on subscriptions that were terminated
     * after they had been fully established (and therefore had called OnSubscriptionEstablished).
     * OnSubscriptionEstablishment().
     */
    virtual void OnSubscriptionTerminated(ReadHandler & aReadHandler){};
 };
```

The second step is registering the callback object to the Interaction Model Engine.

```cpp
// Register ICD subscription callback to match subscription max intervals to its idle time interval
chip::app::InteractionModelEngine::GetInstance()->RegisterReadHandlerAppCallback(&mICDSubscriptionHandler);
```
