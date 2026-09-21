# Rangehood Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback, initializes the rangehood, and updates the display. |
| `InitRangeHoodImpl` | `InitRangeHood` | Initializes the extractor hood endpoint and sets the light LED based on the cluster state. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes fan-control and function-button events. |
| `ActionTriggerHandlerImpl` | `ActionTriggerHandler` | Applies light on/off actions and refreshes the UI when the fan mode changes. |
| `FanControlButtonHandlerImpl` | `FanControlButtonHandler` | Toggles the fan mode in response to a button press. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Routes attribute changes from the Fan Control and On/Off clusters and monitors attribute changes from the Identify cluster. |
