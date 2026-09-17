# Rangehood Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback, initializes the rangehood, and updates the display. |
| `InitRangeHoodImpl` | `InitRangeHood` | Initializes the extractor hood endpoint and light LED from cluster state. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes fan control and function button events. |
| `ActionTriggerHandlerImpl` | `ActionTriggerHandler` | Applies light on/off actions and refreshes the UI for fan mode changes. |
| `FanControlButtonHandlerImpl` | `FanControlButtonHandler` | Toggles the fan mode for a button press. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Routes Fan Control and OnOff changes and observes Identify changes. |
