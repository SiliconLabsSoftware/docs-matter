# Oven Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback, initializes the oven, connectivity handler, cooktop LED, and display. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes oven action and function button events. |
| `OvenButtonHandlerImpl` | `OvenButtonHandler` | Converts an oven button press into a cooktop on/off action. |
| `OvenActionHandlerImpl` | `OvenActionHandler` | Applies an oven or cooktop action and updates the application UI. |
| `ConnectivityEventHandlerImpl` | `ConnectivityEventHandler` | Propagates the cooktop off state after DNS-SD initializes. |
| `InitBindingHandlerImpl` | `InitBindingHandler` | Initializes the Binding Manager and registers its command and context release handlers. |
| `CookTopBindingPropagateStateImpl` | `CookTopBindingPropagateState` | Notifies bound OnOff and Fan Control clusters of the cooktop state. |
| `BoundDeviceChangedHandlerImpl` | `BoundDeviceChangedHandler` | Writes the pending cooktop state to a matching bound OnOff or Fan Control peer. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Routes OnOff changes and observes Temperature Control and Identify changes. |
| `OnAttributeChangedImpl` | `OnAttributeChanged` | Translates an Oven Mode `CurrentMode` change into an application event. |
| `DMOvenModeClusterInitCallbackImpl` | `DMOvenModeClusterInitCallback` | No default application logic. The Oven Mode cluster init callback does nothing. |
| `DMOvenModeClusterShutdownCallbackImpl` | `DMOvenModeClusterShutdownCallback` | No default application logic. The Oven Mode cluster shutdown callback does nothing. |
| `InitOvenImpl` | `InitOven` | Initializes oven endpoints, delegates, binding, supported levels, and initial cluster state. |
| `OnOffAttributeChangeHandlerImpl` | `OnOffAttributeChangeHandler` | Synchronizes cooktop and cooking surface state after an OnOff change. |
| `IsTransitionBlockedImpl` | `IsTransitionBlocked` | Returns true when the requested Oven Mode transition is in the blocked transition list. |
