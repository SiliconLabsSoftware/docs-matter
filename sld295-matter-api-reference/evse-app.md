# EVSE application override APIs

Override each hook below by declaring the `*Impl()` method in `CustomerAppTask.h`
and implementing it in `CustomerAppTask.cpp`. Match the signature in
`autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Register the button callback, run `ApplicationInit`, and register EVSE test event triggers when enabled. |
| `ApplicationInitImpl` | `ApplicationInit` | Initialize the EVSE application and energy management LED. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Route EVSE control button presses to `EnergyManagementActionEventHandler` and function button events to the base application handler. |
| `EnergyManagementActionEventHandlerImpl` | `EnergyManagementActionEventHandler` | Log the control button event. The default does not start a charging action. |
