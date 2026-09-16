# Lighting application override APIs

Override each hook below by declaring the `*Impl()` method in `CustomerAppTask.h`
and implementing it in `CustomerAppTask.cpp`. Match the signature in
`autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Register the button callback, initialize the light, LED, and display. |
| `InitLightImpl` | `InitLight` | Create the off effect timer and load OnOff (and RGB color attributes when enabled) from cluster state. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Route light action and function button events. |
| `OnTriggerOffWithEffectImpl` | `OnTriggerOffWithEffect` | Select and start the timer for an OffWithEffect command. |
| `LightActionEventHandlerImpl` | `LightActionEventHandler` | Toggle the light for a button event and synchronize the OnOff attribute. |
| `LightTimerEventHandlerImpl` | `LightTimerEventHandler` | Post the event that completes an off effect. |
| `LightControlEventHandlerImpl` | `LightControlEventHandler` | Apply level and color control events to the RGB LED. Available when `SL_MATTER_RGB_LED_ENABLED` is enabled. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Route OnOff, Level Control, Color Control, and Identify attribute changes. |
