# Oven application override APIs

Override each hook below by declaring the `*Impl()` method in `CustomerAppTask.h`
and implementing it in `CustomerAppTask.cpp`. Match the signature in
`autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Register the button callback, initialize the oven, connectivity handler, cooktop LED, and display. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Route oven action and function button events. |
| `OvenButtonHandlerImpl` | `OvenButtonHandler` | Convert an oven button press into a cooktop on/off action. |
| `OvenActionHandlerImpl` | `OvenActionHandler` | Apply an oven or cooktop action and update the application UI. |
| `ConnectivityEventHandlerImpl` | `ConnectivityEventHandler` | Propagate the cooktop off state after DNS-SD initializes. |
| `InitBindingHandlerImpl` | `InitBindingHandler` | Initialize the Binding Manager and register its command and context release handlers. |
| `CookTopBindingPropagateStateImpl` | `CookTopBindingPropagateState` | Notify bound OnOff and Fan Control clusters of the cooktop state. |
| `BoundDeviceChangedHandlerImpl` | `BoundDeviceChangedHandler` | Write the pending cooktop state to a matching bound OnOff or Fan Control peer. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Route OnOff changes and observe Temperature Control and Identify changes. |
| `OnAttributeChangedImpl` | `OnAttributeChanged` | Translate an Oven Mode `CurrentMode` change into an application event. |
| `DMOvenModeClusterInitCallbackImpl` | `DMOvenModeClusterInitCallback` | No default application logic. The Oven Mode cluster init callback does nothing. |
| `DMOvenModeClusterShutdownCallbackImpl` | `DMOvenModeClusterShutdownCallback` | No default application logic. The Oven Mode cluster shutdown callback does nothing. |
| `InitOvenImpl` | `InitOven` | Initialize oven endpoints, delegates, binding, supported levels, and initial cluster state. |
| `OnOffAttributeChangeHandlerImpl` | `OnOffAttributeChangeHandler` | Synchronize cooktop and cooking surface state after an OnOff change. |
| `IsTransitionBlockedImpl` | `IsTransitionBlocked` | Return true when the requested Oven Mode transition is in the blocked transition list. |
