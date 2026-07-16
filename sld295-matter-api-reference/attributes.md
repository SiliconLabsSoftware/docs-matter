# Attribute

Attributes represent the current state of a device. For instance if the device is on or off, the current temperature, or the current level of a dimmer. Attributes are defined in the cluster specification.

## Attribute Changes

Depending on your sample app, instructions apply. For more information, refer to [Application customization models](/matter/{build-docspace-version}/matter-references/custom-matter-device/#application-customization-models).

### New Architecture

When a ZCL attribute is updated in the data model, the framework invokes the post-attribute-change path. The Silicon Labs Matter stack routes this as follows: `MatterPostAttributeChangeCallback` in `BaseApplication.cpp` → `AppTask::DMPostAttributeChangeCallback` in `autogen/AppTask.cpp` → your optional `DMPostAttributeChangeCallbackImpl()` override in `CustomerAppTask`.

If this callback is implemented by the device, it is informed of the attribute change. The device may react to the attribute change. For example, in `DMPostAttributeChangeCallback` function the in `AppTask.cpp` file ([onoff-plug-app/src](https://github.com/SiliconLabsSoftware/matter_sdk/blob/main/examples/onoff-plug-app/silabs/src/AppTask.cpp)), if you want to add a custom handler code to control an RGB LED when on/off attribute in the `On-Off` Cluster changes, implement the following in `DMPostAttributeChangeCallbackImpl` in `src/CustomerAppTask.cpp`:

```cpp
void DMPostAttributeChangeCallbackImpl(const chip::app::ConcreteAttributePath & attributePath,
                                                      uint8_t type,
                                                      uint16_t size,
                                                      uint8_t * value)
{
    ClusterId clusterId     = attributePath.mClusterId;
    AttributeId attributeId = attributePath.mAttributeId;
    ChipLogProgress(Zcl, "Cluster callback: " ChipLogFormatMEI, ChipLogValueMEI(clusterId));

    if (clusterId == OnOff::Id && attributeId == OnOff::Attributes::OnOff::Id)
    {
        if (*value) 
        { // turn on LED
            sl_led_turn_on((sl_led_t *)&sl_simple_rgb_pwm_led_rgb_led0);
        } 
        else 
        {// turn off LED
            sl_led_turn_off((sl_led_t *)&sl_simple_rgb_pwm_led_rgb_led0);
        }
        /* ----------- */
    }

    //...
}
```

### Legacy Architecture

When a ZCL attribute is updated in the data model, the framework calls `MatterPostAttributeChangeCallback()` in `src/DataModelCallbacks.cpp`. If this callback is implemented by the device it will be informed of the attribute change. For example, to control an RGB LED when the On/Off attribute changes:

```cpp
void MatterPostAttributeChangeCallback(const chip::app::ConcreteAttributePath & attributePath,
                                        uint8_t type,
                                        uint16_t size,
                                        uint8_t * value)
{
    ClusterId clusterId     = attributePath.mClusterId;
    AttributeId attributeId = attributePath.mAttributeId;
    ChipLogProgress(Zcl, "Cluster callback: " ChipLogFormatMEI, ChipLogValueMEI(clusterId));

    if (clusterId == OnOff::Id && attributeId == OnOff::Attributes::OnOff::Id)
    {
        if (*value)
        { // turn on LED
            sl_led_turn_on((sl_led_t *)&sl_simple_rgb_pwm_led_rgb_led0);
        }
        else
        {// turn off LED
            sl_led_turn_off((sl_led_t *)&sl_simple_rgb_pwm_led_rgb_led0);
        }
    }

    //...
}
```

## Header File

This file contains the high level namespaces and constant definitions for Attributes. In Simplicity Studio, this will be generated in the autogen/zap-generated/ folder of the matter project.

- [Attribute](https://github.com/SiliconLabs/matter_extension/blob/main/third_party/matter_sdk/zzz_generated/app-common/app-common/zap-generated/ids/Attributes.h)
