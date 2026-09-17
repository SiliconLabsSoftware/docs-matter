# EVSE Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback, runs `ApplicationInit`, and registers EVSE test event triggers when enabled. |
| `ApplicationInitImpl` | `ApplicationInit` | Initializes the EVSE application and energy management LED. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes EVSE control button presses to `EnergyManagementActionEventHandler` and function button events to the base application handler. |
| `EnergyManagementActionEventHandlerImpl` | `EnergyManagementActionEventHandler` | Logs the control button event. The default does not start a charging action. |
