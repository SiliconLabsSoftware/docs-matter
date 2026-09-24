# Lighting Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback, initializes the light, LED, and display. |
| `InitLightImpl` | `InitLight` | Creates the off-effect timer and loads the OnOff attribute and, when enabled, the RGB color attributes from the cluster state. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes light action and function button events. |
| `OnTriggerOffWithEffectImpl` | `OnTriggerOffWithEffect` | Selects and starts the timer for an OffWithEffect command. |
| `LightActionEventHandlerImpl` | `LightActionEventHandler` | Toggles the light for a button event and synchronizes the OnOff attribute. |
| `LightTimerEventHandlerImpl` | `LightTimerEventHandler` | Posts the event that completes an off effect. |
| `LightControlEventHandlerImpl` | `LightControlEventHandler` | Applies level and color control events to the RGB LED. Available when `SL_MATTER_RGB_LED_ENABLED` is enabled. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Routes OnOff, Level Control, Color Control, and Identify attribute changes. |
