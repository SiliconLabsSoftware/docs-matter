# Light Switch application override APIs

Override each hook below by declaring the `*Impl()` method in `CustomerAppTask.h`
and implementing it in `CustomerAppTask.cpp`. Match the signature in
`autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Register the button callback, initialize the light switch endpoints, and create the level control long press timer. |
| `InitLightSwitchImpl` | `InitLightSwitch` | Set the light switch and generic switch endpoints and schedule Binding Manager initialization. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Convert hardware button activity into application button events. |
| `AppEventHandlerImpl` | `AppEventHandler` | Translate application button events into On/Off and Level Control binding actions. |
| `InitBindingHandlerImpl` | `InitBindingHandler` | Initialize the Binding Manager and register its command and context release handlers. |
| `LightSwitchChangedHandlerImpl` | `LightSwitchChangedHandler` | Send a pending On/Off or Level Control command through a matching bound peer or group. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Log Identify attribute changes. |
