# Rangehood application override APIs

Override each hook below by declaring the `*Impl()` method in `CustomerAppTask.h`
and implementing it in `CustomerAppTask.cpp`. Match the signature in
`autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Register the button callback, initialize the rangehood, and update the display. |
| `InitRangeHoodImpl` | `InitRangeHood` | Initialize the extractor hood endpoint and light LED from cluster state. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Route fan control and function button events. |
| `ActionTriggerHandlerImpl` | `ActionTriggerHandler` | Apply light on/off actions and refresh the UI for fan mode changes. |
| `FanControlButtonHandlerImpl` | `FanControlButtonHandler` | Toggle the fan mode for a button press. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Route Fan Control and OnOff changes and observe Identify changes. |
