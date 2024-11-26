# Attribute

Attributes represent the current state of a device. For instance if the device is on or off, the current temperature, or the current level of a dimmer. Attributes are defined in the cluster specification.

## Attribute Changes

When a ZCL attribute is updated in the data model, the framework will call the `postAttributeChangeCallback`. If this callback is implemented by the device it will be informed of the attribute change. The device may react to the attribute change. For example, in the [MatterPostAttributeChangeCallback](https://github.com/SiliconLabs/matter_extension/blob/22bfd9fe3f749ba0e1c5ca684a48b6e28a390c7f/examples/onoff-plug-app/src/ZclCallbacks.cpp#L38), say we want to add some custom handler code to control an RGB LED when on/off attribute in the `On-Off` Cluster changes:

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
        /* Custom code */
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

## Header File

This file contains the high level namespaces and constant definitions for Attributes. In Simplicity Studio, this will be generated in the autogen/zap-generated/ folder of the matter project.

- [Attribute](https://github.com/project-chip/connectedhomeip/tree/master/zzz_generated/app-common/app-common/zap-generated/ids/Attributes.h)
