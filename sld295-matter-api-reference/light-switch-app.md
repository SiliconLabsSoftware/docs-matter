# Light Switch Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback, initializes the light switch endpoints, and creates the level control long press timer. |
| `InitLightSwitchImpl` | `InitLightSwitch` | Sets the light switch and generic switch endpoints and schedules Binding Manager initialization. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Converts hardware button activity into application button events. |
| `AppEventHandlerImpl` | `AppEventHandler` | Translates application button events into On/Off and Level Control binding actions. |
| `InitBindingHandlerImpl` | `InitBindingHandler` | Initializes the Binding Manager and registers its command and context release handlers. |
| `LightSwitchChangedHandlerImpl` | `LightSwitchChangedHandler` | Sends a pending On/Off or Level Control command through a matching bound peer or group. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Logs Identify attribute changes. |
